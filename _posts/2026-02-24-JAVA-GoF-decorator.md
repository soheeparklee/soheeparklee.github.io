---
title: Structural_Decorator
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## 🛠️

- add behavior to object dynamically without modifying their class
- wrap an object with another object(**decorator**)

## ✅ Structure and Diagram

[![Screenshot-2026-03-06-at-15-17-18.png](https://i.postimg.cc/WzGfc7V7/Screenshot-2026-03-06-at-15-17-18.png)](https://postimg.cc/ZvqLrpC9)

## 👀

[![Screenshot-2026-03-06-at-16-12-01.png](https://i.postimg.cc/zBngJrSB/Screenshot-2026-03-06-at-16-12-01.png)](https://postimg.cc/njhzkNWb)

- Like in HTML, we decorate text like `<b> <u> <i> Text </i> </u> </b>`

```
Component ➡️ BoldDecorator ➡️ UnderlineDecorator ➡️ ItalicDecorator
```

#### 1. Base Component(interface)

- common interface

```java
interface Text{
    String getContent();
}
```

#### 2. Concrete Component

- base implementation

```java
class PlainText implements Text{
    private String content;

    public PlainText(String content){
        this.content = content;
    }

    @Override
    public String getContent(){
        return content;
    }
}
```

#### 3. Base Decorator

- holds a reference to the wrapped component

```java
abstract class TextDecorator implements Text{
    protected Text text;

    public TextDecorator(Text text){
        this.text = text;
    }

    @Override
    public String getContent(){
        return text.getContent();
    }
}
```

#### 4. Concrete Decorators

- extends the `base decorator` and behavior

```java
class BoldDecorator extends TextDecorator{
    public BoldDecorator(Text text){
        super(text);
    }

    @Override
    public String getContent(){
        return "<b>" + super.getContent() + "</b>";
    }
}

class UnderlineDecorator extends TextDecorator{
    public UnderlineDecorator(Text text){
        super(text);
    }

    @Override
    public String getContent(){
        return "<u>" + super.getContent() + "</u>";
    }
}

class ItalicDecorator extends TextDecorator{
    public ItalicDecorator(Text text){
        super(text);
    }

    @Override
    public String getContent(){
        return "<i>" + super.getContent() + "</i>";
    }
}
```

#### 5. Using the decorators in main class

```java
public class Main{
    psvm{
        Text plainText = new PlainText("hello"); //hello
        Text boldText = new BoldDecorator(new PlainText("hello")); //<b> hello </b>
        Text boldUnderlineItalicText = new BoldDecorator(new UnderlineDecortator(new ItalicDecorator(new PlainText("hello")))); //<b> <u> <i> hello </i> </u> </b>

    }
}
```

## 🛠️

```java
DataInputStream in =
    new DataInputStream(
        new BufferedInputStream(
            new FileInputStream("data.txt")
        )
    );
```

- `InputStream` → Component
- `FileInputStream` → Concrete component
- `FilterInputStream` → Decorator base class
- `BufferedInputStream`, `DataInputStream` → Concrete decorators
