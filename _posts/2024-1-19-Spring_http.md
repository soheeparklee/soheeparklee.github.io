---
title: Cache, HTTP Cache, E-tag, Spring Cache
categories: [JAVA, Spring]
tags: [cache, cashing, etag] # TAG names should always be lowercase
---

## ✅ Cache

> 원래 데이터 소스보다 더 효율적으로 액세스 할 수 있는 **임시 저장소**

특정 API/아이템 20%가 전체 로직의 80%의 쿼리를 차지
이 API/아이템를 자주 쓰니까 어디 가까운 곳에 저장해 두면 좋을 것 같아

Key-value구조로 저장한다.
Cache 저장소가 너무 커지면 임시 저장소 사용하는 의미가 없으니, 크기가 과하게 커지는 것을 지양
웹 브라우저 안에 HTTP Cache가 있다.
Spring Container안에 Spring Cache가 있다. 굳이 DB에 가서 매번 가져오는 것이 아니라!

## ✅ HTTP Cache

> HTTP Client 요청에 대한 응답값의 임시 저장소

HTTP header을 보면 cache 사용했는지 알 수 있음

- cache control: 어떤 방식으로, 얼마동안 캐싱할 것인가
- expire: 캐싱 응답 만료 시점
- X-cache: cache Hit(내부적으로 가지고 있는 값이 있으면 그걸로 처리) 해당 요청 값이 캐시로 응답
- cache location: 해당 cache가 어디에 저장되어 있는가?

👎🏻 HTTP Cache 아쉬운 점

- HTTP Cache 쓴다고 SQL문을 안 쓰는 건 아니다.
- 그래서 서버 속도에 큰 변화는 없음... ➡️ Spring Cache도 사용!

## ⭐️ Cache Validation(HTTP cache)

> cache가 Valid 한 상태인지 파악해야 한다.

❓ HTTP Cache사용하는데 DB내용이 바뀌면?
HTTP 쇼핑몰 홈페이지에서는 item이 2만원인 줄 알았는데, DB에서 아이템 가격을 3만원으로 바꿔버림!

⭐️ If-Mofied-Since (시간)
일정 시간마다 cache가 바뀌었는지 확인한다.
일정 시간을 정해두고 나 N시간만큼 지났는데 바뀐 cache있어?

⭐️ E-tag 이용(ID비교)
나 이런 ID를 가지고 있는데, 바뀐 cache있어?

이렇게 E-tag를 추가하면 HTTP header에 아이디가 생긴다.
이 아이디를 보냈을 때 **@304 Not Modified** 오면 바뀐게 없다는 뜻이다.

```java
//e-tag 추가하는 방법

public class EtagWebConfig {
    @Bean
    public FilterRegistrationBean<ShallowEtagHeaderFilter> shallowEtagHeaderFilterFilter(){
        FilterRegistrationBean<ShallowEtagHeaderFilter> filterRegistrationBean = new FilterRegistrationBean<>();
        filterRegistrationBean.setFilter(new ShallowEtagHeaderFilter());
        filterRegistrationBean.addUrlPatterns("/api/*");
        return filterRegistrationBean;
    }
}

```

## ✅ Spring Cache

일반적으로 service layer에다가 넣는다.
데이터 그냥 받아오기만 하는 메소드 **@Cacheable**
데이터를 변경하거나 삭제하는 메소드 **@CacheEvict**

```java
//Spring Cache 값 넣기
public class ItemService {
//매번 아이템 찾는데, 그냥 spring cache에 저장하기로
    @Cacheable(value= "items", key = "#root.methodName")
    public List<Item> findAllItems() {
        List<ItemEntity> itemEntities=  electronicStoreItemJpaRepository.findAll(); //jpa가 findAllItems바로 실행
        return itemEntities.stream().map(ItemMapper.INSTANCE::itemEntityToItem).collect(Collectors.toList());
    }

    @Cacheable(value= "items", key= "#id")
    public Item findItemById(String id) {
        Integer idInt= Integer.parseInt(id);
        ItemEntity itemEntity= electronicStoreItemJpaRepository.findById(idInt).orElseThrow(()->new NotFoundException("No Item with Id found"));
        Item item= ItemMapper.INSTANCE.itemEntityToItem(itemEntity);
        return item;
    }

    @Cacheable(value= "items", key= "#ids")
    public List<Item> findItemsByIds(List<String> ids) {
        List<ItemEntity> itemEntities= electronicStoreItemJpaRepository.findAll();
        List<Item> items= itemEntities.stream()
                .map(Item::new)
                .filter((item->ids.contains(item.getId())))
                .collect(Collectors.toList());
        return items;
    }
}
```

```java
//Spring Cache 초기화해서 다 지우기
//❓ 만약 delete, update해서 데이터 바뀌면? 새롭게 초기화해야한다.

//데이터가 바뀌는 메소드에는 CacheEvict를 써야 한다.
    //allEntries: 모든 cache 데이터 바꿔라
    @CacheEvict(value="items", allEntries = true)
    public Integer saveItem(ItemBody itemBody) {
        ItemEntity itemEntity= ItemMapper.INSTANCE.idAndItemBodyToItemEntity(null, itemBody);
        ItemEntity itemEntityCreated;
        try{
            itemEntityCreated= electronicStoreItemJpaRepository.save(itemEntity);
        } catch(RuntimeException exception){
            throw new NotAccpetExcpetion("Error while saving item");
        }
        return itemEntityCreated.getId();
    }

        @CacheEvict(value="items", allEntries = true)
    public void deleteItem(String id) {
        Integer idInt= Integer.parseInt(id);
        electronicStoreItemJpaRepository.deleteById(idInt);
    }
    @CacheEvict(value="items", allEntries = true)
    @Transactional(transactionManager = "tmJpa1")
    public Item updateItem(String id, ItemBody itemBody) {

        Integer idInt= Integer.valueOf(id);
        ItemEntity itemEntityUpdated= electronicStoreItemJpaRepository.findById(idInt).orElseThrow(()-> new NotFoundException("No Item with Id found"));

        itemEntityUpdated.setItemBody(itemBody);


        return ItemMapper.INSTANCE.itemEntityToItem(itemEntityUpdated);
    }
```
