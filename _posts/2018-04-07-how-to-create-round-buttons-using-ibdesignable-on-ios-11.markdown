---
layout: post
title: How to Create Round Buttons Using @IBDesignable on iOS 12
date: '2018-04-07 12:01:00'
tags:
- design
- ibdesignable
- ui
- xcode
- storyboard
---

![](/content/images/2017/12/header-render.jpg)

Buttons in Xcode Storyboards require a bit of work to customize, especially if you want a solid background color and an easy to edit corner radius. 

Unfortunately there isn't an easy way to change the corner radius in a Storyboard file with a system `UIButton`.

Rounded Button Solutions:

* Create the button programmatically 
* Create different art assets

In this tutorial you will learn a new approach that combines the best of both worlds (code and Storyboard files) using the `@IBDesignable` UI elements.

You can leverage this approach for other UI elements in your application to create image free, pixel-perfect rounded buttons (or dialogs and other views).

![A stock UIButton with some of the buttons you will be able to build using this tutorial](/content/images/2017/12/examples.png)

## Download the 11 Step `@IBDesignable` PDF

Get the source code and the 11-step guide for creating `@IBDesignable` UI elements for iPhone apps.

You can reference this guide quickly when you make your UI more design friendly, so that you can iterate faster.

<script async id="_ck_312962" src="https://forms.convertkit.com/312962?v=6"></script>

## 1. Create Swift Code File
Create a new Swift code file called: `RoundButton.swift`

![Swift-create-File-Xcode-9](/content/images/2017/12/Swift-create-File-Xcode-9.png)

## 2. Subclass `UIButton` and make it `@IBDesignable`

`@IBDesignable` is a special attribute that allows the Storyboard file to see our custom UI element and it will actually compile the code for the Storyboard.

Subclassing the `UIButton` allows you to use the system animations and default button behavior for free. You won't have to mimic the button fade animation in code.

```swift
import UIKit

@IBDesignable class RoundButton: UIButton {

}
```

## 3. Create the Common `init` Logic

Buttons can be created in multiple ways: either programmatically or via the drag and drop Storyboard/.xib interface files.

You will need to have common setup logic, otherwise your buttons will behave and look differently between the Storyboard file and iPhone Simulator (and if you create them programmatically).

Add the initializers, `prepareForInterfaceBuilder()` and the `sharedInit()` function:
	

```swift
@IBDesignable class RoundButton: UIButton {
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        sharedInit()
    }
    
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        sharedInit()
    }
    
    override func prepareForInterfaceBuilder() {
        sharedInit()
    }
    
    func sharedInit() {
        // Common logic goes here
    }
}
```

Three separate initializer functions are called based on what context the `RoundButton` is created in:

1. `init(frame:)` is for programmatically created buttons
2. `init?(coder:)` is for Storyboard/.xib created buttons
3. `prepareForInterfaceBuilder()` is called within the Storyboard editor itself for rendering `@IBDesignable` controls

