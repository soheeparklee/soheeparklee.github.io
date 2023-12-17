---
title: Inner Class, Transparent Class
categories: [JAVA, JAVA_Basics]
tags: [inner, transparent] # TAG names should always be lowercase
---

## ✅ Single Turn

프로그램 상에서 특정 인스턴스가 **딱 한 개**만 있어야 할 때, 사용하는 기능
(이 인스턴스는 모두 같은 주소를 가질 것임)

```java
//  ⭐️ 이 클래스를 싱글턴으로 만들기
public class Setting {
    // 클래스(정적) 필드
    // - 프로그램에서 메모리에 하나만 존재
    private static Setting setting;

    //  ⭐️ 생성자를 private으로!
    // - 외부에서 생성자로 생성하지 못하도록
    private Setting () {}

    //  💡 공유되는 인스턴스를 받아가는 public 클래스 메소드
    public static Setting getInstance() {
        //  ⭐️ 아직 인스턴스가 만들어지지 않았다면 생성
        //  - 프로그램에서 처음 호출시 실행됨
        if (setting == null) {
            setting = new Setting();
        }
        return setting;
    }

    private int volume = 5;

    public int getVolume() {
        return volume;
    }
    public void incVolume() { volume++; }
    public void decVolume() { volume--; }
}

public class Tab {
    //  ⭐️ 공유되는 유일한 인스턴스를 받아옴
    private Setting setting = Setting.getInstance();

    public Setting getSetting() {
        return setting;
    }
}
//실행클래스

Tab tab1 = new Tab();
Tab tab2 = new Tab();
Tab tab3 = new Tab();

System.out.println(tab1.getSetting().getVolume());
System.out.println(tab2.getSetting().getVolume());
System.out.println(tab3.getSetting().getVolume());

System.out.println("\n- - - - -\n");

tab1.getSetting().incVolume();
tab1.getSetting().incVolume();

System.out.println(tab1.getSetting().getVolume());
System.out.println(tab2.getSetting().getVolume());
System.out.println(tab3.getSetting().getVolume());

//  🎉 외부에서 각 사용처들을 신경쓸 필요 없음
```
