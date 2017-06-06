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
New API for encoding Swift data structures like Enum and Stuct

New KeyPath type

Updates to KVO with KeyPaths

Block-based KVO

Deferring system gestures...

Notification Center - iOS 5

Control Center - iOS 7

iOS 11 provides override method that returns ```UIRectEdge``` objects you want to protect (aka defer the system gesture)

##### Auto Layout and ScrollView
Adding ```contentLayoutGuide``` and ```frameLayoutGuide``` to ```UIScrollView```

##### Dynamic Type
New class ```UIFontMetrics``` that lets you create standard size with a custom font then Dynamic Type system can scale it like a system font

Auto Layout has a new ```constraintEqualToSystemSpacing``` method that takes two anchors and tries to work out a good fit based on Dynamic Type changes

NOTE: A lot of Auto Layout code was shown with no storyboards...do these two prefer programatic?

##### Password AutoFill
System detects User / Password UI fields and presents a key that launches your iCloud Keychain stored passwords

Add an entitlement to your app then a few lines of JSON

Entire session on Password AutoFill

Colors and icons can be added to Asset Catalogs

App thinning for icons - adopted by default in iOS 11 new projects

PDF-backed images

Tab bar images can re-size with accessibility settings (or a future use case?)

##### ProMotion
Can ask ```UIScreen``` for ```maximumFramesPerSecond```

Key as always is to optimize drawing code using Instruments

##### Summary
###### What's new in CocoaTouch?  Not all that much.  Some solid hardening and minor feature additions.

### Session 203 - Introducing Drag and Drop

