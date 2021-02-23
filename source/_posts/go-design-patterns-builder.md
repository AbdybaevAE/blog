---
title: Design Patterns | Builder
date: 2021-02-09 18:55:49
tags:
---
**Creational** pattern - **Builder** 

Use cases: 

- technique that allows to encapsulate construction logic for an object while creating  
- break up construction of complex object into smaller parts and decople construction from its representation that can be reused to create different representations 

Let's look at the example:

{% github_include AbdybaevAE/data-blog/master/patterns-go/8.go go %}

The main idea is next: 

- <code>MessageFormat</code> defines two formats of message(xml, json)
- <code>Message</code> type  define two fields(body of message and format)
- <code>MessageBuilder</code> common interface for builder object with corresponding methods for setters and <code>Build()</code> function
- <code>JsonBuilder</code> and <code>XmlBuilder</code> are concrete implementations <code>MessageBuilder</code> interface. It creates messages in two different formats 
- <code>Sender</code> is *director* class that creates message. It accepts a <code>MessageBuilder</code> type and build it. And it doesn't really matter what exactly type of <code>MessageBuilder</code>

{% github_include AbdybaevAE/data-blog/master/patterns-go/9.go go %}

Basic usage. Define director class and pass two different builders of <code>MessageBuilder</code> type. 

{% github_include AbdybaevAE/data-blog/master/sh/3.sh sh %}

Sample output.
