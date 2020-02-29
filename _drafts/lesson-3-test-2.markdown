---
layout: post
title: Lesson 3 Test 2
---

# Lesson 3: How to Connect UI to Code


NEW Video Embmed (720x405)

<script charset="ISO-8859-1" src="//fast.wistia.com/assets/external/E-v1.js" async></script><div class="wistia_embed wistia_async_oas9dzzmbt" style="height:405px;width:720px">&nbsp;</div>

[If you haven't already setup Xcode, or you want to learn how to install your app on your iPhone, jump back to Lesson 1.](https://supereasyapps.squarespace.com/iphone-apps-101-lesson-1)

Welcome to Lesson 3 of iPhone Apps 101!

You're in the right spot if you've never written any Swift code (or any code for that matter) before. And if you're coming from an previous version of Swift, you'll learn how to write code that works with iOS 11 and Swift 4.


Today you will work to make the design that you implemented interactive, and you'll connect the UI (User Interface) to the code.

## Outcomes ##

1. How to connect UI and code
2. How to write Swift 4 code basics
3. How to hide the keyboard
4. How to create modular code blocks
5. How to animate the iPhone screen

## First, Download the Resources and Sample Code for Lesson 3 ##

<script async id="_ck_285158" src="https://forms.convertkit.com/285158?v=6"></script>

The Lesson 3 download contains all of the design graphics, app mockups, and sample code (beginning and end) so that you can follow along.

## UI Connections ##

Have you ever used an app that made you smile?

Here is a description that has a footnote.[^descriptiveFootnote]
		
[^descriptiveFootnote]: The footnote should be descriptive
        
Apps are truly personal experiences that you can use to help or entertain people around the world.

To make your app interactive, you will need to setup some connections between the UI (user interface) that you designed and the related code files.

In Xcode you'll be working between two files: the Storyboard file and the ViewController.swift file.

Linking these two files together allows you to make buttons respond to user input and update labels with new information.

## Connect the Storyboard UI to Swift 4 Code ##

If this is your first time writing code, or Swift code, make sure you follow along. If you get stuck, just pause the video and try to figure out what doesn’t match.

**Important:** Code is spelling and case sensitive!

**Video**

<script src="//fast.wistia.com/embed/medias/j38ihh83m5.jsonp" async></script>
<script src="//fast.wistia.com/assets/external/E-v1.js" async></script>
<div class="wistia_embed wistia_async_j38ihh83m5" style="height:349px;width:620px">&nbsp;</div>

<script src="//fast.wistia.com/embed/medias/oas9dzzmbt.jsonp" async></script>
<script src="//fast.wistia.com/assets/external/E-v1.js" async></script>
<div class="wistia_embed wistia_async_oas9dzzmbt" style="height:349px;width:620px">&nbsp;</div>



<iframe src="https://fast.wistia.net/embed/iframe/oas9dzzmbt?videoFoam=true"
allowtransparency="true" frameborder="0" scrolling="no" class="wistia_embed"
name="wistia_embed" allowfullscreen mozallowfullscreen webkitallowfullscreen
oallowfullscreen msallowfullscreen width="640" height="360"></iframe>
<script src="//fast.wistia.net/assets/external/iframe-api-v1.js"></script>

If you can't figure it out start over again, and try it one more time.

## Keyboard 101 ##

Any time a user taps on a text field (UITextField) the keyboard will automatically appear.

Your app needs to tell the iPhone what to do when the user is finished typing (only you know!) and how to update your UI.

Depending on where the user is typing, you may find that keyboard covers part of your screen. 

One easy way to fix the keyboard problem is to move your screen up, and I'll show you how to do that in this lesson.




## Download the Swift 4 Code and Xcode Project ##

<script async id="_ck_285158" src="https://forms.convertkit.com/285158?v=6"></script>



## Challenges ##


Try doing the entire lesson again, but this time do it without watching the video. Start from scratch. Start with the "3.0 - Tip Calculator UI - Begin" Xcode project and do it again.

**The more you practice going through the motions, the more it will make sense.**

* **Bonus 1**: Using the `print()` statement, display a custom message with the value of the `billTextField.text!` attribute for a UITextField (read the UITextField reference below).

* **Bonus 2**: Trying changing the value of a tip label dynamically when the Calculate Tip button is pressed. Just make it say "Hi" or something funny. `tip1.text = "hi"` (read more about UILabels in the reference below).

## Links ##

* [UITextField Reference](https://developer.apple.com/documentation/uikit/uitextfield) - text input areas for users to type in
* [UILabel Reference](https://developer.apple.com/documentation/uikit/uilabel) - text that you can position any where on the iPhone screen
* [UIButton Reference](https://developer.apple.com/documentation/uikit/uibutton) - a button to confirm or do an action
* [NotificationCenter Reference](https://developer.apple.com/documentation/foundation/notificationcenter) - Used to listen for events about the keyboard
* [Notification Programming Topics](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/Notifications/Articles/NotificationCenters.html) - additional reference materials on notifications


## Summary ##

In this lesson you learn about working with text input and managing the user experience with the keyboard.

You learned how to make the keyboard dismiss using the UIControl's `resignFirstResponder()` method, and you learned how to animate the entire iPhone screen using keyboard events.

All of your UI is connected, and you can start working with values.

If you had any issues following along, send me an email: [Paul@SuperEasyApps.com](mailto:Paul@SuperEasyApps.com)

-Paul

P.S. Check your email for Lesson 4 tomorrow where you will add the Swift 4 logic to control the tip calculations.