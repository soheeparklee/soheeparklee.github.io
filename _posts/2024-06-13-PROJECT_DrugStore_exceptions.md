---
title: Exceptions Handling
categories: [Project, Drug Store Project]
tags: [project, exceptions]
---

## ✅ Mid-Feedback results

1️⃣ What if there are 100 users buying the same item at the same time? <br>
2️⃣ What if there is 0 product left?<br>
3️⃣ What if the product is not sold anymore?<br>
4️⃣ What if the user wants to buy more items than stock?<br>
5️⃣ What if the user has no money, but wants to buy?<br>

## ✔️ Service

```java
@Service
@RequiredArgsConstructor
public class OrderService {

    @Transactional
    public ResponseDto cartToOrder(CustomUserDetails customUserDetails) {
        //...other methods

        //재고 예외처리 method
        List<OptionQuantityDto> optionQuantityList =  cartList.stream().map(c-> new OptionQuantityDto(c.getOptions().getOptionsId(), c.getQuantity()))
                        .collect(Collectors.toList());
        exceptionCheck(optionQuantityList);


        if(!cartList.isEmpty()) {
            //save order JPA
            //order response DTO

            return new ResponseDto(HttpStatus.OK.value(), "order page show success", orderResponseDto);
        }else{
            throw new EmptyException("유저의 장바구니가 비었습니다.");
        }
    }

    //주문에서 결제로
    public ResponseDto orderToPay(CustomUserDetails customUserDetails, PayRequestDto payRequestDto) {
        List<OptionQuantityDto> optionQuantityList= payRequestDto.getOptionQuantityDto();
        //재고 예외처리
        exceptionCheck(optionQuantityList);

        //사용자가 가진 돈이 주문하려는 금액보다 적으면 예외처리
        User user = userRepository.findById(customUserDetails.getUserId())
                .orElseThrow(() -> new NotFoundException("아이디가  " + customUserDetails.getUserId() + "인 유저를 찾을 수 없습니다."));
        Integer totalPrice = payRequestDto.getTotalPrice();
        if (totalPrice > user.getMoney()) throw new NoMoneyException("You do not have enough money to order");

        try {
            //pay method

            return new ResponseDto(HttpStatus.OK.value(), "주문 성공");
        }catch(Exception e){
            e.printStackTrace();
            return new ResponseDto(HttpStatus.BAD_REQUEST.value(), "주문 실패");
        }
    }




    //재고처리
    private void exceptionCheck(List<OptionQuantityDto> optionQuantityDtoList)  throws SoldOutException, NotEnoughStockException, ProductStatusException{
        for(OptionQuantityDto o: optionQuantityDtoList){
            Options options= optionsRepository.findById(o.getOptionId())
                    .orElseThrow(()-> new NotFoundException("Cannot find option with ID"));
            int buyQuantity=  o.getQuantity();
            int optionQuantity= options.getStock();
            if(optionQuantity==0) throw new SoldOutException("This product is sold out");
            else if(buyQuantity>optionQuantity) throw new NotEnoughStockException("Not possible. Product: "+ options.getProduct().getProductName() + " Option: "+ options.getOptionsName() + "Only "+ optionQuantity +"products available.");
            else if(!options.getProduct().isProductStatus()) throw new ProductStatusException("This product is not available at the moment.");
        }
    }
}
```

## ✔️ ExceptionControllerAdvice

```java

@RestControllerAdvice
@Slf4j
public class ExceptionControllerAdvice {
    //...other exceptions...

    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler(NotEnoughStockException.class)
    public ResponseEntity<ResponseDto> handleNotEnoughStockException(NotEnoughStockException nee){
        log.error("Client 요청에 문제가 있어 다음처럼 출력합니다. " + nee.getMessage());
        ResponseDto responseDto = new ResponseDto(HttpStatus.BAD_REQUEST.value(), nee.getMessage());
        return new ResponseEntity<>(responseDto, HttpStatus.BAD_REQUEST);
    }

    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler(SoldOutException.class)
    public ResponseEntity<ResponseDto> handleSoldOutException(SoldOutException soe){
        log.error("Client 요청에 문제가 있어 다음처럼 출력합니다. " + soe.getMessage());
        ResponseDto responseDto = new ResponseDto(HttpStatus.BAD_REQUEST.value(), soe.getMessage());
        return new ResponseEntity<>(responseDto, HttpStatus.BAD_REQUEST);
    }

    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler(ProductStatusException.class)
    public ResponseEntity<ResponseDto> handleProductStatusException(ProductStatusException pse){
        log.error("Client 요청에 문제가 있어 다음처럼 출력합니다. " + pse.getMessage());
        ResponseDto responseDto = new ResponseDto(HttpStatus.BAD_REQUEST.value(), pse.getMessage());
        return new ResponseEntity<>(responseDto, HttpStatus.BAD_REQUEST);
    }

    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler(NoMoneyException.class)
    public ResponseEntity<ResponseDto> handleNoMoneyException(NoMoneyException nme){
        log.error("Client 요청에 문제가 있어 다음처럼 출력합니다. " + nme.getMessage());
        ResponseDto responseDto = new ResponseDto(HttpStatus.BAD_REQUEST.value(), nme.getMessage());
        return new ResponseEntity<>(responseDto, HttpStatus.BAD_REQUEST);
    }
}
```

## ⭐️ Result

### ✔️ cart to order

#### 💡 SoldOutException

<img width="699" alt="Screenshot 2024-06-18 at 12 01 53" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/afa7c797-3614-4742-a086-189056e8076d">

#### 💡 ProductStatusException

<img width="692" alt="Screenshot 2024-06-18 at 12 02 22" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/8d28bec8-640c-4240-b729-488fa12fb22e">

### ✔️ order to pay

#### 💡 SoldOutException

<img width="1030" alt="Screenshot 2024-06-14 at 15 43 31" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/00cf0b09-4c67-4e28-8df8-43023797dcf5">

#### 💡 NotEnoughStockException

<img width="1026" alt="Screenshot 2024-06-14 at 15 43 13" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/3848ed61-c86b-42ba-9282-f4dc69fe822c">

#### 💡 ProductStatusException

<img width="697" alt="Screenshot 2024-06-18 at 12 13 40" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/2f0a6615-607c-4d60-8061-e94c40c420ec">

#### 💡 NoMoneyException

<img width="604" alt="Screenshot 2024-06-14 at 16 02 47" src="https://github.com/soheeparklee/Backend-shoppingMall-Mar2024/assets/97790983/c8f69615-7aec-470d-8c60-7bfe2abf4100">
