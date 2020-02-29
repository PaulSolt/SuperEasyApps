---
layout: post
title: Buggy Render
---

# Buggy render, code blocks within a list cause the entire list to take up more width

## 10. Create an `@IBInspectable` `UIColor` Property

You can create `UIColor` properties that are @IBInspectable and let the user pick a color using Xcode's built-in color picker.

1. Create a function to update the color of the UIButton's background image:

    ```swift
    func refreshColor(color: UIColor) {
        let image = createImage(color: color)
        setBackgroundImage(image, for: UIControlState.normal)
        clipsToBounds = true
    }
    ```

    Creating the image and setting the backround image are fairly self-explanitory, but clipToBounds needs to be enabled, otherwise the corners will not rounded (which is kind of the point of this tutorial).

2. Create a `@IBInspectable` variable for the background color named `backgroundImageColor` and call the `refreshColor(color:)` method:

    ```swift
    @IBInspectable var backgroundImageColor: UIColor = UIColor.init(red: 0, green: 122/255.0, blue: 255/255.0, alpha: 1) {
        didSet {
            refreshColor(color: customBGColor)
        }
    }
    ```


    The logic is similar to how the corner radius worked, except the default value is a light blue color, similar to the default `Tint` Color on iOS 11.

3. Make sure to add the call to `refreshColor()` to your `sharedInit()` to ensure the default color is set when you create the `RoundedButton` and run the app:


## NOT BUGGY

## 10. Create an `@IBInspectable` `UIColor` Property

You can create `UIColor` properties that are @IBInspectable and let the user pick a color using Xcode's built-in color picker.

1. Create a function to update the color of the UIButton's background image:

    Creating the image and setting the backround image are fairly self-explanitory, but clipToBounds needs to be enabled, otherwise the corners will not rounded (which is kind of the point of this tutorial).


2. Create a `@IBInspectable` variable for the background color named `backgroundImageColor` and call the `refreshColor(color:)` method:

    The logic is similar to how the corner radius worked, except the default value is a light blue color, similar to the default `Tint` Color on iOS 11.

3. Make sure to add the call to `refreshColor()` to your `sharedInit()` to ensure the default color is set when you create the `RoundedButton` and run the app: