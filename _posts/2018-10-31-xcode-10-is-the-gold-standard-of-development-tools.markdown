---
layout: post
title: Xcode 10 is the Gold Standard of Development Tools
date: '2018-10-31 14:10:47'
tags:
- macos
- xcode
- ios
---

Xcode 10 is a fantastic update to an already great piece of software for developing and debugging apps. Xcode allows you to easily create an iPhone app or a Mac app that you can launch and sell on the App Store.

![Xcode-10-1](/assets/images/2018/10/Xcode-10-1.png)

Are there bugs? Yes. 

Can it be improved? Yes. 

Is Apple fixing bugs? Yes.

[Xcode 10](https://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12) brings many improvements to the editor experience including multiple cursors, multiple selections, code folding, and enhancements to Playgrounds.

Error messages in Xcode have gone from unhelpful to extremely helpful with the latest release of Xcode. And if I ever do come across a strange error, searching on Google or StackOverflow has always pointed me in the right direction.

Xcode is vastly better than Visual Studio and other code integrated development environments (IDEs) because of several key reasons. Read on, so that you can understand what makes Xcode stand out.

## What Xcode Enables

With Xcode, I'm able to easily take an idea to the App Store to make $$$ (i.e.: [Super Easy Timer](https://itunes.apple.com/us/app/super-easy-timer/id1353137878?ls=1&mt=12)).

[![icon_256x256](/assets/images/2018/10/icon_256x256.png)](https://itunes.apple.com/us/app/super-easy-timer/id1353137878?ls=1&mt=12)

![0-App-Store-Connect-Super-Easy-Timer-Sales-October-2018](/assets/images/2018/10/0-App-Store-Connect-Super-Easy-Timer-Sales-October-2018.png)

[Download Xcode 10](https://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12) today and get started making that app you've always wanted to make.

## Xcode vs. Visual Studio

Xcode 10 is far easier to use than Visual Studio, which is overloaded with so many buttons and hidden settings. In Xcode I can easily configure a project to work with FAT libraries (32/64/simulator/device), and in Visual Studio I have to manage every single library for 32 and 64 bit (and debug and release, which is a nightmare due to 4x the number of clicks drilling in/out of Visual Studio project settings).

Cocoapods and workspaces make it super easy to get started with an open source framework that allows me to stand on the shoulders of the giants in the iOS/Mac development community.

The Address Sanitizer and Thread Sanitizer have both helped me solve so many bugs that slipped through the cracks when I was working in C and C++ cross-platform code (Windows/macOS). Debugging threads on Visual Studio is a nightmare as the threads change randomly (as you step through code), while in Xcode it's effortless to follow and doesn't randomly jump.

![Xcode memory and thread debugging is amazing](/assets/images/2018/10/1-Xcode-10-thread-sanitizer-address-sanitizer-.png)

I much prefer developing in Xcode than Visual Studio, even though I first started programming in Visual Studio 6 with C++ back in 2004. I grew up on Windows computers, and I didn't start using Mac computers until 2008. But now I can't go back to Windows. The experience and the development environment is better on Mac. (The only downfall is Mac gaming performance)

Apple understands easy-to-use software and manages to simplify complex tasks intuitively. The prominent "play" button is an outstanding example of why Xcode is easier to use. It doesn't overcomplicate the UI and provides a great development experience for starting your app right away. For contrast, take a look at Visual Studio and tell me what button, out of the 20+ buttons makes the project build. (Hint sometimes in Visual Studio it's not even visible!)

![Xcode 10 Play Button is Easy](/assets/images/2018/10/Xcode-Play.png)

Compare Xcode 10 to Visual Studio 2017.

![Mobile Development with Visual Studio 2017 (Microsoft)](/assets/images/2018/10/Mobile-development-with-.NET_copy_opt.jpg)

## Bugless?

Is Xcode bugless? No. 

There are numerous issues, but every piece of software I use has bugs. Sometimes the bugs get in the way, but many times there are workarounds. Read the release notes.

I've heard that Xcode doesn't work well with large code bases (100,000+ lines), but since I'm only working on small apps, that hasn't been a problem for me. And there are probably ways to make large code bases work well and rookie mistakes that will make builds take forever. If you invest time in learning how to leverage Xcode's strengths and best practices that will help improve your daily development experience.

## Room for Improvement

Right now I have around 19 bugs I need to submit for Xcode, so it's not bug-free. What I love about Apple is that they're far more responsive to bugs than they used to be. Many of my bugs have been resolved, and I'm not worried when I see a duplicate bug report, because I can now see (in Bug Report) when the original bug # gets fixed.

The visual designer in Storyboard files is extremely helpful at understanding how Auto Layout works (I'm writing a book on [Auto Layout for beginners](https://pages.convertkit.com/e119bf9a85/858c1c1a46)). In my apps, I use a mix of Storyboard files, .xib files, and programmatic UIs. Overall storyboards have been the best way to visually design app UIs that scale to the numerous retina displays in customer's hands.

In Storyboard files, there are some zoom and clicking quirks, but I look forward to Apple fixing these bugs. I'd love to get zoom support back in Mac Storyboard files, as right now I have to use the Accessibility Zoom to see the "pixels" I need to nudge around.

It would be nice to see Apple go through the initial "onboarding experience" to make it easier to get started. I find that there are a lot of "false positive" errors on the initial setup experience as you make your first app. Many times that means cleaning, rebuilding, enabling/disabling your development credentials, or restarting Xcode.

## Playgrounds Are Almost Great

Playgrounds in the "Manual" mode feel far more stable than any prior version of Xcode. It was fun to write a little tool to pull down search ranking stats for my iOS and Mac apps using Playgrounds. 

BUT, there are still some "indeterministic run" bugs with Playground so they can be hard for a beginner to use. They don't always run, and even sometimes will get stuck in an endless loop, preventing them from running the code.

The keyboard shortcuts don't always work to run the Playground — my workaround is to press the Play/Stop button in the bottom left corner. Hopefully, Apple will fix my bug reports and make Playgrounds even better for beginners!

![Playgrounds upgraded in Xcode 10](/assets/images/2018/10/Playgrounds-Upgrade-in-Xcode-10.png)

I'm not sure if Apple's going to enable debugging in Playgrounds, but it feels like a missing feature. 

Without debugging it's much harder to write the correct code, and with the frequent API changes as Swift has migrated the entire SDK, this has been a bit challenging at times. 

My workaround when Playgrounds don't work is to use a Mac Command Line app to test Swift code, or a throwaway iOS project when I needed to check an iOS feature.

## Report Xcode Bugs

If you have a problem, submit a [bug report](http://bugreport.apple.com) to Apple with the expected, actual, and steps to reproduce the issue.

## Comments

What do you think? Do you like Xcode?

Have you reported any bugs?

Reach out on Twitter [@PaulSolt](http://twitter.com/PaulSolt) or comment below.