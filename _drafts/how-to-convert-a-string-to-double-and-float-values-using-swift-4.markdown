---
layout: post
title: How to Convert a String to Double and Float type using Swift 4
---

In Swift 4 you get native String support for working with different numeric types (Float, Double, and Int). But that's not the end of the story, you may need to use the NumberFormatter (NSNumberFormatter) class to convert formatted numbers (1,000,000) or currency ($3.50) in your Swift code.

In this `String` to `Double` Guide, you'll learn how to convert different types of `String` values and how to handle edge cases. Plus you'll learn about a word of caution when converting to `NSString` to use the `doubleValue` property.

Grab the **String to Double Cheatsheet** and **Swift Playground** mentioned below in the toolkit for a quick reference that you can use as you work on your apps. 

## Convert Swift `String` to `Double` ##

Use `Double`, `Float`, `CGFloat` to convert floating-point values (real numbers).

````swift
let lessPrecisePI = Float("3.14")
let morePrecisePI = Double("3.1415926536")
let width = CGFloat(Double("200.0")!)
````

## Convert Swift `String` to `Int` ##

Use `Int` and the variants like `Int32`, `UInt64`, etc. to convert integer values.

````swift
let wholeNumber = Int("27")
let smallInt = Int16("34")
let largeInt = Int64("39384")
````

But that's not everything you need to know, because this conversion process can fail, and that gives you an optional `Double` (i.e. `Double?`), optional `Float` (i.e. `Float?`), or optional `Int` (i.e. `Int?`).

How do you use the value if it's wrapped in an optional type?

## Get the String Conversion Toolkit ##

Not everyone learns the same way, get the String Conversion Toolkit so that you can follow along with this guide.

1. Print the <script src="//static.leadpages.net/leadboxes/current/embed.js" async defer></script> <a href="" data-leadbox-popup="TA3AbeLkkGqD3WQY6ciTKU" data-leadbox-domain="iphonedev.lpages.co">String to Double Cheatsheet</a> for quick reference
2. Explore the code in the <script src="//static.leadpages.net/leadboxes/current/embed.js" async defer></script> <a href="" data-leadbox-popup="TA3AbeLkkGqD3WQY6ciTKU" data-leadbox-domain="iphonedev.lpages.co">Swift Playground</a>  (Swift 4)
3. Watch an easy to follow video describing how to use NumberFormatter

<script async id="_ck_366864" src="https://forms.convertkit.com/366864?v=7"></script>

## Optionals: Failure Is an Option ##

These `String` conversions can fail, because you're using a [failable initializer](https://developer.apple.com/swift/blog/?id=17) for the `Double`, `Float`, or `Int` types.

Why?

If the number is not valid, the conversion from `String` to `Double` isn't possible. For example, trying to convert from "alphabet" to a `Double` doesn't make sense.

````swift
let invalidNumber = Double("alphabet") // nil
````

There's no good number representation for a word like "alphabet", and the result becomes `nil`, which means that it's not a number.

To use the converted numbers you'll need to unwrap them—I recommend using the `if let` syntax for user input from a `UITextField` (or you can use the `guard`).

````swift
if let cost = Double(textField.text!) {
    print("The item is valued at: \(cost)")
} else {
    print("Not a valid number: \(textField.text!)")
}
````

You will need to unwrap the optional to get the value. The `if let` syntax above makes it safe to use `cost` if it’s a valid number, otherwise you can handle the invalid case in the else expression (i.e.: If the user typed “alphabet” the conversion would fail and print the message "Not a valid number: alphabet").

## When Formatted Currency and Formatted Numbers Fail ##

BUT, the same thing can happen if you're trying to convert currency numbers ($3.49), or even formatted numbers with grouping separators (4,300.99). And that's because the initializers will not use locale information.

````swift
let failedCurrency = Double("$3.49") // nil
let failedFormattedNumber = Double("4,300.99") // nil
````

If you need to convert currency or formatted number `String`'s read below (and if you want to convert a number to a currency String read [How to use NumberFormatter in Swift](https://supereasyapps.com/blog/2016/2/8/how-to-use-nsnumberformatter-in-swift-to-make-currency-numbers-easy-to-read).

## What Are You Trying to Do? ##

Depending on the reason that you need convert between `String` and `Double` will change how I would recommend moving forward.

1. Are you getting user input from a UITextField (user input) or is it data from a database?
2. Are you working with currencies?
3. Are the numbers formatted or unformatted?
4. Is your app a simple test app, or is it an app you plan to publish?
5. Do you need to support different localizations? (different countries write numbers differently!)

## Download the Number Converter Playground 

<script async id="_ck_366864" src="https://forms.convertkit.com/366864?v=7"></script>

## Convert `Double`, `Float`, or `Int` to `String` ##

