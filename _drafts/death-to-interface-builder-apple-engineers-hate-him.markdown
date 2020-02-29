---
layout: post
title: 'The end of Interface Builder: Find out what Apple doesn''t want you to know!'
---


# IBEnemy 

One of the easiest ways to tell the difference between a Senior iOS developer and the rest of us plebians is their ability to understand and debug issues with autolayout. If your goal is to become a true iOS master, understanding autolayout is essential. What you may not be ready for, however, is getting rid of interface builder completely.

![STOP-INTERFACE-BUILDER](/content/images/2018/01/STOP-INTERFACE-BUILDER.png)
# A Quick History of Interface Builder

<p> First, let's begin by celebrating the Interface Builder's 30th birthday. That's right, it came out in 1988. Interface builder is older than I am. When it was created, the USSR was still a thing. The Berlin wall still stood. It's OLD. </p>
<p> While it's certainly become fancy and snazzy lately, it hasn't improved in it's usefulness for larger teams - and allow me to explain why.</p>

# Interface Builder vs Programmatically Built Views

While can easily guide you into the world of iOS development, they introduce a lot of problems when you have more than one developer touching them. If you've ever encountered git merge conflicts, you may know what I'm talking about. This is due to the ugly underlying structure of a storyboard or .xib file - it's just a gigantic XML document. Every change you make to that fancy GUI in your storyboard gets saved as a couple of properties in those XML sheets. 

Do yourself a favor by right clicking on one of your storyboards to see what it looks like as source code.

![Screen-Shot-2018-01-19-at-11.37.34-AM](/content/images/2018/01/Screen-Shot-2018-01-19-at-11.37.34-AM.png)


![Screen-Shot-2018-01-19-at-11.37.43-AM](/content/images/2018/01/Screen-Shot-2018-01-19-at-11.37.43-AM.png)

*Yuck.*

I'm going to guess that you don't want to debug that mess when you run into a merge conflict.




# Programmatic Design
The answer, of course, is to draw your user interface through code. It sounds intimidating to newer developers, but it's actually pretty easy. Let's start by adding a view to a ViewController. For this example, I've created a completely blank Single View App.

    import UIKit

    class ViewController: UIViewController {
    
        override func viewDidAppear(_ animated: Bool) {
            super.viewDidAppear(true)
        
            let exampleView = UIView.init(frame: CGRect.init(x: 0, y: 0, width: 100, height: 100))
            
            exampleView.backgroundColor = UIColor.red

            
            self.view.addSubview(exampleView)
        }

    }

*Protip: Make sure you put this code in your viewDidAppear method instead of your viewDidLoad. If you want to know why, we'll explain it in a later post.*

Easy, right? All you need to do is instantiate a UIView, initialize it with a CGRect, and add it to the subview of your current view and *voila.* (I set the background color of the view to be red solely for illustrative purposes) Here's our code running on an iPhone SE:

![Screen-Shot-2018-01-19-at-4.52.39-PM](/content/images/2018/01/Screen-Shot-2018-01-19-at-4.52.39-PM.png)

Something you might have noticed is that the coordinate systems for computer graphics are a bit different for what you might be used to if you've come from a mathematics background.

While you may have been used to X,Y coordinates having the position 0,0 be in the bottom left like this:

![CoordinateSystems](/content/images/2018/01/CoordinateSystems.png)

In iOS, the point 0,0 is in the top left, like this:

![CoordinateSystem2](/content/images/2018/01/CoordinateSystem2.png)

Adding views to a ViewController is great, but the thing everyone struggles with is AutoLayout. While Interface builder is a much older product, AutoLayout was actually introduced in 2012 alongside the iPad and the iPhone 5. Before then, every Apple device had the same aspect ratio, meaning every view rendered on the screen could be given exact sizes and positions, like we did above.

It quickly becomes clear why pixel perfect graphics are bad when we take our code from earlier and run on on something like the new iPhone X:

![Screen-Shot-2018-01-19-at-4.56.30-PM](/content/images/2018/01/Screen-Shot-2018-01-19-at-4.56.30-PM.png)

*Yikes.* I hope this illustrates my point.

So faced with this issue, Apple developed AutoLayout. If you've worked with web development, guess what - AutoLayout has about as much in common with CSS as Java does with JavaScript. 

This leads us into the most misunderstood and horrifying concept to new devs: The constraint. Constraints give us the ability to draw our views through relationships rather than pixel perfect values. Normally, you'd draw a constraint in Interface Builder like this:

![IBConstraints](/content/images/2018/01/IBConstraints.gif)

While programmatically, you'd get the same functionality by modifying our original code to look like this:

    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(true)
        
        let exampleView = UIView.init()
        exampleView.backgroundColor = UIColor.red
        self.view.addSubview(exampleView)
      exampleView.translatesAutoresizingMaskIntoConstraints = false

        let leadingConstraint = NSLayoutConstraint.init(item: exampleView, attribute: .leading, relatedBy: .equal, toItem: self.view, attribute: .leadingMargin, multiplier: 1.0, constant: 0.0)
        
        let trailingConstraint = NSLayoutConstraint.init(item: exampleView, attribute: .trailing, relatedBy: .equal, toItem: self.view, attribute: .trailingMargin, multiplier: 1.0, constant: 0.0)
        
        let bottomConstraint = NSLayoutConstraint.init(item: exampleView, attribute: .bottom, relatedBy: .equal, toItem: self.view, attribute: .bottomMargin, multiplier: 1.0, constant: 0.0)
        
        let topConstraint = NSLayoutConstraint.init(item: exampleView, attribute: .top, relatedBy: .equal, toItem: self.view, attribute: .topMargin, multiplier: 1.0, constant: 0.0)
        
        self.view.addConstraints([leadingConstraint, trailingConstraint, bottomConstraint, topConstraint])
    }

"But Luke!" 
You may be saying. "That's a lot of code! I liked when things were in the storyboard, all simple and easy. This is a lot to remember!" 
Well, yes. You're right. Its scary, but now Apple has given us an even better way to do things, called LayoutAnchors.


TODO:
Finish explaining a programmatic constraint
Talk about the anatomy of a constraint (constraint formula, etc)
Show some really cool modularity with programmatic views & global constants for object sizes, colors, and fonts
Show a really cool animation





reference:
https://www.youtube.com/watch?v=g6yz5oX5iWc
https://www.youtube.com/watch?v=DmpoiN-SVds
http://kean.github.io/post/creating_views?utm_campaign=Revue%20newsletter&utm_medium=Newsletter&utm_source=Swiftly%20Curated
