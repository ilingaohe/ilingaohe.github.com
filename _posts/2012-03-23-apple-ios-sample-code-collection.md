---
layout: post
title: "苹果iOS范例代码集锦"
category: 学习笔记
tags: [iOS]
---
{% include JB/setup %}

## 学习目的

苹果官方提供了一系列非常优秀的iOS代码范例，这里做一个整理和集锦。

## 具体例子

#### [ABUIGroups](http://developer.apple.com/library/ios/#samplecode/ABUIGroups/Introduction/Intro.html#//apple_ref/doc/uid/DTS40011307)

ABUIGroups demonstrates how to retrieve, add, and remove group records from the address book database using AddressBook APIs. It displays groups organized by their source in the address book.

----

#### [AccelerometerGraph](http://developer.apple.com/library/ios/#samplecode/AccelerometerGraph/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007410)

AccelerometerGraph sample application graphs the motion of the device. It demonstrates how to use the UIAccelerometer class and how to use Quartz2D and Core Animation to provide a high performance graph view. It also demonstrates a low-pass filter that you can use to isolate the effects of gravity, and a high-pass filter that you can use to remove the effects of gravity.

----

#### [Accessory](http://developer.apple.com/library/ios/#samplecode/Accessory/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008066)

Demonstrates how to implement a custom accessory view for your UITableView in the form of a checkmark button. It shows you how to override the appearance or control of the accessory view, much like that of "UITableViewCellAccessoryDetailDisclosureButton". It implements the custom accessory view by setting the table's "accessoryView" property with a UIButton of type "UIButtonTypeCustom". It can be toggled by selecting the entire table row by implementing UITableView's "didSelectRowAtIndexPath". The green checkmark is trackable (checked/unchecked), and can be toggled independent of table selection.

----

#### [AddMusic](http://developer.apple.com/library/ios/#samplecode/AddMusic/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008845)  

AddMusic demonstrates basic use of iPod library access, part of the Media Player framework. You use iPod library access to play songs, audio books, and audio podcasts that are synced from a user's desktop iTunes library. This sample uses the Media Player framework's built-in user interface for choosing music.  
AddMusic also demonstrates how to mix application audio with iPod library audio. The sample includes code for configuring application audio behavior using the AVAudioSession class and Audio Session Services.  

----

#### [AdvancedTableViewCells](http://developer.apple.com/library/ios/#samplecode/AdvancedTableViewCells/Introduction/Intro.html#//apple_ref/doc/uid/DTS40009111)

AdvancedTableViewCells includes three different cells that all display content in the same form as the App Store application. One uses individual subviews (image views, labels, etc.) to display the content. Another uses a single view that draws all of the content. A third uses a single view to draw most of the content and separate views for the remainder.

----

#### [AdvancedURLConnections](http://developer.apple.com/library/ios/#samplecode/AdvancedURLConnections/Introduction/Intro.html#//apple_ref/doc/uid/DTS40009558)

This sample demonstrates various advanced networking techniques with NSURLConnection. Specifically, it demonstrates how to respond to authentication challenges, how to modify the default server trust evaluation (for example, to support a server with a self-signed certificate), and how to provide client identities.

----

#### [AlternateViews](http://developer.apple.com/library/ios/#samplecode/AlternateViews/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008755)

Demonstrates how to implement alternate or distinguishing view controllers for each particular device orientation. Through the help of the following UIViewController properties, this can be easily achieved -

@property(nonatomic,assign) UIModalTransitionStyle modalTransitionStyle;	// for a transition fade

@property(nonatomic,assign) BOOL wantsFullScreenLayout; // for any view controller to appear over another

This sample implements a two different view controllers one for portrait and one for landscape. The portrait view controller listens for device orientations in order to properly swap in and out the landscape view controller. It uses the above two properties to achieve the visual cross-fade effect.

----

#### [AppPrefs](http://developer.apple.com/library/ios/#samplecode/AppPrefs/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007799)

Demonstrates how to display your app's preferences or settings in the "Settings" system application. A settings bundle, included in your application’s bundle directory, contains the information needed by the Settings application to display your preferences and make it possible for the user to modify them. It then saves any configured values in the defaults database so that your application can retrieve them at runtime.

This sample also shows how to dynamically update it's UI when its settings are changed while the app is in the background via "NSUserDefaultsDidChangeNotification".

This sample offers an Xcode project already pre-configured to build your Settings bundle as a target. To customize your settings UI, change the Root.plist file.

----

#### [AQOfflineRenderTest](http://developer.apple.com/library/ios/#samplecode/AQOfflineRenderTest/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008413)

