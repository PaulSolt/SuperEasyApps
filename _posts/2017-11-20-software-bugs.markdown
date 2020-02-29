---
layout: post
title: Software Bugs . . .
date: '2017-11-20 12:29:00'
tags:
- bugs
---

One thing that can be frustrating is how easy it is to create bugs—both unintentionally and from in-experience.

* A good tester understands how to use software and thinks of creative ways to break it.
* A good tester is someone who's observant of the details, and that's what makes them good.
* A good tester is can put themselves into the shoes of a customer and use the software, game, or app without any "understanding" of how the app should be used.

## A good tester is unconventional. ##

They can quickly spot a quirk, or they see a small detail that others miss.

Then they make several hypothesis's for what might be wrong.

They then test that quirk, and they exercise different edge cases to understand it better.

For example, I'm working on a new timer app for Mac: **Super Easy Timer**

<iframe src='https://gfycat.com/ifr/DisfiguredDependableDegus' frameborder='0' scrolling='no' width='300' height='178' allowfullscreen></iframe>

I discovered that when the window is offscreen (so the center isn't visible), and I click the "Fullscreen button", it jumps to my second monitor.

I expected it to stay on my current monitor, not my second monitor.

## Full-screen Bug ##


![Half-Offscreen-Timer-App](/content/images/2017/11/Half-Offscreen-Timer-App.png)

The second monitor (my MacBook Pro's retina display) has the timer app in full-screen, but it's not where you expect it to be as a user.

It should have been on my primary monitor (5K LG UltraFine)

![Wrong-Monitor-Fullscreen](/content/images/2017/11/Wrong-Monitor-Fullscreen.png)


## How do you cultivate this testing philosophy? ## 

You have to use software, and you have to use it often.

Most bugs I find are issues that fall into two categories: 

1. I've either seen before in other apps
2. They are issues that are discovered by chance.

The only way you can discover this bugs is if you use the software.

BUT . . . you need to be willing to invest time into actually using the software in different situations that might exercise different features.

## Testing different edge cases . . . ##

1. Does feature X work on single (dual) screen systems? (i.e. computer configuration testing)
2. Does it work for different types of input? (i.e.: large numbers, small numbers, positive numbers, negative numbers)
3. What happens when you type words instead of numbers?
4. What happens when you type special symbols instead of words?
5. What happens if you use a huge image, or a small image?
6. What if you set a setting to a very large number or a small number?
7. What happens if you click very quickly or type really fast?
8. What if you toggle between settings quickly?
9. What happens when you click buttons multiple times in a row?
10. What happens when you click buttons in different orders?

## Beta Test the Super Easy Timer ##

<script async id="_ck_298469" src="https://forms.convertkit.com/298469?v=6"></script>


Signup above to beta test Super Easy Timer and learn more about creating software for macOS and iOS.

## What are you testing? ##

Share your story below.