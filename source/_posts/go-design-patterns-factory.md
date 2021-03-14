---
title: Design Patterns | Factory
date: 2021-03-14 23:23:31
tags:
---

**Creational** pattern - **Factory**

Use cases:

- when you don't know what exact types and dependencies your code should support 
- when you want to extend some properties of objects that you provide
- when you want to save resources by providing existing objects 

Pros: 

- avoid coupling of between creator and concrete type 
- ability to add new types without breaking old code 
- more control on code because there are one place where your objects are creating

Example: 

Define <code>Product</code> interface with single method <code>GetCost()</code>:

{% github_include AbdybaevAE/data-blog/master/patterns-go/10.go go %}

Define two concrete types of <code>Product</code>:

{% github_include AbdybaevAE/data-blog/master/patterns-go/11.go go %}

Define factory that will create for us <code>Product</code> types:

{% github_include AbdybaevAE/data-blog/master/patterns-go/12.go go %}

Example of usage:

{% github_include AbdybaevAE/data-blog/master/patterns-go/13.go go %}