Demonstrates using Audio Queue offline render functionality and the AudioQueueOfflineRender API. The sample produces LPCM output buffers from an ALAC encoded source which are then written to a .caf file. The output.caf file is then played back confirming the offline functionality worked as expected. All the code demonstrating the Audio Queue is in a single file called aqofflinerender.cpp.

----

#### [Audio Mixer (MixerHost)](http://developer.apple.com/library/ios/#samplecode/MixerHost/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010210)

MixerHost demonstrates how to use the Multichannel Mixer audio unit in an iOS application. It also demonstrates how to use a render callback function to provide audio to an audio unit input bus. In this sample, the audio delivered by the callback comes from two short loops read from disk. You could use a similar callback, however, to synthesize sounds to feed into a mixer unit. This sample is described in Audio Unit Hosting Guide for iOS.

----

#### [Audio UI Sounds (SysSound)](http://developer.apple.com/library/ios/#samplecode/SysSound/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008018)

Demonstrates use of System Sound Services (AudioToolbox/AudioServices.h) to play alerts and user-interface sound effects, and to invoke vibration.

----

#### [aurioTouch](http://developer.apple.com/library/ios/#samplecode/aurioTouch/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007770)

aurioTouch demonstrates use of the remote i/o audio unit for handling audio input and output. The application can display the input audio in one of the forms, a regular time domain waveform, a frequency domain waveform (computed by performing a fast fourier transform on the incoming signal), and a sonogram view (a view displaying the frequency content of a signal over time, with the color signaling relative power, the y axis being frequency and the x as time).  

The code in auriouTouch uses the remote i/o audio unit (AURemoteIO) for input and output of audio, and OpenGL for display of the input waveform. The application also uses Audio Session Services to manage route changes (as described in Core Audio Overview).  

----

#### [aurioTouch2](http://developer.apple.com/library/ios/#samplecode/aurioTouch2/Introduction/Intro.html#//apple_ref/doc/uid/DTS40011369)

aurioTouch2 demonstrates use of the remote i/o audio unit (AURemoteIO) for handling audio input and output. The application can display the input audio in one of the forms, a regular time domain waveform, a frequency domain waveform (computed by performing a fast fourier transform on the incoming signal), and a sonogram view (a view displaying the frequency content of a signal over time, with the color signaling relative power, the y axis being frequency and the x as time).

The code in aurioTouch2 uses the remote i/o audio unit (AURemoteIO) for input and output of audio, and OpenGL for display of the input waveform. The application also uses Audio Session Services to manage route changes (as described in Core Audio Overview).

aurioTouch2 supports iOS 5 or later.

----

#### [AVCam](http://developer.apple.com/library/ios/#samplecode/AVCam/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010112)

AVCam demonstrates how to use the AV Foundation capture APIs for recording movies and taking still images. There is a record button for recording movies, a camera button for switching between front and back cameras (on supported devices), and a still button for taking still images.

----

#### [AVMovieExporter](http://developer.apple.com/library/ios/#samplecode/AVMovieExporter/Introduction/Intro.html#//apple_ref/doc/uid/DTS40011364)

This universal sample application reads movie files from the Asset Library and Media Library then exports them to a new media file using user defined settings. The user can adjust the exported file in the following ways:

- Export presets can be chosen which influence the size and quality of the output.

- The file type can be changed.

- Tracks and existing metadata can be inspected.

- Metadata can be replaced or deleted.

----

#### [AVPlayerDemo](http://developer.apple.com/library/ios/#samplecode/AVPlayerDemo/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010101)

Uses AVPlayer to play videos from the iPod Library, Camera Roll, or via iTunes File Sharing. Also displays metadata.

----

#### [avTouch](http://developer.apple.com/library/ios/#samplecode/avTouch/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008636)

The avTouch sample demonstrates use of the AVAudioPlayer class for basic audio playback.

The code in avTouch uses the AV Foundation framework to play a file containing AAC audio data. The application uses Core Graphics and OpenGL to display sound volume meters during playback.

This application shows how to:

* Create an AVAudioPlayer object from an input audio file.

* Use OpenGL and Core Graphics to display metering levels.

* Use Audio Session Services to set an appropriate audio session category for playback.

* Use the AVAudioPlayer interruption delegate methods to pause playback upon receiving an interruption, and to then resume playback if the interruption ends.

* Demonstrates a technique to perform Fast Forward and Rewind

avTouch does not demonstrate how to play multiple files, nor does it demonstrate more advanced use of AV Foundation.

----

#### [BatteryStatus](http://developer.apple.com/library/ios/#samplecode/BatteryStatus/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008812)

Demonstrates the use of the battery status properties and notifications provided via the iOS SDK.

----

#### [BonjourWeb](http://developer.apple.com/library/ios/#samplecode/BonjourWeb/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007415)

