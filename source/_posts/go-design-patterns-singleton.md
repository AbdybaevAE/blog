---
title: Design Patterns | Singleton
date: 2021-02-07 19:35:16
tags:
---

**Creational** pattern - **Singleton**

{% github_include AbdybaevAE/data-blog/master/patterns-go/1.go go %}

Here we define package cards, that encapsulates relationship between card number and and owner of a card. It's concurency free function <code>func New() </code>code, that creates object only if it's not initialized before. 

Below you can find the basic usage of this pattern:

{% github_include AbdybaevAE/data-blog/master/patterns-go/2.go go %}

Sample output of program shows that there are no another instance was created. 