# WWDC 2017 Notes

## Tuesday June 6, 2017

### Session 201 - What's New in Cocoa Touch

#### Productivity

##### Drag and Drop
Introduging ```UIDragInteraction``` - subclass off ```UIInteraction```

Built-in support for TableView, CollectionView, TextView, TextField, WebView

Multiple sessions this week

##### File Management
```UIDocumentBrowserViewController```

Other applications may access your files

Use ```NSFileCoordinator``` or subclass ```UIDocument``` to avoid file access conflicts

#### UI Refinements

##### Large Navigation Title
Large title with built in Search Bar

```prefersLargeTitle``` property on ```UINavigationBar```

Generally, first view on navigation stack should use large title, subsequent views should use traditional titles

View is part of the navigation bar not the content view, changes size as TableView or CollectionView scrolls

New property on ```safeAreaInsets``` property on ```UIView```

This property has a ```.top``` and ```.bottom``` value

New property on ```UIScrollView```, ```adjustedContentInset```

TableViews have unified swipe actions

Check out ```UIContextualAction``` class, seems very nice for TableView editing

New ```separatorInsetReference``` property on ```UITableView``` allows more consistent placement of cell separators

Check out Design Studio Shorts session

#### API Enhancements

##### Swift 4 and Foundation
New API for archiving Swift types like Enum and Stuct

New KeyPath type

Updates to KVO with KeyPaths

Block-based KVO

##### Deferring System Gestures

- Notification Center - iOS 5

- Control Center - iOS 7

iOS 11 provides override method that returns ```UIRectEdge``` objects you want to protect (aka defer the system gesture)

##### Auto Layout and ScrollView
Adding ```contentLayoutGuide``` and ```frameLayoutGuide``` to ```UIScrollView```

##### Dynamic Type
New class ```UIFontMetrics``` that lets you create standard size with a custom font then Dynamic Type system can scale it like a system font

Auto Layout has a new ```constraintEqualToSystemSpacing``` method that takes two anchors and tries to work out a good fit based on Dynamic Type changes

_NOTE: A lot of Auto Layout code was shown with no storyboards...do these two prefer programatic?_

##### Password AutoFill
System detects User / Password UI fields and presents a key that launches your iCloud Keychain stored passwords

Add an entitlement to your app then a few lines of JSON

Entire session on Password AutoFill

##### Asset Catalogs
Colors and icons can be added to Asset Catalogs

App thinning for icons - adopted by default in iOS 11 new projects

PDF-backed images

Tab bar images can re-size with accessibility settings (or a future use case?)

##### ProMotion
Can ask ```UIScreen``` for ```maximumFramesPerSecond```

Key as always is to optimize drawing code using Instruments

#### Summary
##### What's new in CocoaTouch?  Not all that much.  Some solid hardening and minor feature additions.

### Session 203 - Introducing Drag and Drop

#### Goals
- Be responsive
- Secure, more so than pasteboard
- A great multi-touch experience

#### Demo
You can drag links into Safari as a tab

Seems like an impressive implementation but will more casual users want to use this workflow?

_NOTE: iOS 11 icons are looking flatter and more minimal than ever, new App Store icon is like empty_

#### Phases of a Drag Session
- Lift
- Drag
- Set Down
- Data Transfer

#### Drag API
UIDragInteraction has a delegate similar to gesture recognizers

UIDragItem is the model object

You can enable a drop using ```UIPasteConfiguration``` but ```UIDropInteraction``` is the more robust API that has a delegate that returns an intention (not an Android Intent), it can say no thanks or call ```performDrop```

#### API RoadMap
Source application > middle ground where both may have access (plus the OS?) > Destination application

UIKit manages timeline and lifecycle of a drag and drop session

High level flow is:
- Get items to drop
- Get a drop proposal
- Perform the drop

NSItem provider only deals in Objects, so String should be cast to NSString

UIDropOperation has enumerated values of .cancel, copy, .move, .forbidden

NOTE: Look for a Ray Wenderlich or NSHipster tutorial on this.  It's a fairly involved API.  Get the sample code and mess around with it.

Only one drag interation but could be multiple drop interactions as the drag is hovering over drop target views. There are some cool opportunities for creative UX here as users drag over different types views.