This application illustrates the fundamentals of browsing for network services using Bonjour. The BonjourBrowser hierarchically displays Bonjour domains and services as table views in a navigation controller. The contents of the table views are discovered and updated dynamically using NSNetServiceBrowser objects. Tapping an item in the services table causes the corresponding NSNetService object to be resolved asynchronously. When that resolution completes, a delegate method is called which constructs a URL and opens it in Safari.

----

#### [Breadcrumb](http://developer.apple.com/library/ios/#samplecode/Breadcrumb/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010048)

Demonstrates how to draw a path using the Map Kit overlay, MKOverlayView, that follows and tracks the user's current location. The included CrumbPath and CrumbPathView overlay and overlay view classes can be used for any path of points that are expected to change over time. It also demonstrates what is needed to track the user's location as a background process.

----

#### [BubbleLevel](http://developer.apple.com/library/ios/#samplecode/BubbleLevel/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007331)

The Bubble Level sample application demonstrates how to receive and interpret acceleration information, animate a view, and display a utility view (used for calibration).

----

#### [CopyPasteTile](http://developer.apple.com/library/ios/#samplecode/CopyPasteTile/Introduction/Intro.html#//apple_ref/doc/uid/DTS40009040)

CopyPasteTile demonstrates how to implement the copy-cut-paste feature introduced in iPhone OS 3.0. The sample:

* Shows how to use the UIMenuController class to position and display the editing menu (the menu with the Copy, Cut, Paste, and other commands).

* Illustrates how you might implement the canPerformAction:withSender: method of UIResponder to validate the menu commands for the current context.

* Shows how to respond when the user taps a menu command by reading and writing data to a pasteboard, (an instance of the UIPasteboard class).

----

#### [CoreDataBooks](http://developer.apple.com/library/ios/#samplecode/CoreDataBooks/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008405)

This sample illustrates a number of aspects of working with the Core Data framework with an iPhone application:

* Use of an instance of NSFetchedResultsController object to manage a collection of objects to be displayed in a table view.

* Undo and redo.

* Database initialization.

* Use of a second managed object context to isolate changes during an add operation.

----

#### [CoreTelephonyDemo](http://developer.apple.com/library/ios/#samplecode/CoreTelephonyDemo/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010746)

This sample shows how to use Core Telephony framework to access the user's current calls, call center and carrier information.

The application uses a grouped table view with 3 sections, each section displaying one Core Telephony object.

The techniques shown in this sample are:   
* correct way of instantiating Core Telephony framework objects   
* using a block-based event handler to receive call events    
* access Core Telephony object properties

----

#### [CoreTextPageViewer](http://developer.apple.com/library/ios/#samplecode/CoreTextPageViewer/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010699)

This sample shows how to use Core Text to display large bodies of text, text with mixed styles, and text with special style or layout requirements, such as use of custom fonts. A version of this sample was used in the "Advanced Text Handling for iPhone OS" WWDC 2010 Session.

----

#### [CryptoExercise](http://developer.apple.com/library/ios/#samplecode/CryptoExercise/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008019)

This sample demonstrates the use of the two main Cryptographic API sets on the iPhone OS SDK. Asymmetric Key Encryption and random nonce generation is handled through the Security framework API set, whereas, Symmetric Key Encryption and Digest generation is handled by the CommonCrypto API set. The CryptoExercise sample brings both of these APIs together through a network service, discoverable via Bonjour, that performs a "dummy" cryptographic protocol between devices found on the same subnet.

----

#### [CurrentAddress](http://developer.apple.com/library/ios/#samplecode/CurrentAddress/Introduction/Intro.html#//apple_ref/doc/uid/DTS40009469)

Demonstrates basic use of MapKit, displaying a map view and setting its region to current location.

It makes use of the MKReverseGeocoder class that provides services for converting your map coordinate (specified as a latitude/longitude pair) into information about that coordinate, such as the country, city, or street. A reverse geocoder object is a single-shot object that works with a network-based map service to look up placemark information for its specified coordinate value. To use placemark information is leverages the MKPlacemark class to store this information.

----

#### [DateCell](http://developer.apple.com/library/ios/#samplecode/DateCell/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008866)

Demonstrates formatted display of date objects in UITableViewCells and use of UIDatePicker to edit those values.

Using a grouped style UITableViewController, the sample has two UITableViewCells to draw the primary title and NSDate value. This is accomplished using the built-in cell type "UITableViewCellStyleValue1" which supports left and right text. In addition, this sample shows how to use NSDateFormatter class to achieve the custom cell's date-formatted appearance.

----

#### [DateSectionTitles](http://developer.apple.com/library/ios/#samplecode/DateSectionTitles/Introduction/Intro.html#//apple_ref/doc/uid/DTS40009939)

