# Bespot iOS SDK - Release
> Bespot iOS SDK for proximity events and analytics reporting

[![VERSION](https://img.shields.io/badge/VERSION-0.0.2-green)](#)
[![Swift Version][swift-image]][swift-url]
[![License][license-image]][license-url]

Bespot iOS SDK offers proximity events and analytics reporting to 3rd party apps using BLE technology and Machine Learning methods.

## Features

- [x] Indoor location (InOut)
- [ ] Indoor area detection
- [ ] Outdoor location
- [ ] Analytics

## Requirements

- iOS 10.0+
- Xcode 12

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
  pod 'BespotSDK', :git => 'https://gitlab.com/bespot/bespot-sdk-ios-release.git', :tag => '0.1.0'

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

```Swift
import BespotSDK
```

In your application's AppDelegate ```application(_:didFinishLaunchingWithOptions:)``` method add this line to init/configure the BespotSDK singleton object:

```Swift
BespotSDK.shared.configure(applicationId: "your_app_id", applicationSecret: "your_app_secret")
```

### Use the `BTInOutDelegate` delegate to receive InOut updates
In your view controller's ```viewDidLoad()``` method add this:

```Swift
BespotSDK.shared.inOutDelegate = self
```

Extend your view controller to implement delegate methods:
```Swift
extension YourViewController: BTInOutDelegate {
    func didUpdateInOut(status: BTInOutStatus) {
        // TODO: Use In-Out status
    }

    func didFailUpdateInOut(error: BTError) {
        // TODO: Inspect possible errors
    }
}
```



### Subscribe for In-Out status updates
The user's location (latitude and longitude) are needed in order for the solution to geolocate the nearby store (physical building).

```Swift
BespotSDK.shared.subscribeForInOutUpdates(latitude: USER_LOCATION_LATITUDE, longitude: USER_LOCATION_LANGITUDE)
```

### Unsubscribe from updates

To unsubscribe from updates just use this:
```Swift
BespotSDK.shared.unsubscribe()
```

## Support

If you find a bug please fill out an issue report or contact us at dev@bespot.me

## License
Distributed under the MIT license. See ``LICENSE`` for more information.


[swift-image]: https://img.shields.io/badge/swift-5.0-orange.svg
[swift-url]: https://swift.org/
[license-image]: https://img.shields.io/badge/License-MIT-blue.svg
[license-url]: https://opensource.org/licenses/MIT
