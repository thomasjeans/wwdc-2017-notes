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

### Session 229 - Building Great Document-based Apps in iOS 11
#### UIDocumentBrowserViewController
There is a ```UISupportsDocumentBroswer``` key you need to set to ```YES``` in your info.plist
```UIDocumentBrowserViewController``` has a didRequestDocumentCreationWithHandler delegate method that let's you create documents

Other delegate methods get called when document creation completed, failed

You configure the Document Types your document browser view controller can pick in a different section of the info.plist

```UIDocument``` works naturally with ```UIDocumentBrowserViewController``` and gives you a lot of features out of the box

Your ```UIDocument``` subclass is where you load the actual document

A ```UIDocumentViewController``` subclass is where you open and close the ```UIDocument``` object

The ```UIDocumentBrowserViewController``` presents your document view controllers

There are 3 styles of ```UIDocumentBrowserViewController``` interfaces: dark, light, and white

The tintColor of the browser controller's view updates almost every control or element, together, these two properties let you quickly update the entire color scheme of your UI

#### Open In Place
This shows a pop over in springboard with a preview of the documents available to open

The Xcode template implements open in place for you

Calls your app delegate, you can check if the inputURL is a fileURL and if so, handle opening and presenting it

#### Custom Actions
```UIDocumentBrowserAction``` lets you define an action and a completion handler

Seems like a nice block based API, these seem to be a theme of recent CocoaTouch APIs and of the conference 

#### Custom Transitions
Let you customize creating or opening an existing document

```UIDocumentBrowserViewController``` creates the transitioning view controller for you

All you need to do is set the target view from the destination view controller and implement the ```UIViewControllerTransitioningDelegate``` protocol

Works for presenting and dismissing the document view controller

#### Thumbnails
There is a fileAttributesToWrite delegate method on your ```UIDocument``` subclass for files created by your application

There is also a new Thumbnail Extension that works system-wide under the QuickLook framework

The cloud provider asks QuickLook to look for any extensions with the thumbnail types

You can only provide thumbnails for UTIs that you own

You can draw the thumbnail or provide an image file URL

This is pretty sweet and will result in a rich platform wide document access system

There are strong implications here for a video moment sharing application

#### Summary
##### This is a big set of APIs. The team seems to have really thought this through and all of the features you would expect are here. You can get started with a base implementation by using UIDocument based documents with UIDocumentBrowserViewController and reach deeper for more powerful customizations like non iCloud cloud providers, VC transitions, and document thumbnails.

### Session 409 - What's New in Testing
:construction:
Some nice improvements to UITesting performance, they re-designed the way the system queries for UI elements

You can chain together multi app testing now by specifying the bundle ID of the app you'd like to launch or activate

You can organize like groups of test methods into Activities now, this is probably a nicer approach than the page object model our team is using now but we'll need to explore it further

You can control + click the test diamond to jump to the test report or other quick actions

The big takeaway was that you can take screen shots and save them to disk now

You can even view in the split pane editor in Xcode

You can customize when the images should be saved or discarded via the scheme settings or in the UITest code

Very nice ability to capture a full screen screenshot or a shot of an individual element, this his huge

### Session 411 - What's New in LLVM
:construction:

### Session 234 - What's New in iMessage Apps
#### What's New
New app drawer UI

When a user installs your app via the Messages App Store or the main App Store, it is installed by default in Messages and set to the most recent app

#### Direct Send
Now you can use send() API to post messages directly without the user needing to hit send

  Similar to insert() API from iOS 10
 
Make sure to clearly denote that when they tap an element, it will send right away

Requirements:
- Application must be visible (not in background)
- Can send one message per interaction only
- New error codes were added to handle these cases

#### Live Message Layouts
You can add completely custom views with maps, live updating countdowns, text - whatever you want to the conversation

You can have different views for sender and receiver

Tapping a live message can open your iMessage app in a different presentation style like full screen

This uses ```MSMessagesAppViewController``` for the view in the conversation and the app itself in the keyboard area

```MSMessageLayout``` lets you customize the app bubble with ```MSMessageTemplateLayout```

```MSMessageLiveLayout``` is new in iOS 11 lets you on devices that have your app installed and are on the latest xOS version

Use .transcript presentation style for display in the conversation in your ```MSMessagesAppViewController``` subclass
Use .compact / .expanded for display in the keyboard area

Override contentSizeThatFits to account for larger system fonts due to dynamic type

_NOTE: There is a .lineHeight property on UIFont objects_

There is an ```isPending``` property that lets you know if your vc is in the preview pane about to be sent

#### Best Practices
Use ```safeAreaInsets``` property on UIView in iOS 11

There is a ```summaryText``` property on ```MSMessage``` that will now be used for notifications when a text comes in

#### Summary
##### Major focus was on more useful and functional applications, not stickers. Hopefully the design and APIs will bring some life to this seemingly barron app ecosystem.
