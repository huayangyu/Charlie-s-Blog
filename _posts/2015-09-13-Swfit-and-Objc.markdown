---
layout: post
title:  Interacting with Objective-C APIS
date:   2015-09-12 23:00:10
categories: Charlie update
body-class: post-welcome
---

1.init
			let myTableView: UITableViiew = 
						UITableView(frame:CGRectZero, style: .Grouped)

			let myTableView = 
						UITableView(frame:CGRectZero, style: .Grouped)

		as for factory method 

			let color = UIColor(red: 0.5, green: 0.0, blue: 0.5, alpha: 1.0)

		Failable Initianlzation : 这部分不太懂

			init(...)

			init?(...)

			if let fileContents = 
						NSString(contentsOfFile: 
							"MyFile.txt") {

							println(fileContents)
						}

2.Accessing Properties
			
			myTextFiled.textColor =
						UIColor.darkGrayColor()
			myTextFiled.text = "Hello World"

3.Working with Methods
			
			myTableView.insertSubView(mySubview, atIndex: 2)

			myTableView.layoutIfNeeded()

4.id Compatibility
     		var myObject: AnyObject = 
     					UITableViewCell()
     		myObject = NSDate()

     		说是AnyObject比id要安全

     		myObject.characterAtIndex(5)
     		//crash , myObject doesn't respond to that method

     		let myCount = myObject.count?

     		let myChar = myObject.characterAtIndex?(5)

     		if let fifthCharacter = 
     					myObject.characterAtIndex?(5) {
     				println("found \(fifthCharacter at index 5")

     					}

     		let userDefulats = 
     				NSUserDefaults.standardUserDefaults()

     		let lastRefreshDate: AnyObject? =
     				userDefulats.objectForKey("date")

     		if let date = lastRefreshDate as? NSDate {
     				println("\(date.timeIntervalSinceReferenceDate")

     		}
     		//这个不执行、为什么

5.Working with nil
			func dueDateForProject(project:Project!) -> NSDate!

			//这里不太明白关于 implicitly unwrapped optionals

6.Extensions
			extension UIBezierPath {
				convenience
					init(triangleSideLength: CGFloat, origin: CGFloat) {
						self.init()

						let squareRoot = CGFloat(sqrt(3.0))

						let altitude = (squareRoot * triangleSideLength) / 2

						moveToPoint(origin)

						addLineToPoint(CGPoint(x: triangleSideLength, y: origin.x))

						addLineToPoint(CGPoint(x: triangleSideLength / 2, y: altitude))

						closePath()
					}
			}

			extension CGRect {
				var area: CGFloat {
					return width * height
				}
			}

			//extension里可以加入用于计算的属性,不能用来存储

			let rect = CGRect(x: 0.0, y: 0.0, width: 10.0, height; 50.0)

			let area = rect.area

			// you can also use extension to add protocol conformance to a class without subclassing it.
			// 这句话什么意思？

			// extension 还有好多东西没搞明白

7.Clousures
			Objective-C : 
				void (^completionBlock)(NSDate *, NSError *) = ^(NSDate *date, NSError *error)
							{/* ... */}

			Swift
				let completionBlock: (NSDate, NSError) -> void = {data, error in /* ... */}

			// 有个区别是 swfit 里的 Clousure 里的变量是可变的不是OC中的Copy的， 所以不用写 __block 了

8.Object Comparison
			equality (==) : compares the contents of the objects.

			identity (===) : determines whether or not the constants or variables refer to the same object instance.

			//The NSObject class only performs the identity compare, so you should implement your own isEqual: method that derived from the
			//NSObject class.

			//As part of implementing equality for your class, be sure to implement the hash property according to the rules in Object comparison 
			// in Cocoa Core Competencies.  这句话什么意思 ,怎么和hash有关了呢?

9.Swift Type Compatibility
			//不懂

10.Exposing Swift Interfaces in Objective-C
			//@objc 没做过，不懂
			@objc (Squirrel)
			class squirrel {
				@objc(initWithName:)
				init (name: String) { /* ... */ }
				@objc(hideNuts:inTree)
				func hideNuts(Int, inTree: String) {

				}
			}

11.Requiring Dynamic Dispatch
			//完全晕了

12.Objective-C Selectors
			class MyViewController: UIViewController {
				let myButton = UIButton(frame: CGRectZero)

				init(nibName nibNameOrNil: String?, bundle nibBundleOrNil: NSBundle?) {
					super.init(nibName:nibNameOrNil, bundle:nibBundleOrNil)

					myButton.addTarget(self, action: "tappedButton:", forControlEvents: .TouchUpInside)
				}

				func tappedButton(sender: UIButton!) {
					println("tapped button");
				}
			}
			//这章也看看吧，后面不是很懂