SpringLoading is a thing, something happens when a drag hovers over a spring loaded view?

This is a substantial API with powerful delegates on the level of ```UITableView``` or ```UICollectionView```

#### Demo
Demo app shows dragging photos from Photos to pin board app, you can drag around from within that app, cool use cases here

Use .copy for between applications and .move within the same app

Interesting that some of the delegates take a position of type ```CGPoint```, doesn't seem the most Auto Layout friendly?

#### Next Steps
Exlpre the system

Start simple by adopting drop target

Try the drag source delegates

Spring load a few controls

Refine and iterate for your use case

#### Summary
##### This is a very powerful new set of features. I don't think they would have invested all this time in designing this system if it didn't have a lot of potential. Will dig deeper in future sessions and after visiting the labs.

### Session 402 - What's New in Swift
:construction:

### Session 703 - Introducing Core ML
:construction:

### Session 704 - Creating Immersive Apps with Core Motion
DeviceMotion, a powerful API from watchOS is now available for iPhone 7 and iPhone 7 Plus with iOS 11

Go back and look at 2016 SceneKit demo, get this Badger game

To use DeviceMotion, you create a ```CMMotionManager``` object and call ```startDeviceMotionUpdates()``` with the appropriate reference frame

### Session 602 - Introducing ARKit: Augmented Reality for iOS
Augmented Reality is creating the illusion that virtual objects appear in the physical world

Sneak Peaks at WithIn - Storytelling with AR, Ikea - Virtual furniture shopping, PokemonGo - Better AR UX

ARKit is supported on A9 and up (iPhone 6S and iPhone 6S Plus)

Framework provides tracking, scene understanding, and rendering to simplify the developer experience

There are ARViews for SpriteKit and SceneKit

Unity and Unreal are supporting full set of features from ARKit

#### Getting Started

ARKit calls AVFoundation and CoreMotion

```ARSessionConfiguration``` lets you create an ```ARSession```, then run it

```ARSession``` produces ```ARFrame```s, you can inspect the ```currentFrame``` property or sign up as the delegate

```ARFrame```uses ```ARAnchor```

#### Tracking
World Tracking gives you information about position, orientation, scale, physical distance movement - all relative to the starting point of your ```ARSession```

```ARCamera``` is the virtual camera for the 3D scene (not the device camera)

#### Demo
They show how to make a simple hello world ARKit app

SceneKit APIs work very nicely with ARKit

You can add a gesture recognizer to the base app template to do some really cool things like putting a snapshot view on a plane

#### More on Tracking
The framework gives you a ```cameraDidChangeTrackingState``` delegate method to let you know when the user is facing a white wall or bad lighting conditions

There are also delegate methods to inform you when tracking was interupted or ended

#### Scene Understanding
First step is plane detection, is there a surface available?

Plane detection runs over multiple frames to build full understanding of the world and provide ```ARPlanAnchor```s

Hit-testing provides an array of hit-test results in the order of nearest to the camera first

Light Estimation lets you understand relative brightness of the world so you can apply the right lighting to your augmentation

#### Demo
Debug mode shows you plane detection in real time, pretty impressive

Real world scaling is enabled by real world tracking and the model itself being created using real world coordinates

The ARKitExample demo app is one of the most insane things I have ever seen

There is an ```ARSCNViewDelegate``` that provides more seamless integration with SceneKit

You also get an ```ARSKView``` which maps ```SKNodes``` to ```ARAnchors```

Sprites are treated like billboards in ARKit, meaning they always face the camera

#### Summary
##### ARKit looks fucking amazing! This could be a serious game changer. The integration with SpriteKit and SceneKit will be rewarding for the small community of developers who have spent time learning these frameworks. I am curious what the interaction with AR will look like over time. It may end up as more of a watchOS experience where you experience cool easter eggs in AR over shorter durations. I can't see myself looking at the world through the lense of my phone screen for minutes or hours on end as you would with a traditional app or game. That said, this is some epic tech.

## Open Questions
1. WebViews support drag and drop by default , which ones?  UIWebView? WKWebView? SafariVC?
2. Which hardware supports iOS 11 productivity?