This application shows how to create section information for NSFetchedResultsController using dates.

A single table view controller displays events sorted by date and grouped into sections by year and month. The Event entity has three attributes:

* timeStamp (persistent NSDate object).

The time stamp represents the time the event occurred.

* title (persistent NSString object).

The title of each event as it will be displayed on a row in the table view (this is not to be confused with section title). When the default data is created in the application delegate, the title is initialized to a string representation of the date.

* sectionIdentifier (transient NSString object).

The sectionIdentifier is used to divide the events into sections in the table view. It is a string value representing the number ((year * 1000) + month). Using this value, events can be correctly ordered chronologically regardless of the actual name of the month. It is calculated and cached on demand in the custom accessor method.

The sorting is all done at fetch time by the fetched results controller. The section name transformations are UI level and have no effect on the order of data.

----

#### [DocInteraction](http://developer.apple.com/library/ios/#samplecode/DocInteraction/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010052)

Demonstrates how to use UIDocumentInteractionController to obtain information about documents and how to preview them. There are two ways to preview documents: one is to use UIDocumentInteractionController's preview API, the other is directly use QLPreviewController. This sample also demonstrates the use of UIFileSharingEnabled feature so you can upload documents to the application using iTunes and then to preview them. With the help of "kqueue" kernel event notifications, the sample monitors the contents of the Documents folder.

----

#### [DrillDownSave](http://developer.apple.com/library/ios/#samplecode/DrillDownSave/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007800)

Demonstrates how to restore the user's current location in a drill-down list style user interface and restore that location when the app is relaunched. The drill-down or content hierarchy is generated from a plist file called 'outline.plist'. The sample stores the user's location in its preferences file using NSUserDefaults.

----

#### [EADemo](http://developer.apple.com/library/ios/#samplecode/EADemo/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010079)

The sample can be used with any Made For iPod (MFI) device designed for use with the External Accessory Framework. The application will display an External Accessory attached device in the Accessories window, provide information registered by the MFI device, and provides methods to send and receive data to the device.

----

#### [ExternalDisplay](http://developer.apple.com/library/ios/#samplecode/ExternalDisplay/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010724)

How to detect the presence of an external display, determine the available display resolutions, select a resolution, and show content on the display.

---- 

#### [FastEnumerationSample](http://developer.apple.com/library/ios/#samplecode/FastEnumerationSample/Introduction/Intro.html#//apple_ref/doc/uid/DTS40009411)

A Mac OS X command line project that demonstrates how to implement the NSFastEnumeration protocol. In this sample the MyFastEnumerationSample class implements -countByEnumeratingWithState:objects:count: to return strings on demand. This sample avoids considering how you may implement a storage class, whereas a real implementation would likely need to do less work to provide values, such as directly copying object pointers from an internal representation. Regardless of your class's actual implementation, adopting the NSFastEnumeration protocol also allows you to use the for...in syntax to access your containers objects.

----

#### [Formulaic](http://developer.apple.com/library/ios/#samplecode/Formulaic/Introduction/Intro.html#//apple_ref/doc/uid/DTS40008932)

Formulaic is a sample iPhone app that illustrates how to effectively use the iPhone Accessibility API. Using the Accessibility API allows your app to work correctly with VoiceOver.

The app draws a graph of a formula and allows the user to change certain constants in the formula, however its main purpose is to illustrate the iPhone Accessibility API.

----

#### [GenericKeychain](http://developer.apple.com/library/ios/#samplecode/GenericKeychain/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007797)

This sample shows how to add, query for, remove, and update a keychain item of generic class type. Also demonstrates the use of shared keychain items. All classes exhibit very similar behavior so the included examples will scale to the other classes of Keychain Item: Internet Password, Certificate, Key, and Identity.

----

#### [GeocoderDemo](http://developer.apple.com/library/ios/#samplecode/GeocoderDemo/Introduction/Intro.html#//apple_ref/doc/uid/DTS40011097)

This sample application demonstrates using a CLGeocoder instance to perform forward and reverse geocoding on strings and dictionaries. The application also includes an example distance calculator that will display the distance between two placemarks.

----

#### [Popovers](http://developer.apple.com/library/ios/#samplecode/Popovers/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010436)

This sample demonstrates proper use of UIPopoverController in iOS. UIPopoverController presentation, dismissing, and rotation handling are covered. The sample is provided using a UISplitViewController in order to show proper handling of UIPopoverControllers being presented from UIBarButtonItems. Additional handling ensures that multiple UIPopoverControllers are never presented at the same time.

----

## 其他资料
1. [Collection of Open Source Apps and Sample Code](http://www.ifans.com/forums/threads/collection-of-open-source-apps-and-sample-code.147476/)