You want to leverage code reuse to make each button look the same—no matter where or how you create it by using a single function (the less code you write the less bugs you'll have).

<script async id="_ck_312962" src="https://forms.convertkit.com/312962?v=6"></script>

## 4. Create Rounded Corners Using CALayer Properties

The `CALayer` properties have an attribute that you can change to create a `cornerRadius` on any `UIView`.

Add a helper method named `refreshCorners()` to update the corner radius:

```swift
func refreshCorners(value: CGFloat) {
    layer.cornerRadius = value
}
```

## 5. Create an `@IBInspectable` Attribute for Rounded Corners


Inside "RoundButton.swift" at the top of the RoundButton class, add an `@IBInspectable` attribute:


```swift
@IBInspectable var cornerRadius: CGFloat = 15 {
    didSet {
        refreshCorners(value: cornerRadius)
    }
}
```


`@IBInspectable` variables are exposed to the Storyboard UI, which allows you to change these properties via the "Attributes Inspector" when editing a `RoundButton`.

Set a default value of `15` for cases when the user (i.e.: developer) doesn't change the attribute.

Use the `didSet` computed propetry to update the visuals anytime the `cornerRadius` is changed in code or via the Storyboard file.

## 6. Update the Corner Radius


Make sure you add a call to `refereshCorners()` in your `sharedInit` function to keep the behavior consistent: 

```swift
func sharedInit() {
    refreshCorners(value: cornerRadius)
}
```


This step will make sure the `layer.cornerRadius` value is set to the default of 15 when the `RoundButton` is created (Otherwise you'll see differences between when you run the iPhone app and what you see in the Storyboard file).

## 7. Create a UIButton in `main.storyboard`

1. Drag a `UIButton` onto the iPhone canvas.
2. Set the Background color to blue (or any color you choose).
3. Set the text (i.e.: Tint color) to white.
4. Open the `Identity Inspector` and set the Class attribute to `RoundButton`.

    ![Corners](/content/images/2017/12/Corners.gif)

5. After you set the `UIButton`'s Class to `RoundButton`, you get a separate option to adjust the corner radius in the "Attributes Inspector".

<script async id="_ck_312962" src="https://forms.convertkit.com/312962?v=6"></script>

## 8. Reuse Apple's System UIButton Fade Animation and Behavior

Try the button on your iPhone or the iPhone Simulator.

How does it behave?

Compare it to a standard button, and look at the animation.

It's not the same ... but you can fix it to use Apple's button fade animation.

The `UIButton`'s background color property was functional, but it doesn't have the same behavior as a system button (without additional work).

You can get the behavior by using the `UIButton`'s background image, but you would need an image of every color.

Instead of creating tons of images for any possible color, you can write a little code to programmatically create a 1x1 pixel image. 

## 9. Create a Colored UIImage Programmatically

Create a function that will create a UIImage programmatically:

```swift
func createImage(color: UIColor) -> UIImage {
    UIGraphicsBeginImageContextWithOptions(CGSize(width: 1, height: 1), true, 0.0)
    color.setFill()
    UIRectFill(CGRect(x: 0, y: 0, width: 1, height: 1))
    let image = UIGraphicsGetImageFromCurrentImageContext()!
    return image
}
```

This function is a little complex if you're new to computer graphics:

1. `UIGraphicsBeginImageContextWithOptions` is called, creating a blank 1x1 pixel graphics buffer in memory (i.e.: image).
2. The `color.setFill()` sets the color for any draw operations that follow. 
3. `UIRectFill()` is a Core Graphics routine that can paint a rectangle with the set fill color.
4. The last step renders an `UIImage` from the open graphics context

    ![background-creation](/content/images/2017/12/background-creation.png)

## 10. Create an `@IBInspectable` `UIColor` Property

You can create `UIColor` properties that are `@IBInspectable` and let the user pick a color using Xcode's built-in color picker.

1. Create a function to update the color of the `UIButton`'s background image:

    ```swift
    func refreshColor(color: UIColor) {
        let image = createImage(color: color)
        setBackgroundImage(image, for: UIControlState.normal)
        clipsToBounds = true
    }
    ```

    Creating the image and setting the backround image are fairly self-explanitory, but `clipToBounds` needs to be enabled, otherwise the corners will not rounded (which is kind of the point of this tutorial).

2. Create a `@IBInspectable` variable for the background color named `backgroundImageColor` and call the `refreshColor(color:)` method:

    ```swift
    @IBInspectable var backgroundImageColor: UIColor = UIColor.init(red: 0, green: 122/255.0, blue: 255/255.0, alpha: 1) {
        didSet {
            refreshColor(color: customBGColor)
        }
    }
    ```


    The logic is similar to how the corner radius worked, except the default value is a light blue color, similar to the default Tint Color on iOS 12.

3. Make sure to add the call to `refreshColor()` to your `sharedInit()` to ensure the default color is set when you create the `RoundedButton` and run the app:

	```swift
	func sharedInit() {
	    refreshCorners(value: cornerRadius)
	    refreshColors(color: customBGColor)
	}
	```
    
    
<script async id="_ck_312962" src="https://forms.convertkit.com/312962?v=6"></script>


## 11. Preview the @IBDesignable Button in main.storyboard

1. Click on your main.storyboard file and open the Attributes Inspector on the right.
2. Change the "Background Image Color" property for your `RoundButton` to a new color:

    ![ColorPicker_New](/content/images/2017/12/ColorPicker_New.gif)


3. Tap the button and watch the fade animation:

    ![ClickAnimation](/content/images/2017/12/ClickAnimation.gif)

Awesome!

You can now drag-and-drop custom controls into your Storyboard and .xib interface files.

You can create more complex interfaces or widgets using this same process, to design any control that Apple doesn't provide.

## Try It! ##

Following a tutorial will only get you so far.

Now that you know the steps:

1. Create the round bounds again from scratch (do it again!)
2. Create a UI element for your app idea

## Custom Border Width and Colors

Wayne shared his code to customize the border width and color. Check it out:

```swift
@IBInspectable var borderWidth: CGFloat = 2 {
    didSet {
        refreshBorder(_borderWidth: borderWidth)
    }
}

func refreshBorder(_borderWidth: CGFloat) {
    layer.borderWidth = _borderWidth
}

@IBInspectable var customBorderColor: UIColor = UIColor.init (red: 0, green: 122/255, blue: 255/255, alpha: 1){
    didSet {
        refreshBorderColor(_colorBorder: customBorderColor)
    }
}

func refreshBorderColor(_colorBorder: UIColor) {
    layer.borderColor = _colorBorder.cgColor
}

func sharedInit() {
    refreshCR(_value: cornerRadius)
    refreshColor(_color: customBGColor)
    refreshBorderColor(_colorBorder: customBorderColor)
    refreshBorder(_borderWidth: borderWidth)
    self.tintColor = UIColor.white
}
```

In the process of creating an @IBDesignable element you will learn how to debug problems and deal with issues. You'll learn way more by doing, instead of following a tutorial word for word.

1. Let us know what you create, email Paul at [Paul@SuperEasyApps.com](mailto:Paul@SuperEasyApps.com) with the subject "[IBDesignable] Round Buttons Idea <your idea here>".

2. Start the free 4-part course and make your first iPhone app: [SuperEasyApps.com](http://supereasyapps.com/?utm_source=blog&utm_medium=social&utm_campaign=ibdesignable_round_buttons).


## Download the 11 Step `@IBDesignable` PDF

Get the source code and the 11-step guide for creating `@IBDesignable` UI elements for iPhone apps.

You can reference this guide quickly when you make your UI more design friendly, so that you can iterate faster.

<script async id="_ck_312962" src="https://forms.convertkit.com/312962?v=6"></script>