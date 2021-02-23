---
title: Design Patterns | Prototype
date: 2021-02-08 13:55:19
tags:
---
**Creational** pattern - **Prototype**

Use cases: 

- you need  a chance to have a copy of given object without coupling on object's dependency classes 
- your code shouldn't depend on conrete realization of class 
- when you add some specific configuration to classes and want to supply your object with this config 

Example: 

{% github_include AbdybaevAE/data-blog/master/patterns-go/4.go go %}

Here we define basic interface inode that have clone and print functions.

{% github_include AbdybaevAE/data-blog/master/patterns-go/5.go go %}

Structure <code>file</code>code that *implements* inode interface.

{% github_include AbdybaevAE/data-blog/master/patterns-go/6.go go %}

Structure <code>folder</code>code that *implements* inode interface.

{% github_include AbdybaevAE/data-blog/master/patterns-go/7.go go %}

Initialize filesystem and create identical copy.
{% github_include AbdybaevAE/data-blog/master/sh/1.sh sh %}