---
title: Design Patterns | Abstract Factory
date: 2021-03-15 02:38:35
tags:
---

**Creational** pattern - **Abstract Factory**

Use cases:

- when you need to work with related classes while decoupling it on concrete classes 
- Consumer of your factory can easily use your factory methods and do not worry about compatibility of objects from different sub types 

Example: 

Define <code>iShirt and shirt</code>:

{% github_include AbdybaevAE/data-blog/master/patterns-go/14.go go %}

Define <code>iShoe and shoe</code>:

{% github_include AbdybaevAE/data-blog/master/patterns-go/15.go go %}

Define concrete<code>nike</code>:

{% github_include AbdybaevAE/data-blog/master/patterns-go/16.go go %}

Define concrete<code>adidas</code>:

{% github_include AbdybaevAE/data-blog/master/patterns-go/17.go go %}

Define <code>iWearFactory</code>:

{% github_include AbdybaevAE/data-blog/master/patterns-go/18.go go %}

Simple usage:

{% github_include AbdybaevAE/data-blog/master/patterns-go/19.go go %}

