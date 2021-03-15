---
title: Design Patterns | Adapter
date: 2021-03-15 20:15:31
tags:
---

**Structural** pattern - **Adapter**

It allows you to connect objects with different interfaces. 

Use cases:

- When you have existing classes, but its' interfaces isn't compatible with your code 

Let's imagine next situation: 

You wanna stream your computer desktop(with VGA OUTPUT) on TV. You only have VGA connector. In case if your TV compatible with VGA you just need to plug in connector, otherwise you need to get an adapter which convert all your computer signals to proper destination. 

1. Define <code>VGAClient</code>. In this case this will be your connector with VGA output 
2. Define two types of devices that support VGA and HDMI Inputs
3. Define two concrete classes of <code>VGADevice and HDMIDevice</code>
4. Create and adapter that accepts hdmi signal and convert it to VGA

{% github_include AbdybaevAE/data-blog/master/patterns-go/20.go go %}