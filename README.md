# atlas-sdk-ios

# ATLAS SDK (iOS)
![version](https://img.shields.io/badge/version-v1.0.0-blue)

ATLAS SDK is used to capture all types of Location, Document, Face, Aadhaar, Data, Video, Email, Phone, Consent, Video Declaration.

You can find the latest changelog at [Changelog](CHANGELOG.md).

# Table Of Content

- [Set Up Atlas SDK](#set-up-atlas-sdk)
    - [Requirements](#requirements)
    -  [Permission](#Permission)
    - [Install Atlas SDK](#install-atlas-sdk)
- [Getting Started](#getting-started)
- [Atlas Result](#atlas-result)
- [Help](#help)

## Set Up Atlas SDK

#### Requirements
Make sure that your project meets these requirements:
- Xcode 16.4
- iOS 13.0+
- Swift 5.0

## Permission

In Info.plist file add following code to allow your application to access :
iPhone's camera:
``<key>NSCameraUsageDescription</key>
<string>Allow access to camera</string>``

Location access :
``<key>NSLocationWhenInUseUsageDescription</key>
<string>Allow access to location</string>``

Microphone access : 
``<key>NSMicrophoneUsageDescription</key>
 <string>Allow access to microphone</string>``


#### Install Atlas SDK

### Cocoapods


You can use [CocoaPods](http://cocoapods.org/) to install `atlas` by adding it to your `Podfile`:

```ruby
source 'https://gitlab.com/frslabs-public/ios/atlas-sdk-ios.git'
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
target '<Your Target Name>' do
use_frameworks!
pod 'Atlas', '1.0.0'
end
```
###### Save/Edit Netrc settings to install custom pod

You will need a valid netrc credentials to install atlas from maven, which can be obtained by contacting `support@frslabs.com`. 

1. Create or edit .netrc file under current user's home directory
2. Write the below lines into that file, replace <YOUR_USERNAME> and <YOUR_PASSWORD> with your credentials which is shared through email and save the file.
```ruby
machine www.repo2.frslabs.space
login <YOUR_USERNAME>
password <YOUR_PASSOWRD>
```
3. In terminal enter below command to install the pod 

   pod install or pod update or pod install --repo-update.

To get the full benefits import `Atlas` wherever you import UIKit

``` swift
import UIKit
import Atlas
```
## Getting Started

### Swift

1. Initialize the input parameters and import delegate atlasControllerDelegate

```swift
class YourViewController: UIViewController,atlasControllerDelegate {

    func atlasScanner(_ scanner: Atlas.AtlasNavigationController, didFinishScanningWithResults results: Atlas.atlasScannerResults) {
        print(results.capturedSucess)
    }
    
    func atlasScanner(_ scanner: Atlas.AtlasNavigationController, didCancel cancel: String) {
        print("cancel")
    }
    
    func atlasScanner(_ scanner: Atlas.AtlasNavigationController, didFailWithError error: String) {
        print(error)
    }
}
```

2. Invoke Atlas SDK

```swift
    // ...
    
    override func viewDidLoad(_ animated: Bool) {
        let scanner = AtlasNavigationController(delegate:self)
        scanner.modalPresentationStyle = .fullScreen
        scanner.checkId = "CHECK_ID" //Pleaae input the check ID
        scanner.AtlasUrlType = "STAGING" (or) "PRODUCTION"  
        present(scanner, animated: true)
    }
    
    // ...    
```

## Atlas Result

You can use the following methods in the `AtlasResult` instance to parse the success result:

| Return Type              | Method                        | Usage                                                            |
| ------------------------ | ----------------------------- | ---------------------------------------------------------------- |
| String | results.capturedSucess          | Returns a string value of "success" after successfull capture                             |

`results.capturedSucess` returns capture is successfull instance with following methods:

```swift
  (results.capturedSucess)
```

## Help
For any queries/feedback , contact us at `support@frslabs.com`
