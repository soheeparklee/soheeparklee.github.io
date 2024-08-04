---
title: Browser
categories: [Computer Science, WEB]
tags: [] # TAG names should always be lowercase
---

## ✅ Main components of the broswer

> browser follows HTML and CSS rules based on W3C `world wide web consortium` <br>
> Each tab runs in a seperate process(multiple instances of rendering engine) <br>

<img width="595" alt="Screenshot 2024-08-03 at 09 48 27" src="https://github.com/user-attachments/assets/7f12c771-5be0-4db5-b1f5-2d9c49163947">

### 1. User Interface

> where user interacts with the browser <br>

- address bar
- next buttons
- home button
- refresh
- all parts except the window where requested web page is displayed

### 2. Browser Engine

> bridge between user interface and rendering engine <br>

### 3. Rendering Engine

<img width="623" alt="Screenshot 2024-08-03 at 10 01 21" src="https://github.com/user-attachments/assets/dee00bf1-fb6f-4e34-9c6b-7cda7b27384d">

> render the requested web page on the browser screen <br>
> interprete HTML, XML documents and images <br>
> interpete CSS, generate the layout that is displayed on UI <br>

- Different browser different rendering engine
  - Chrome: Blink
  - Chrome iphone & Safari: Webkit

### 4. Networking

> retrieves the URLs using HTTP or FTP <br>
> handle internet communication, security <br>

- use cache of documents to reduce network traffic

### 5. Javascript Interpreter

> interprete, execute JS <br>
> interpreted results are sent to rendering engine for display <br>

### 6. UI Backend

> draw widgets <br>
> not platform specific <br>

### 7. Data persistence/storage

> persistence layer <br>
> small database created on the local drive of the computer where browser is installed <br>
> store data such as cookies, cache, bookmarks, preferenes <br>

## 💡 DOM

> Document Object Model <br>
> how web browser interpretes HTML <br>

<img width="394" alt="Screenshot 2024-08-03 at 09 38 45" src="https://github.com/user-attachments/assets/60e26df5-df9c-49c6-a9af-8171508cf35f">

## 💡 Parsing

> interprete document so that browser can understand code <br>

## ✅ Summary of how browser works

1. Enter URL, hit enter, request is sent to server <br>
2. `Rendering engine` `parse` through HTML, construct `DOM tree` <br>
3. Then `parse` CSS, making style <br>
4. With HTML, CSS, construct `render tree`. This render tree will create page with resources and style <br>
5. `Layout` of the render tree <br>
6. `Painting` the rendering tree with UI backend painting. <br>
7. Rendering Engine display content on the screen as soon as possible for better user experience. Painting and Layout does not wait for HTML parsing to be complete. Display content while rest of content still keeps coming from the network. <br>

## 💡 Reference

<https://medium.com/@yaduvanshineelam09/how-does-web-browsers-work-ec0f171aedc6>
