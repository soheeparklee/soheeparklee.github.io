---
title: Structural_Facade Pattern
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅ Facade

- provide a **👍🏻 simplified, unified interface** to a **👎🏻 complex subsystem**
- define a high level interface
- that makes the subsystem easier to use

- 👎🏻 client interacts with many classes and complicated workflow
- 👍🏻 client just interacts with single facade class
- facade class does all the underlying difficult job, coordiate the sub components

- 👀 Like having a remote control in a smart home
- to control lights, speaker, caldera...

## ✅ Diagram

[![Screenshot-2026-03-06-at-17-35-01.png](https://i.postimg.cc/hGz0FvC6/Screenshot-2026-03-06-at-17-35-01.png)](https://postimg.cc/NytXmsvk)

## 👀

#### ✔️ sub types of file

- has class of file reading, writing and deleting

```java
class FileReader {
    public String readFile(String filePath){
        //read file function
    }
}

class FileWriter {
    public void writeFile(String filePath, String content){
      //write file function
    }
}

class FileDeleter {
    public void deleteFile(String filePath){
      //delete file function
    }
}
```

#### ✔️ Fascade class

- like a remote control that controls everything related to files

```java
class FileSystemFacade {
    private FileReader fileReader;
    private FileWriter fileWriter;
    private FileDeleter fileDeleter;

    public FileSystemFacade() {
       //constructor
    }

    public String readFile(String filePath) {
      //manage read file
      fileReader.readFile(filePath)
    }

    public boolean writeFile(String filePath, String content) {
        //manage write file
        fileWriter.writeFile(filePath, content);
    }

    public boolean deleteFile(String filePath) {
        //maange delete file
        fileDeleter.deleteFile(filePath);
    }
}
```

#### ✔️ Main class

```java
// 👎🏻 before
// client has to know
FileWriter fileWrite = new FileWriter();
fileWrite.writeFile(); //need to write each subsystem
FileReader fileRead = new FileReader();
fileRead.readFile();

// 👍🏻 after
// client just has to call FileSystemFacade class
// FileSystemFacade will do everything!

FileSystemFacade fs = new FileSystemFacade();

// Write to file
fs.writeFile();

// Read from file
fs.readFile("test.txt");

// Delete file
fs.deleteFile("test.txt");
```

## 🛠️

- **Logger Factory**
- `Logger logger = LoggerFactory.getLogger(MyClass.class);`
- `LoggerFactory` acts as a facade over different logging implementations

- **DriverManager**
- `Connection conn = DriverManager.getConnection(url);`
- `DriverManager` acts as a facade for DB drivers