You can do the reverse conversion from a `Double` to a `String` by using one of the many `String` initializers. (These methods don't fail!)
````swift
let costString = String(9.99)
let ageString = String(18)
````

As long as the number isn’t optional the resulting value will be a `String` type, not a `String?` type.

### String Interpolation ###

[String interpolation](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/StringsAndCharacters.html) is another method to convert numbers to String.

````swift
let yearsAgo: Int = 10
let outputString = "I had \(3) pairs of running shoes \(yearsAgo) years ago."
````

## Converting a Formatted Decimal Number `String` ##

Using the `Double` initializer is not going to work when you need to convert numbers from different counties. The initializer is not locale aware, and differences in how numbers are formatted in other languages is going to make it fail.

For example the number `9,999.99` (English USA) would be written as:

* Germany: `9.999,99`
* France: `9 999,99`

If you need to work with different locales you have two options:

1. Use `NumberFormatter` with your user's current local, or a [specific iOS locale identifier for another country.](https://gist.github.com/jacobbubu/1836273). The `NumberFormatter` is the most robust and can handle different locale's grouping separators for the thousands separators. 

	````swift
	let formatter = NumberFormatter()
	formatter.locale = Locale.current // USA: Locale(identifier: "en_US")
	formatter.numberStyle = .decimal 
	let number = formatter.number(from: "9,999.99")

	let frenchLocale = Locale(identifier: "fr_FR")
	let germanLocale = Locale(identifier: "de_DE")
	
	formatter.locale = frenchLocale
	let numberFrance2 = formatter.number(from: "9 999,99")
	
	formatter.locale = germanLocale
	let numberGerman2 = formatter.number(from: "9.999,99")
	````

All of the formatted numbers will be of type `NSNumber`, which has a doubleValue property.

2. Use `NSDecimalNumber` for accurate numbers. Your currency data should be stored as a `NSDecimalNumber` (not a Double or a Float). I only show the simple Double or Float examples because they are easier to start using.

	````swift
	let usLocale = Locale(identifier: "en_US")
	let frenchLocale = Locale(identifier: "fr_FR")
	let germanLocale = Locale(identifier: "de_DE")
	
	// Convert decimal numbers (cannot have grouping separators!)
	let numberUSA = NSDecimalNumber(string: "1000.0", locale: usLocale)
	let numberFrance = NSDecimalNumber(string: "9999,99", locale: frenchLocale)
	let numberGermany = NSDecimalNumber(string: "9999,99", locale: germanLocale)
	````

The problem with `Double` is that it's not 100% accurate. It loses precision for decimal values that exceed it's maximum value, and it starts to round your numbers. When it comes to money you don't want to start losing fractions of a dollar in your application.

## Converting a Currency `String` ##

If you need to convert a user `String` you should store all your numbers as decimal numbers. a numeric currency you need to use `NSDecimalNumber`.

Use `NumberFormatter` with the currency style to convert formatted currency `String`'s

````swift
let usLocale = Locale(identifier: "en_US")
let frenchLocale = Locale(identifier: "fr_FR")
let germanLocale = Locale(identifier: "de_DE")
let englishUKLocale = Locale(identifier: "en_GB") // United Kingdom
formatter.numberStyle = .currency

formatter.locale = usLocale
let usCurrency = formatter.number(from: "$9,999.99")

formatter.locale = frenchLocale
let frenchCurrency = formatter.number(from: "9999,99€")
// Note: "9 999,99€" fails with grouping separator
// Note: "9999,99 €" fails with a space before the €

formatter.locale = germanLocale
let germanCurrency = formatter.number(from: "9999,99€")
// Note: "9.999,99€" fails with grouping separator

formatter.locale = englishUKLocale
let englishUKCurrency = formatter.number(from: "£9,999.99")
````

## Warning About `NSString` ##

You may find code that uses the `NSString` conversion to get access to a `doubleValue` property. I don't recommend using this approach. 

````swift
let cost = ("9.99" as NSString).doubleValue  // not recommended
````

BUT, you can have problems if you use this code, since the following two lines will return the same result:


````swift
let cost1 = ("abc" as NSString).doubleValue  // invalid returns 0, not an optional. (not recommended)
let cost2 = ("0.00" as NSString).doubleValue // also returns 0 
````

It's a problem because both lines of code result in 0, but only one of the lines was actually 0, while the other was an error. A failure to parse a number using NSString results in 0. 

This error mode is not safe and will cause logic errors in your app! Use `NumberFormatter` instead.

## Watch the String to Number Conversion Video ##

<script async id="_ck_366864" src="https://forms.convertkit.com/366864?v=7"></script>

## Questions or Comments? ##

If you have a question, leave a comment down below. 

And if you need to see how this code works in action, get the toolkit above so that you can watch me walk through the process of converting numbers.