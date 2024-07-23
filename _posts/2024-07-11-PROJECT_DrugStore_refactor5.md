---
title: TroubleShooting_Concurrency issue
categories: [Project, Drug Store Project]
tags: [project, trouble]
---

## ✅ Concurrency Issue

Complex issue related to concurrent purchases of a popular product with limited stock.
Multiple users attempted to buy the last few units of the product simultaneously,
leading to race conditions where the stock count was not updated accurately, causing **overselling**.

## 🔵 Refactor 1. Database locking

> prevent race conditions
> When a user initiates a purchase, a lock is placed on the product's stock row until the transaction completes

### ☑️ Database locking

- row-level locking: only that row lock, least restrictive lock
- table-level locking
- page-level locking
- pessimistic locking: no other transaction can modify until lock is released
- optimistic locking: multiple transactions can acess data, but checks for data changes

### ☑️ Why pessimistic locking?

pessimistic locking

> once a transaction reads a row,
> prevents other transactions from accessing until the first one completes.

1. High likelihood of conflicts(row-level not adequate❌)
2. Immediate locking
3. Maintain data integrity

#### 🆚 Comparision with other locking mechanisms

- row-level
  - row-level is suitable for low conflict rates. However, this issue seems hightly likely.
- table-level
  - Overly restrictive. Multiple transactions need to access different rows in same table
- page-level
  - Not as precise as row-level locking
- optimistic level
  - suitable for low conflict rates. would lead to frequent transaction rollbacks and retries.

## 🟢 Outcome, Benefits

- eliminate chance of race conditions
- maintain data integrity
- sutability for high-conflic scenarios

#### ✔️ @Transactional

Before

```java
    //pessimistic database locking
    public void optionStockChange(List<OptionQuantityDto> optionQuantityDtoList) {
        for(OptionQuantityDto o: optionQuantityDtoList){
            int optionId = o.getOptionId();
           Options options= optionsRepository.findById(optionId)
                   .orElseThrow(()-> new NotFoundException("Cannot find option with ID"));
            int orignialOptionStock= options.getStock();
            int orderedStock= o.getQuantity();
            options.setStock(orignialOptionStock - orderedStock);
            optionsRepository.save(options);
        }
    }
```

After

```java
    //pessimistic database locking
    @Transactional
    public void optionStockChange(List<OptionQuantityDto> optionQuantityDtoList) {
        for(OptionQuantityDto o: optionQuantityDtoList){
            int optionId = o.getOptionId();
            Options options= optionsRepository.findByIdWithLock(optionId) //repository change
                    .orElseThrow(()-> new NotFoundException("Cannot find option with ID"));
            int orignialOptionStock= options.getStock();
            int orderedStock= o.getQuantity();
            options.setStock(orignialOptionStock - orderedStock);
            optionsRepository.save(options);
        }
    }
```

#### ✔️ Repository

```java
@Repository
public interface OptionsRepository extends JpaRepository<Options,Integer> {
    //other methods...

    @Lock(LockModeType.PESSIMISTIC_WRITE)
    @Query(
            "SELECT o FROM Options o " +
                    "WHERE o.optionsId = :optionId "
    )
    Optional<Options> findByIdWithLock(int optionId);
}
```

#### ✔️ For save order, delete cart as well

In order service, `optionId` was found from `Option Repository` for **saving order** and **deleting from cart** as well.
For these methods, implement `@Transaction` and `lock` as well.

```java
    @Transactional
    public void deleteFromCart(User user, List<OptionQuantityDto> optionQuantityDtoList) {
        for(OptionQuantityDto o: optionQuantityDtoList){
            Options options= options
            Repository.findByIdWithLock(o.getOptionId())
                    .orElseThrow(()-> new NotFoundException("Cannot find option with ID"));


            Cart cart= cartRepository.findByUserIdAndOptionId(user.getUserId(), options.getOptionsId())
                    .orElseThrow(() -> new NotFoundException("There is no product in cart with matching user and option."));

            //finally delete cart
            cartRepository.delete(cart);
        }
    }

    @Transactional
    public String saveOrder(User user, Integer optionId, String ordersNumber, LocalDate orderAt){

        Options options= optionsRepository.findByIdWithLock(optionId)
                .orElseThrow(()-> new NotFoundException("Cannot find option with ID"));

        Orders orders= Orders.builder()
                .user(user)
                .options(options)
                .ordersNumber(ordersNumber)
                .ordersAt(orderAt)
                .build();
        ordersRepository.save(orders);
        return "order saved successfully";
    }
```

## 🔵 Refactor 2. Atomic Operations

> ensure the stock count was decremented correctly without interference from other transactions.

```java
synchronized (product) {
    if (product.getStock() < requestedQuantity) {
        throw new NotEnoughStockException("Requested quantity exceeds available stock.");
    }
    product.setStock(product.getStock() - requestedQuantity);
    productRepository.save(product);
}
```

## 🔵 Refactor 3. Retry Mechanism

> handle deadlock scenarios gracefully. If a transaction failed due to a deadlock, it was automatically retried.

```java
int retries = 3;
while (retries > 0) {
    try {
        // Attempt transaction
        break; // Break on success
    } catch (DeadlockException e) {
        retries--;
        if (retries == 0) throw e; // Rethrow exception if out of retries
    }
}
```
