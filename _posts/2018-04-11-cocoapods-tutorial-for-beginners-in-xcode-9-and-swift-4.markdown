---
layout: post
title: CocoaPods Tutorial for Beginners in Xcode 9 and Swift 4
date: '2018-04-11 15:55:05'
tags:
- cocoapods
- xcode
- tutorial
- beginners
- getting-started
---

Follow along with a CocoaPods tutorial that will show you how to setup Cocoapods for the first time using Xcode 9 and Swift 4.

What are CocoaPods?

![Cocoapods-Logo](/assets/images/2018/04/Cocoapods-Logo.png)

Cocoapods is a system that helps you create the Xcode project (Workspace) that can include other open source Swift and Objective-C projects (Networking, Animation, Auto Layout, etc.). 

Traditionally there has been a lot of setup to use open source projects, and to keep them up to date. Which is why [Cocoapods](https://cocoapods.org), [Carthage](https://github.com/Carthage/Carthage), and the [Swift Package Manager](https://swift.org/package-manager/) exist. These three tools will help you download source code from public GitHub projects, and import them into your project to build your apps.

In this tutorial we're going to focus on just getting started with Cocoapods. You're going to need to be a little familar with using Terminal. If you don't know how to use Terminal, see this [Terminal tutorial](https://www.youtube.com/watch?v=IGmfU6QU5dI).

Cocoapods helps you manage dependencies (open source code) that you want to leverage in your app to do something (make networking/HTTP requests easier, or animation (Facebook POP). It'll automatically change your Xcode project into a Workspace that includes any of the open source projects you request in your "Podfile".

## Alternatives? ##

1. You can manually setup a project by dragging in [Frameworks](https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/BPFrameworks/Frameworks.html), [static libraries](https://www.raywenderlich.com/41377/creating-a-static-library-in-ios-tutorial) (libXML.a), [dynamic libraries](https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/DynamicLibraries/100-Articles/OverviewOfDynamicLibraries.html) (swiftCore.dylib) ... and then setting up all the compiler paths to the right header files (.h) ... which can be a real pain to get right, and it's very error prone. See a tutorial on how to make a [Reusable Swift Framework](https://medium.com/flawless-app-stories/getting-started-with-reusable-frameworks-for-ios-development-f00d74827d11).
2. You can use [Carthage](https://github.com/Carthage/Carthage) to pull down your dependencies, but you'll manually include the build products into your Xcode project.
3. You can use the [Swift Package Manager](https://swift.org/package-manager/) (Xcode 9.3) for Swift Mac/Linux projects (iOS not officially supported ... yet)

Let's learn how to use CocoaPods for the first time and use it to make an [API request on Github](https://developer.github.com/v3/).

## CocoaPods Sample Project ##

<script async id="_ck_373521" src="https://forms.convertkit.com/373521?v=7"></script>

## Install CocoaPods ##

	$ gem install cocoapods

If you're using the default version of Ruby on macOS, you'll need to use `sudo` for the command. 

Otherwise, when you run the above command, it'll fail with something like this error: 

	ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.

To install CocoaPods, use `sudo` in front of the command, and then type your login password to confirm. Why? This elevates the privileges of the install command, so that it can put files in the protected folder mentioned in the `/Library/Ruby/Gems` path. 

	$ sudo gem install cocoapods


## Using Ruby to Install Cocoapods ##

We're using Ruby's `gem` tool to install (or update CocoaPods). Both Sierra and High Sierra should work without any issues, here's how to check your ruby version: 

	$ ruby --version
	ruby 2.3.3p222 (2016-11-21 revision 56859) [universal.x86_64-darwin17]

## Start Using CocoaPods with AlamoFire ##

AlamoFire is a helper for HTTP and web requests in Swift. 

<https://github.com/Alamofire/Alamofire> 

1. You need an Xcode project to start. Create a project (or use an existing project)
2. Close your Xcode project, as Cocoapods is going to make project changes.
3. Open Terminal to the location of your Xcode project folder 
4. Type `pod init` in Terminal 

		$ pod init
		
5. Open the `Podfile` in TextEdit (I prefer [TextMate](https://macromates.com))		 

		$ open Podfile

	Or with TextMate installed:

		$ mate Podfile

	It'll look something like this: 

		# Uncomment the next line to define a global platform for your project
		# platform :ios, '9.0'
		
		target 'GithubProfile' do
		  # Comment the next line if you're not using Swift and don't want to use dynamic frameworks
		  use_frameworks!
		
		  # Pods for GithubProfile
		
		end

	The lines started with `#` are comments and since we're using Swift, you'll need `use_frameworks!` 

6. Open the Podfile and change it so that it looks like:

		platform :ios, '10.3'
		use_frameworks!
		
		target 'GithubProfile' do

		end


7. Add AlamoFire's current version (use version 4.7 with Xcode 9.3) by adding the line `pod 'Alamofire', '~> 4.7'` inside the `target area`, see below: 


		platform :ios, '10.3'
		use_frameworks!
		
		target 'GithubProfile' do		
		  pod 'Alamofire', '~> 4.7'
		end

8. Run CocoaPods install (this may take time if it's your first CocoaPods install . . . )

		$ pod install

9. Depending on how old your CocoaPod install is, you might need to try the `update` command to get the version numbers to work. 

	If you see this type of error, checkout the troubleshooting tips below.

		[!] CocoaPods could not find compatible versions for pod "Alamofire":
		  In Podfile:
		    Alamofire (~> 4.7)
		
		None of your spec sources contain a spec satisfying the dependency: `Alamofire (~> 4.7)`.
		
		You have either:
		 * out-of-date source repos which you can update with `pod repo update` or with `pod install --repo-update`.
		 * mistyped the name or version.
		 * not added the source repo that hosts the Podspec to your Podfile.
		
		Note: as of CocoaPods 1.0, `pod repo update` does not happen on `pod install` by default.

## Troubleshoot Your CocoaPods

Sometimes things fail, and you need to try the commands again. I find that either clearing the cache, making sure the Podfile changes are saved, and then doing an update (or an install command) fixes the problems. 

Clear cached files to start over 

	$ pod cache clear --all

Update Cocoapods (or try to do `pod install` again)

	$ pod update


## Cocoapods Sample Project

Follow along with a GitHub API demo using Cocoapods. Download the sample code now, and you can follow the tutorial below.

<script async id="_ck_373521" src="https://forms.convertkit.com/373521?v=7"></script>

## Using Alamofire ##

1. Open your Workspace file that was generated `GithubProfile.xcworkspace` 

2. Add the statement at the top of the "ViewController.swift" file under `import UIKit`

````swift
import Alamofire
````

3. Create a new function that will use one of the [Alamofire request APIs](https://github.com/Alamofire/Alamofire/blob/master/Documentation/Usage.md)

````swift
    func searchForUserAlamo(username: String) {

        Alamofire.request(URL(string: "https://api.github.com/users/\(username)")!)
            .validate()
            .response { (response) in

            print("Request: \(response.request)")
            print("Response: \(response.response)")
            print("Error: \(response.error)")

            if let data = response.data {
                do {
                    let json = try JSONSerialization.jsonObject(with: data, options: [])
                    print(json)

                } catch {
                    print("Error: ", error)
                }

            }
        }
    }
````

4. Call the function with a button press, or in your `viewDidLoad()` method.

````swift
    override func viewDidLoad() {
        super.viewDidLoad()

        searchForUserAlamo(username: "PaulSolt")
    }
````

Using the new Swift 4 support for JSON parsing, you can take the example a step further ... mapping the Github .json data to a structure in Swift.

````swift
import UIKit

struct GithubProfile: Codable {
    let name: String?
    let location: String?
    let avatarUrl: URL?

    enum CodingKeys: String, CodingKey {
        case name
        case location
        case avatarUrl = "avatar_url"
    }
}
````


And in your `if let data = ...` you can then parse the GitHub JSON.

````swift
// Try to decode a GithubProfile struct
let decoder = JSONDecoder()
let profile = try decoder.decode(GithubProfile.self, from: data)
````

One more step would be to actually download and present an image using this code:

````swift
func downloadProfilePhoto(url: URL) {

    URLSession.shared.dataTask(with: url) { (data, response, error) in
        guard let data = data else {
            print("Invalid image request data: \(String(describing: error))")
            return
        }

        let image = UIImage.init(data: data)
        print(String(describing: image))
        // Display in UI
        DispatchQueue.main.async {
            self.imageView.image = image
        }

    }.resume()  // MUST call resume() to start the URL request
}
````

# Download the Sample Project #

You can see how this works in action between Alamofire and the native URLSession from Apple. (Make sure you have Cocoapods setup!)

<script async id="_ck_373521" src="https://forms.convertkit.com/373521?v=7"></script>

## Next Steps ##

There's a lot that you can do with Alamofire, and any open source project that supports Cocoapods.

Now that you have a base level understanding, dig into the documentation for Alamofire, or try a tutorial to take it to the next step. On the [Alamofire Readme](https://github.com/Alamofire/Alamofire) they list out the features that it supports.

If you want to try another fun animation framework, checkout [Facebook's POP framework](https://github.com/facebook/pop) that uses Cocoapods.


## Resources ##

* [Getting Started with CocoaPods](https://guides.cocoapods.org/using/getting-started.html)
* [Alamofire](https://github.com/Alamofire/Alamofire)
* Read this: [Alamofire Usage](https://github.com/Alamofire/Alamofire/blob/master/Documentation/Usage.md)
* Follow this [Alamofire tutorial](https://www.raywenderlich.com/147086/alamofire-tutorial-getting-started-2)
* Checkout another Cocoapod for animations: [Pop](https://github.com/facebook/pop) 
* [Terminal tutorial](https://www.youtube.com/watch?v=IGmfU6QU5dI)



