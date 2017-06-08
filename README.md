# WWDC 2017 Notes

## Day 1: Tuesday June 5, 2017

### Session 101 - WWDC 2017 Keynote
:construction:
### Session 102 - Platforms State of the Union
:construction:

## Day 2: Tuesday June 6, 2017

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

## Day 3: Wednesday June 7, 2017

### Session 404 - Debugging with Xcode 9

#### Wireless Development
No more fighting over lightning cables

This will be good for AR, VR, and camera app development

Support for tvOS too

Quicktime supported wirelessly on tvOS for screen sharing

There is a Connect via Network option in Devices screen

You can connect via IP address for "complex" networks

Brave live demo of hitting a breakpoint wirelessly. At this point, they can stop selling it. We are all going to use this from now until forever anyway

There are some nice minor improvements to Instruments like the ability to transfer a debugging session and pin a track to the bottom to align it with other lanes

#### Breakpoints
Code completion added to debugging conditions and actions

Breakpoints show you if they have options set

Breakpoint navigator deep filtering

#### View Controller Debugging
View Controllers show up in the navigator under the square hotdog

SpriteKit and SceneKit are now first class citizens in the view debugger

Memory graph debugger is built with SpriteKit and the visual debugger uses SceneKit!!!

#### Summary
##### Not much substance here. If you're expecting a deep dive into LLDB and hardcore debugging, you won't find it in this session. Nice love shown to SpriteKit and Scenekit.

### Session 212 - What's New in Foundation
:construction:

### Session 802 - Essential Design Principles
The session speaks for itself and notes won't really do it justice

They discussed in detail the design principles of:
- Wayfinding
- Feedback
- Visibility
- Consistency
- Mental Model
- Proximity
- Grouping
- Mapping
- Affordance
- Progressive Disclosure
- 80/20 Rule
- Symmetry

Loved this quote, "When a system breaks out mental model, we perceive it to be unintuitive."

All of these principles allow users to:
- feel safe
- understnad
- achieve
- experience beauty and joy

#### Summary
##### This was a very cool session that should be a must watch for any engineer working on front end development (or API design). I plan to use this as a reference for high level UX best practices for a long time to come.

### Session 506 - Vision Framework: Building On Core ML
:construction:

### Session 803 - Designing Sound
:construction:

### Session 2220 - Safari, WebKit, and Password AutoFill Lab
:lock:

## Day 4: Tuesday June 8, 2017

### Session 223 - Drag and Drop with Collection and Table View

#### Placeholders 
Don't use ```reloadData```, use ```performBatchUpdates``` to avoid losing the placeholder cells

Placeholder cells come with a built in progress loading UI, can this be overriden?

#### Supporting Reordering
Use a drop proposal with type of .move

Table View will call ```performDropWith``` behind the scenes

Collection View requires you to provide a dragDelegate and dropDelegate

Collection View now allows for a reorderingCadence of:
.immediate (the current reordering behavior)
.fast (ironically named - provides a fast movement but delayed cell movement until you stop dragging)
.slow (similar to iOS SpringBoard home screen reordering)

#### Spring Loading
This works by default for Table View and Collection View

#### Customizing Cell Appearance
There are phases of .none, .lifting, .dragging

```dragStateDidChange``` lets you customize the look of your cells or drop items based on their current state

#### Customizing the Drag Preview
There is a delegate method that lets you clip or crop cell images if there are borders that you don't want to be shown in your drop item preview

#### Summary
##### Nothing earth shattering here. As expected, these foundational UI building blocks work well with drag and drop with minimal customization required but you can tweak the experience if you like. Placeholders for async cell loading is a nice addition. 

### Session 711 - Accelerate and Sparse Solvers
#### Accelerate
Start by importing Accelerate
Much faster and more energy efficient than vsmul, vclip, sgemm for matrix and vector manipulation
Don't write your own code for matrix multiplication, use Accelerate
BNNS functions in Accelerate are the backbone of CoreML

#### Compression
LZFSE on GitHub
High performance 

#### BNNS
Basic Neural Network Subroutines
High performance kernels for ML

You can generally convert a trained model from 32 bit floating point values to 8 bit unsigned ints without losing precission

Enhancements to perf for functions used by CoreML and Vision

#### simd Module
Good for small vector and matrix math

SceneKit leverages simd

Matrix multiplication is more performant and readable the BLAS or GLKit

Support for Quaternions?!?!

#### BLAS and LAPACK
Basic linear algebra subroutines & Linear Algebra PACKage

#### Sparse Matricies
Sparse Solver on Watch 2 beat Dense Solver on the MacBook Air in a race and it wasn't close

Iterative Method is only faster on huge vectors and matricies

Use Accelerate for faster and more efficient code that is hardware optimized for low level graphics or ML code

#### Summary
##### This was an extremely advanced talk on linear algebra concepts. If you aren't writing custom shaders or building a neural network framework from scratch, you won't get much out of it.

### Session 712 - What's New in Core Bluetooth
#### Introduction
Core Bluetooth is the framework to interact with BluetoothLE devices

Frameworks like Apple Music Service and iBeacon let you interact with no BTLE implementation

iOS and macOS devices are allowed to be the central and the peripheral

A BTLE device can for example, read the time off of your iPhone

The GATT database manages services and characteristics for managing transfers

#### Enhanced Readability
Enhancements to state preservation and restoration

State callbacks now persist even across device reboot or other Bluetooth system events

_NOTE: Apple calls killing an app "force quit" through the app switcher_

New property will tell your app if more data can be sent

Support for iOS, macOS, tvOS, and now watchOS

tvOS is foreground only and Central only, limited to 2 simultaneous devices, peripherals are disconnected when your app moves to the background

watchOS is similar to tvOS, central only and 2 simultaneous connections only, disconnect when app suspended

watchOS only supported on Watch Series 2

Both tvOS and watchOS

#### L2CAP Channels
This is the protocol Core Bluetooth uses and now it's available directly to developers

PSM can be thought of as the TCP port for L2CAP

There is also peripheral support for L2CAP, you can specify if encryption should be used or not

The ```CBL2CAPChannl``` class encapsulates a lot of this functionality

You get an end encountered callback when channel is closed

Use L2CAP when GATT doesn't meet your needs, when you want the best performance or lowest overhead, good for large updates like a firmware update

#### Best Practices
Discovery timeline can be optimized by using shortest advertising interval possible but beware of energy tradeoffs

Reconnecting - You can connect directly if you stored the identifier

Discovering the GATT database performs better the fewer services or characteristics you use

Support GATT caching

When making a device, use the latest chipset / Bluetooth standards (4.2 or 5.0)

#### Getting the Most out of Core Bluetooth
You can achieve an increase from 2.5kbps to nearly 400kbps using L2CAP directly with EDL can get to near 400kbps for write only transfers

#### Summary
##### Support for Watch Series 2 and direct access to the L2CAP protocol are the big news here. There are also a lot of oppotunities to increase connection speeds with the latest Bluetooth and L2CAP.

## Open Questions
1. WebViews support drag and drop by default , which ones?  UIWebView? WKWebView? SafariVC?
2. Which hardware supports iOS 11 productivity?
3. How far does the Xcode feature to mirror the file system from your groups go? When you create a new group, does it create a new folder?
4. Is there anything stopping you from compiling Swift for web ASM or has no one tried it yet?

## Watch List
- Mastering Drag and Drop
- Advances in Networking, Part 1
- Advances in Networking, Part 2
- Customized Loading in WKWebView
