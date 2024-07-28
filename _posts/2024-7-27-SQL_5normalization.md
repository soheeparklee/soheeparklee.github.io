---
title: Normalization
categories: [Database, Database]
tags: [] # TAG names should always be lowercase
---

## ✅ Normalization

> reduce data **repetition**, increase data integerty

## ✔️ 1NF(First Normal Form)

> table column to have one atomic value <br>
> Don't use multiple fields in a single table to store similar data <br>

- one phone number per user

## ✔️ 2NF

> Create separate tables for sets of values that apply to multiple records. <br>
> Relate these tables with a foreign key <br>

- user address is used in customer table, orders, shipping, invoices table.
- do not repeat this field as a seperate entry in all tables, but place it on customer table and set foreign key

## ✔️ 3NF

> Elimiate fields that don't depend on key

## 💡 Reference

<https://learn.microsoft.com/en-us/office/troubleshoot/access/database-normalization-description>
<https://gyoogle.dev/blog/computer-science/data-base/Normalization.html>
