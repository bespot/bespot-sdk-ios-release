# Bespot iOS SDK - Release
> Bespot iOS SDK for proximity events and analytics reporting

[![VERSION](https://img.shields.io/badge/VERSION-0.4.4-green)](#)
[![Swift Version][swift-image]][swift-url]

Bespot iOS SDK offers proximity events and analytics reporting to 3rd party apps using BLE technology and Machine Learning methods.

## Features

- [x] Indoor location (InOut)
- [ ] Indoor area detection
- [ ] Outdoor location
- [ ] Analytics

## Requirements

- iOS 10.0+
- Xcode 13

## Installation

### CocoaPods
You can use [CocoaPods](http://cocoapods.org/) to install *BespotSDK*. See steps below:

1. Add *BespotSDK* dependency to your *Podfile* - using https git link|version. See sample code hereby:

```ruby
# Minimum supported iOS platform for BespotSDK
platform :ios, '10.0'

target '[Your app]' do
  # Needed for the project to use frameworks
  use_frameworks!

  # BespotSDK Framework
  pod 'BespotSDK', :git => 'https://gitlab.com/bespot/bespot-sdk-ios-release', :tag => '0.4.4'

  # Other CocoaPods libraries/frameworks you may use...

end
```

2. Run `pod update` for the CocoaPods to download the *BespotSDK* dependency. When you are prompted, insert the **provided** credentials (username & password) to authenticate with *GitLab*.
3. Run `pod install`


### Manually

For manually installing *BespotSDK* into your app, follow the steps below:

1. Download and drop ```BespotSDK.framework``` folder in your project (select "copy items if needed" in the popup menu).
2. Select "Embed & Sign" at the BespotSDK.framework listing in your application's Target General settings menu (Xcode 11)

## Usage example

### Preparation
BespotSDK uses CoreBluetooth. Put the `NSBluetoothAlwaysUsageDescription` key in your `Info.plist` file along with a string value explaining to the user how the app uses the Bluetooth data. Otherwise, the app will **crash** with the following console error:

```
This app has crashed because it attempted to access privacy-sensitive data without a usage description.  The app's Info.plist must contain an NSBluetoothAlwaysUsageDescription key with a string value explaining to the user how the app uses this data.
```

### Initialization

Do the import :

```swift
import BespotSDK
```

In your application's AppDelegate ```application(_:didFinishLaunchingWithOptions:)``` method add this line to init/configure the BespotSDK singleton object:

```swift
BespotSDK.shared.configure(applicationId: "your_app_id", applicationSecret: "your_app_secret")
```
### Use the `BTConfigurationDelegate` optional delegate for the Configuration of a user
In your view controller's ```viewDidLoad``` method add this:
```swift
BespotSDK.shared.configurationDelegate = self
```

Extend your view controller to implement delegate methods:
```swift
extension YourViewController: BTConfigurationDelegate {
   func didCompleteConfiguration() {
     // TODO: When the user has completed the configuration process
   }

   func didFailUpdateConfiguration(error: BTError) {
     // TODO: Inspect possible errors
   }
}
```

### Use the `BTInOutDelegate` delegate to receive InOut updates
In your view controller's ```viewDidLoad()``` method add this:

```swift
BespotSDK.shared.inOutDelegate = self
```

Extend your view controller to implement delegate methods:
```swift
extension YourViewController: BTInOutDelegate {
    func didUpdateInOut(status: BTInOutStatus) {
        // TODO: Use In-Out status
    }

    func didFailUpdateInOut(error: BTError) {
        // TODO: Inspect possible errors
    }
}
```
 Find more details regarding the errors list [here](https://docs.opap-dev.bespot.io/sdk/errors/).

### Get all available stores

```swift
BespotSDK.shared.getStores { (stores: [BTStore]?, error: BTError?) in
    // Check for error
    guard error == nil else {
        // TODO: Handle error
        return
    }

    // Check for stores
    guard let stores = stores else { return }

    // TODO: Use stores
}
```

### Subscribe for InOut status updates
In order for the solution to geolocate the nearby store (physical building), there are two ways to subscribe for InOut updates:
 - by using Bluetooth to read nearby beacons **OR**
 - by providing a location object

Use Bluetooth (default implementation):
```swift
BespotSDK.shared.subscribeForInOutUpdates()
```
**OR**

Use user's location (latitude and longitude in the form of coordinates object - `CLLocationCoordinate2D` - from `CoreLocation` iOS framework) are needed:

```swift
import CoreLocation

BespotSDK.shared.subscribeForInOutUpdates(coordinates: CLLocationCoordinate2D(latitude: USER_LOCATION_LATITUDE, longitude: USER_LOCATION_LONGITUDE))
```

### Unsubscribe from updates

To unsubscribe from updates just use this:
```swift
BespotSDK.shared.unsubscribe()
```

### Get last InOut status
Helper method to provide the last known InOut status.

```swift
// Get the InOut result tuple
let resultTuple = BespotSDK.shared.getLastInOutStatus()

// Check for error        
if let error: BTError = resultTuple.1 {
    // TODO: Handle error
}

// Check for the InOut status
guard let inOutStatus: BTInOutStatus = resultTuple.0 else { return }

// TODO: Use In-Out status

```

### Application lifecycle
It is **highly** recommended to unsubscribe from InOut updates when application enters background and subscribe again when applcation enters foreground.

In your view controller's ```viewDidLoad()``` method add this:

```swift
let notificationCenter = NotificationCenter.default
notificationCenter.addObserver(self, selector: #selector(appMovedToBackground), name: UIApplication.willResignActiveNotification, object: nil)
notificationCenter.addObserver(self, selector: #selector(appMovedToForeground), name: UIApplication.didBecomeActiveNotification, object: nil)
```

And then, implement these selector methods accordingly:

**Application moves to background**

```swift
@objc func appMovedToBackground() {
    // Unsubscribe from updates
    BespotSDK.shared.unsubscribe()
}
```

**Application moves to foreground**

```swift
@objc func appMovedToForeground() {
    // Subscribe to InOut updates again
    BespotSDK.shared.subscribeForInOutUpdates()
}
```

### Set user identifier
After initializaion/configuration is complete, user identifier can be provided at any time using the following code:

```swift
BespotSDK.shared.setUserId(USER_IDENTIFIER)
```

## Support

If you find a bug please fill out an issue report or contact us at dev@bespot.com

## License

(C) Copyright 2020-2022 Bespot P.C. All rights reserved. See `LICENSE` for more information.
[Bespot](https://bespot.com/) Location tracking to drive growth, profitability and customer engagement


[swift-image]: https://img.shields.io/badge/swift-5.0-orange.svg
[swift-url]: https://swift.org/
