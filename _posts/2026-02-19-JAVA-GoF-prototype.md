---
title: Creational_Prototype Pattern
categories: [JAVA, GoF]
tags: [] # TAG names should always be lowercase
---

## ✅

- create a new instance
- by copying an existing instance
- the existing instance has a `clone() method`

- `the existing instance` == `new copied instance` ➡️ false
- `the existing instance`.equals(`new copied instance`) ➡️ true

## ✅ Diagram

[![image.png](https://i.postimg.cc/nLb9XSv2/image.png)](https://postimg.cc/RWdZ8RpJ)

## 👍🏻

- when creating an instance is resource expensive
- 👀 connecting to database, connecting to network

## 👎🏻 If we did not have prototype pattern...

- cannot clone an existing instance

```java
GithubIssue githubIssue1 = new GithubIssue(repository);

//before prototype
//have to create new instance with constructor
GithubIssue githubIssue2 = new GithubIssue(repository);
GithubIssue githubIssue3 = githubIssue.clone(); // This will not work❌
```

## ✅ clone() from `Object class`

- Java by default provides the `clone()` method from `Object class`

#### ✔️ Cloneable interface

- the class we want to clone must `implement Cloneable()`

```java
public class GithubIssue implements Cloneable{
    private int id;
    private String title;
    private GithubRepository repository;

    //then override clone()
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    //and override equals()
    //bc cloned instance and existing instance should be equal
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof GithubIssue that)) return false;
        return id == that.id && Objects.equals(title, that.title) && Objects.equals(repository, that.repository);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, title, repository);
    }
}
```

#### ✔️ Main class

- ❓ `existing instance` and `cloned instance` will have same memory? ❌
- ❓ `existing instance` and `cloned instance` will have same value? `equals()`? ⭕️
- ❓ `existing instance` and `cloned instance` will have same `.getClass()`? ⭕️

- ⚠️ Default `clone()` from Java is a swallow copy
- so, the `Repository` of `existing instance` and `cloned instance` are the same ⭕️

```java
GithubIssue githubIssue1 = new GithubIssue(repository);

GithubIssue githubIssue3 = (GithubIssue) githubIssue1.clone();

// githubIssue1 == githubIssue3  => false
// githubIssue1.equals(githubIssue3) => true
// githubIssue1.getClass() == githubIssue3.getClass() => true
// githubIssue1.getRepository() == githubIssue3.getRepository() => true, shallow copy
```

## Swallow copy 🆚 Deep copy

- In `GithubIssue`, it has `Repository` as its field
- in **swallow copy**, the `cloned instance` will have the same `Repository` as the `existing instance`
- if `existing instance`'s `Repository` changes,
- `cloned instance`'s `Repository` will also change

- In **deep copy**, `cloned instance` will have its own `Repository`
- Even if `existing instance`'s `Repository` changes,
- `cloned instance`'s `Repository` will NOT change

## ✅ Create my own clone() for deep copy

- If I want `cloned instance` to have a complete separate `Repository`
- should not use `clone()` from Java ❌
- Can create my own `clone()`

#### ✔️ Create my own clone()

- This way, we can have deep copy

```java
public class GithubIssue implements Cloneable{
    private int id;
    private String title;
    private GithubRepository repository;

    //create new repository
    //and return the newly created instance
    @Override
    protected Object clone() throws CloneNotSupportedException {
        GithubRepository repository = new GithubRepository(); //create new repository
        repository.setUser(this.repository.getUser());
        repository.setName(this.repository.getName());

        GithubIssue issue = new GithubIssue(repository); //new instance
        issue.setId(this.id);
        issue.setTitle(this.title);

        return issue;
    }
```
