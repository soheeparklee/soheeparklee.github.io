---
title: Request Body
categories: [Backend, FastAPI]
tags: [backend, requestbody, fastapi] # TAG names should always be lowercase
---

## ✅ Request Body

> When you need to send data from a client (let's say, a browser) to your API, you send it as a request body.

**Request body**

data sent by the client to your API

**Response body**

data your API sends to the client

<img width="516" alt="스크린샷 2023-11-18 오후 12 10 23" src="https://github.com/soheeparklee/portfolioWebsite_dreamcoding/assets/97790983/ad15dc78-6dd8-4d25-adf9-87db8c4291ad">

## ✅ Import Pydantic's `BaseModel`

💡 to declare a **request** body, you use `Pydantic`

you need to import BaseModel from pydantic:

## ✅ Create your data model

decalre a data model as a `class` that inherits from `BaseModel`

```python
class Person (BaseModel):
    name: str
    description: str
    age: float
    level: float
```

this will decalre a JSON `object` like

```
{
    "name": "So Hee",
    "description": "Glasses",
    "age": 27,
    "level": 3,
}
```

## ✅ Declare as a paramteter

```python
@app.post("/persons/")
async def create_person(person: Person):
    return person
```

and declare as the type model you created, `Person`

## ☑️ Result

**FastAPI** will

- read the body of the request as `JSON`
- Convert the corresponding types and Validate the data
- Give you the recieved data in the parameter `person`

## ✅ Use the model

Inside the function, you can access all the attribute of the model object directly

```python
@app.post("/persons/")
async def create_person(person: Person):
    person_dict= person.dict()
    if person.age:
        class = person.age+ person.level
        person_dict.update({"class": class})
    return person_dict
```

## ✅ Request body + path parameters

decalre path parameters and request body at the same time!

- function parameters that match path parameters should be **taken from the path**
- function parameters that are declared to be Pydantic models should be **taken from the request body**

```python
@app.put("/persons/{person_id}")
async def create_person(person_id: int, person: Person):
    return {"person_id": person_id}
```

## 💟 reference

<https://fastapi.tiangolo.com/ko/tutorial/body/>
