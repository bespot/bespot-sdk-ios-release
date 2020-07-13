# Bespot iOS SDK - Release
> Bespot iOS SDK for proximity events and analytics reporting

[![Swift Version][swift-image]][swift-url]
[![License][license-image]][license-url]

Bespot iOS SDK offers proximity events and analytics reporting to 3rd party apps using BLE technology and Machine Learning methods.

## Features

- [x] Indoor/Outdoor events
- [x] Analytics

## Requirements

- iOS 10.0+
- Xcode 11

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

Do the import :
```Swift
import BespotSDK
```

In your view controller's ```viewDidLoad()``` method add these:
```Swift
// Initialize Bespot Proximity object
let proximity = BespotProximity()

// Print 'Hello World!' message
print(proximity.helloWorld())
```

## Support

[Konstantinos Dimitros](k.dimitros@bespot.me)

## License
Distributed under the MIT license. See ``LICENSE`` for more information.


[swift-image]: https://img.shields.io/badge/swift-5.0-orange.svg
[swift-url]: https://swift.org/
[license-image]: https://img.shields.io/badge/License-MIT-blue.svg
[license-url]: https://opensource.org/licenses/MIT
