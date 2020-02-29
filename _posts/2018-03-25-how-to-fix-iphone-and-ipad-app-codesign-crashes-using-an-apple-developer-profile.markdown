---
layout: post
title: How to Fix iPhone and iPad App codesign Crashes using an Apple Developer Profile
date: '2018-03-25 02:59:10'
tags:
- xcode
- bugs
---

Does your iPhone app run in the iPhone Simulator, but crash on start when you run it on an iPhone or iPad?

Or does the app launch from Xcode on one Mac, but it crashes on launch from another Mac?

If either of these cases are happening to you (like they did for me, and some of my students), then you probably have an issue with your developer credentials.

Most likely you're in the Apple Developer program ($99/year), or you were an active member a few years back, and that's why you're having problems.

**Why?**

There have been changes to the `codesign` process used by Xcode in recent years. 

Code signing is a final step to run your app on an iPhone. It's Xcode's way of signing off that your app is valid. You need this step because Apple only lets trusted apps run on iPhone or iPad.

## Developer Certificate and codesign Symptoms ##

1. If you had a paid developer account before iOS 8 (2014)
	2. Apple changed the process after this date, so things may require a couple new steps to fix
2. If you see `Thread 1: signal SIGABRT` when you start a brand new Xcode project on an iPhone or iPad.

## About the Issue ##

This is the second time this month that I ran into issues with Xcode 9 running an app on an iPhone. The first time was when I updated my [Artwork Evolution app for iOS 11](http://itunes.apple.com/us/app/artwork-evolution/id393135008?mt=8). 

Today one of my students was stuck with Xcode crashing the app on start. It would white screen, and there wasn't a whole lot of useful information.

We dug a little deeper and discovered that there was a "Thread 1: signal SIGABRT" message, followed by an issue about not being able to load a library using dyld (dynamic linker). All Swift modules are loaded dynamically on iOS 11.

![Xcode 9 Crash SIGABRT libswiftCore.dylib: code signing blocked](/content/images/2018/03/1-Xcode-crash-SIGABRT-dyld-library-not-loaded-libswiftCore.png)

		dyld: Library not loaded: @rpath/libswiftCore.dylib
		  Referenced from: /var/containers/Bundle/Application/9AC9EC51-7480-4E92-8C24-654EAB6A6046/Test.app/Test
		  Reason: no suitable image found.  Did find:
			/private/var/containers/Bundle/Application/9AC9EC51-7480-4E92-8C24-654EAB6A6046/Test.app/Frameworks/libswiftCore.dylib: code signing blocked mmap() of '/private/var/containers/Bundle/Application/9AC9EC51-7480-4E92-8C24-654EAB6A6046/Test.app/Frameworks/libswiftCore.dylib'
		(lldb) 

You'll notice something about: `libswiftCore.dylib: code signing blocked` which is a problem with your iPhone Developer Certificate.

Rebooting and restarting Xcode didn't fix the issue.

Instead we had to export the developer credentials and then re-import them into Xcode.

## Two Fixes ##

I believe there's two potential fixes to this issue, but it's hard to diagnose because it's hard to re-create the bug.

1. You need to change your iPhone Developer Certificate's trust levels
2. You need to export/import your Apple ID Credentials if you're seeing this issue between two or more Mac computers 

## Solution 1: Change You iPhone Developer Profile Certificate Trust Levels


1. Open the Keychain app and navigate to Certifcates

    ![Open Keychain](/content/images/2018/03/2-Keychain-Access-for-iPhone-Developers-Certificate.png)

2. Double click the "iPhone Developer: YOUR NAME (XYZ)" 
3. Expand the Trust section at the top and change from "Always Trust" to "Use System Defaults"

    ![Change Always Trust to Use System Defaults](/content/images/2018/03/3-Xcode-9-Always-Trust-Certificate-Issue.png)

4. After making the change it should look like:

![Xcode 9 Certificate Use System Defaults](/content/images/2018/03/4-Xcode9-Certificate-bug-fix.png)

4. Close the Certificate Window (it'll prompt you to authenticate to make changes)
6. Open your Xcode project and "Clean your Xcode Build Folder"
	1. `Command + Alt + Shift + K`
8. Verify your developer profile is selected 

	![Select Your Xcode Team Profile](/content/images/2018/03/5-Select-Your-Team-Profile-Xcode-9.png)

9. Run your iPhone app

## Solution 2: Export Xcode Profile Credentials From a Working Mac

If you have the iPhone app working on another Mac (might be a newer Mac). You might need to transfer your working credentials to your other Mac.

If that's the case, you'll go into Xcode preferences to export from one machine, and then import on the other machine.

Note: It would probably be a good idea to export on both machines to backup any settings (just in case, as we're going to try and remove settings from one machine).

1. Go to Xcode > Preferences > Accounts
2. In the bottom left corner click the Cog button and "Export Apple ID and Code Signing Assets..."

	![Export Apple ID and Code Signing Assets...](/content/images/2018/03/11-Export-Apple-ID-and-Code-Signing-Assets.png)

3. Find a shared location (Dropbox) and create a password (You'll want to keep these protected and backed up)

	![Save to Dropbox with a Secure Password](/content/images/2018/03/12-Export-Apple-Developer-Certificate-to-Dropbox.png)

4. On the 2nd Mac import the developer credentials using "Import Apple ID and Code Signing Assets..."

	Note: If you have issues, try removing all the Developer Accounts on the problematic Mac, and then re-import

	![Import Apple ID and Code Signing Assets...](/content/images/2018/03/13-Import-Apple-Developer-Code-Signing-Assets.png)
	
6. Clean your Xcode Build Folder
	1. `Command + Alt + Shift + K`
8. Verify your developer profile is selected
9. Run your iPhone app
10. At one of these steps you'll see a dialog to login to enable `codesign` . . . and this is where things get a little weird in Xcode 9 (buggy). If you see a dialog with the message "codesign wants to access key "access" in your keychain" you might have to type your Mac password a lot to make it go away. (there might be 10-30 dialog's sitting behind it all asking the same question ... the clue is the drop shadow might be really dark).

	![codesign wants to access key "access" in your keychain](/content/images/2018/03/14-Codesign-xcode-access.png)
	
	1. If that's the case you'll have to type the password 10-30 times ... to close all of the windows.
	2. I believe this is because there's all those fields in the Certificate displayed in Option 1, but I'm not positive.
13. After you close out of all the dialogs your app should hopefully run on your iPhone

## Fixing False Errors in Xcode for First Time iPhone Developers ##

1. If you're building your first iPhone app (with your Developer profile), Xcode might throw some errors . . . 
	2. Don't worry, just Clean (Command + Shift + K) and Run it again. Try this at least 2-3x.
2. If that doesn't work, restart Xcode 
3. If that fails, restart your Mac

Good luck and have fun building your iPhone App!

Comment below if this helped you solve your problem.

If you're still stuck, checkout the references for further debugging.

# References for Further Reading

* [Codesign wants to access key “access” in your keychain, I put in my login password but keeps asking me](https://stackoverflow.com/questions/46774005/codesign-wants-to-access-key-access-in-your-keychain-i-put-in-my-login-passwo)
* [Always Trust iPhone Developer](https://stackoverflow.com/a/30252254/276626)
* [Enterprise Development Certificate](https://stackoverflow.com/a/31672991/276626)
* [Apple's Technical Q&A QA1886](https://developer.apple.com/library/content/qa/qa1886/_index.html)
