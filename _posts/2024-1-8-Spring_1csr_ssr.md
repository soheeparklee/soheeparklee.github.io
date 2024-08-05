---
title: SPA, SSR, CSR
categories: [Computer Science, WEB]
tags: [csr, ssr] # TAG names should always be lowercase
---

## ✅ SPA

> Single Page Application <br>
> Once page is loaded, only change content(no page loading) <br>

## ✅ CSR, SSR

rendering: 정보를 보여주기 <br>
정보를 누가 보기 쉽게 뿌려주는가?<br>

## ☑️ CSR

> Client Side Rendering

클라이언트(웹)이 주도적으로 렌더링 <br>
👍🏻 클라이언트가 자원 할당 가능 <br>
👍🏻 프론트엔드, 백엔드 업무 분리 가능 <br>
👍🏻 read only the needed data(instead of reading the whole page) <br>
👍🏻 faster than SSR <br>
👍🏻 reduce traffic <br>
👍🏻 user experience: no need to refresh page <br>
👎🏻 difficult for search croller to collect serach data <br>

## ☑️ SSR

> Server Side Rendering

서버가 주도적으로 렌더링을 해서 페이지를 보여줌 <br>
👍🏻 처음 로딩속도가 빠름 <br>
👍🏻 일관된 렌더링이 가능하다 <br>
👍🏻 search engine <br>

## ✅ thymeleaf로 SSR 구현

```java
@Controller
public class SampleSSRController {
    @GetMapping("/sample")
    public String samplePage(Model model){
        List<SampleData> sampleDataList = new ArrayList<>();
        sampleDataList.add(new SampleData(1, "sample item1"));
        sampleDataList.add(new SampleData(2, "sample item2"));
        sampleDataList.add(new SampleData(3, "sample item3"));
        sampleDataList.add(new SampleData(4, "sample item4"));
        sampleDataList.add(new SampleData(5, "jack"));

        //model에다가 dataList를 추가할 것이다.
        model.addAttribute("dataList", sampleDataList);
        return "samplePage";
    }
}

```

<img width="351" alt="스크린샷 2024-01-08 오후 1 35 00" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/0e3bb737-2384-454a-ba50-32df221890b5">

## ✅ JS fetch로 Restful API CSR 구현

```java
//CSR은 rest controller
@RestController
@RequestMapping("/api")
public class SampleCSRController {
    @GetMapping("/sample")
    public List<SampleData> getSamplelist(){
        List<SampleData> sampleDataList= new ArrayList<>();
        sampleDataList.add(new SampleData(1, "sample item1"));
        sampleDataList.add(new SampleData(2, "sample item2"));
        sampleDataList.add(new SampleData(3, "sample item3"));
        sampleDataList.add(new SampleData(4, "sample item4"));
        sampleDataList.add(new SampleData(5, "client"));

        return sampleDataList;
    }

}
```
