---
title: SQL Injection
categories: [Database, SQL]
tags: [] # TAG names should always be lowercase
---

## ✅ SQL Injection

> Malicious SQL by a hacker to be transmitted to DB, attacking the data

## 😈 SQL Injection Attack

1. Delete data attack

- when user logs in, inputs ID and password
- hacker would add SQL to
  when the ID, password is true, delete user
- results in unintended alternation of DB

2. Reveal Data

- hacker intentionally makes error
- when the error appears, get additional message to know database design, use it for hacking

## 💊 Prevention

1. When recieving input, check for typographical symbols

- add logic to prevent login when typographical symbols`$%()*?` are input

2. If SQL error occurs, hide error message

- prevent hacker from accessing DB
- prevent hacker from getting hints of DB architecture

3. use preparestatement

- When preparestatement is used, typographical symbols are escaped
- thus, recieves `????` instead of typographical symbols
