---
layout: post
title: How To Fix Spotlight Search On Mac (Spotlight Search Not Showing Apps)
date: '2018-07-12 14:57:34'
tags:
- macos
- bugs
- quick-fix
- productivity
---

Is Spotlight broken? Can't find the app, document, or photo you want using Spotlight on your Mac? You can fix it in 5 seconds using Terminal.

If you're using Spotlight on Mac (`Command` + `Spacebar`) to quickly open an app, document, or photo—and it doesn't work—you may need to re-index Spotlight. Use this guide to fix Spotlight using Terminal on your Mac (plus a pro Spotlight tip). The solution works on any macOS version (tested on macOS High Sierra).

* [How to Fix Spotlight Search on macOS High Sierra](#fix)
* [Symptoms of a Corrupt Spotlight on Mac](#symptoms)
* [Why Does Spotlight Search Break?](#why)
* [Pro Spotlight Tip: Type Less](#tip)
* [References](#references)
* [Follow me](#follow-me)

![How to Fix Spotlight on Mac High Sierra](/assets/images/2018/07/How-to-fix-spotlight-on-Mac.jpg)

## How to Fix Spotlight Search on macOS High Sierra  with Terminal<a id="fix"></a>

Terminal is another way to control your Mac, and if you've never used it before, don't worry, this is a safe command to run (even if you have no idea what you're doing).

![0-Terminal](/assets/images/2018/07/0-Terminal.png#full)

1. Open the Terminal app from your "Applications" folder 

    ![Finder Applications to Utilities Folder on Mac](/assets/images/2018/07/1-Finder-applications-utilities-macos-high-sierra.png)

2. Open the "Utilities" folder and launch "Terminal"

    ![Finder Applications Utilities Folder Terminal on Mac](/assets/images/2018/07/2-Finder-applications-utilities-terminal-macos-high-sierra.png)

3. Copy and paste this command and press enter:

        sudo mdutil -E /

    
    1. The `-E` command will "Erase and rebuild index"—which is exactly what you want to do to fix the problem. `/` means to start at your hard drives root directory, which will make it re-index everything on your hard drive.


    2. Other guides might have you try to delete the Spotlight files, which I think is unnecessary, and a huge risk if you're new to the command line tools (i.e.: Terminal).
        
    > **Warning**: Do not type any command with the `rm` keyword (remove) and `-rf` options (recursive force: i.e.: no confirmation . . . goodbye files!), unless you know what you're doing. You can accidentally delete your entire hard drive, as this command is not safe!

4. Type your password, and let it run. Give your Mac 15-30 seconds to start re-indexing all your files, apps, and images.

    ![Reindex spotlight on Mac using Terminal Successful](/assets/images/2018/07/3Reindex-Mac-Spotlight-Search-Using-Terminal.png)

5. Try searching for "Safari" with Spotlight (`Command` + `Spacebar`). 

    ![Spotlight Search Working on Mac](/assets/images/2018/07/01-Spotlight-search-mac-working.png)
    
> **Note**: You may have to wait longer your entire hard drive (and all the files) to be indexed, but apps should be indexed pretty quickly.

## Symptoms of a Corrupt Spotlight on Mac <a id="symptoms"></a>

The telltale sign of a corrupt Spotlight is when you try to search for an app you use frequently using Spotlight, and it's not the first result (it might not even be in the list!).

Numerous times I'll try to open an app like TextMate, Evernote, or even Terminal, and the search results only show web pages, documents, and no apps. 

Since I use my keyboard to launch apps quickly, this is a huge decrease in my productivity. The workaround is to use the Applications folder, or Launchpad to find the app I want to use.

## Why Does Spotlight Search Break? <a id="why"></a>

Spotlight will sometimes fail due to bugs in the macOS. On the initial launch of If you're experiencing this frequently, you should submit a [bug to Apple at bugreport.apple.com](http://bugreport.apple.com). 

Explain what happened, and they will follow up with you, and the bug will get fixed, rather than never getting fixed!

I submitted a bug #31646293, "Spotlight loses index for apps that are updated from App Store," on April 15th 2017, and Apple fixed it on July 11th 2017 (duplicate of bug #24109163).

I worked at Apple in the past, and they do read your bug reports, and they **do fix** issues when they know the problem exists. 

## Pro Spotlight Tip: Type Less <a id="tip"></a>

You can change the default search result if you start typing the first few letters, and then select the option you want with the arrow keys (or the mouse).

The next time you start typing "Terminal" stop with the first three letters: "Ter". Try it:

1. Open Spotlight from the top right corner icon (`Command` + `Spacebar`)
2. Start typing "Ter" (add more letters if you don't see Terminal in the list)
3. Select Terminal

![Terminal-spotlight-retrain-ter](/assets/images/2018/07/Terminal-spotlight-retrain-ter.png)

Now you've *"re-trained"* Spotlight for showing Terminal as the first result for "Ter".

## References <a id="references"></a>
* [How to rebuild the Spotlight index on your Mac - Apple.com](https://support.apple.com/en-us/ht201716)
* [How to fix spotlight search on a Mac](https://www.amsys.co.uk/blog/how-to-fix-spotlight-search-on-a-mac/)
* [rm manual page](https://ss64.com/bash/rm.html)
* [mdutil manual page](https://ss64.com/osx/mdutil.html)

## Follow Me <a id="follow-me"></a>

Let me know if this was helpful in the comments below, or [follow me on Twitter @PaulSolt](http://twitter.com/PaulSolt)