# Customized PhoneGap Plugin BarcodeScanner for iOS only
================================

[![Build Status](https://travis-ci.org/phonegap/phonegap-plugin-barcodescanner.svg)](https://travis-ci.org/phonegap/phonegap-plugin-barcodescanner)

Cross-platform BarcodeScanner for Cordova / PhoneGap.

Follows the [Cordova Plugin spec](https://cordova.apache.org/docs/en/latest/plugin_ref/spec.html), so that it works with [Plugman](https://github.com/apache/cordova-plugman).

This plugin is forked from [PhoneGap Plugin BarcodeScanner](https://github.com/phonegap/phonegap-plugin-barcodescanner) and customized by BlueROR815 for iOS only.

## Installation

```
ionic cordova plugin add https://github.com/blueror815/phonegap-plugin-barcodescanner.git
```
After running the above, just follow command

```
npm install --save @ionic-native/barcode-scanner
```

### Supported Platforms

- Android
- iOS
- Windows (Windows/Windows Phone 8.1 and Windows 10)
- Windows Phone 8
- BlackBerry 10
- Browser


## Using the plugin ##
The plugin creates the object `cordova.plugins.barcodeScanner` with the method `scan(success, fail)`.

The following barcode types are currently supported:

|  Barcode Type | Android | iOS | Windows8 | Windows Phone 8 | BlackBerry 10 |
|---------------|:-------:|:---:|:--------:|:---------------:|:-------------:|
| QR_CODE       |    ✔    |  ✔  |     ✔    |        ✔        |       ✖       |
| DATA_MATRIX   |    ✔    |  ✔  |     ✔    |        ✔        |       ✔       |
| UPC_A         |    ✔    |  ✔  |     ✔    |        ✔        |       ✔       |
| UPC_E         |    ✔    |  ✔  |     ✔    |        ✔        |       ✔       |
| EAN_8         |    ✔    |  ✔  |     ✔    |        ✔        |       ✔       |
| EAN_13        |    ✔    |  ✔  |     ✔    |        ✔        |       ✔       |
| CODE_39       |    ✔    |  ✔  |     ✔    |        ✔        |       ✔       |
| CODE_93       |    ✔    |  ✖  |     ✔    |        ✔        |       ✖       |
| CODE_128      |    ✔    |  ✔  |     ✔    |        ✔        |       ✔       |
| CODABAR       |    ✔    |  ✖  |     ✔    |        ✔        |       ✖       |
| ITF           |    ✔    |  ✔  |     ✔    |        ✔        |       ✔       |
| RSS14         |    ✔    |  ✖  |     ✔    |        ✔        |       ✖       |
| PDF417        |    ✔    |  ✖  |     ✔    |        ✔        |       ✖       |
| RSS_EXPANDED  |    ✔    |  ✖  |     ✖    |        ✖        |       ✖       |
| MSI           |    ✖    |  ✖  |     ✔    |        ✔        |       ✖       |
| AZTEC         |    ✖    |  ✖  |     ✔    |        ✔        |       ✔       |

`success` and `fail` are callback functions. Success is passed an object with data, type and cancelled properties. Data is the text representation of the barcode data, type is the type of barcode detected and cancelled is whether or not the user cancelled the scan.

A full example could be:
```js
   cordova.plugins.barcodeScanner.scan(
      function (result) {
          alert("We got a barcode\n" +
                "Result: " + result.text + "\n" +
                "Format: " + result.format + "\n" +
                "Cancelled: " + result.cancelled);
      },
      function (error) {
          alert("Scanning failed: " + error);
      },
      {
          preferFrontCamera : true, // iOS and Android
          showFlipCameraButton : true, // iOS and Android
          showTorchButton : true, // iOS and Android
          torchOn: true, // Android, launch with the torch switched on (if available)
          saveHistory: true, // Android, save scan history (default false)
          prompt : "Place a barcode inside the scan area", // Android
          resultDisplayDuration: 500, // Android, display scanned text for X ms. 0 suppresses it entirely, default 1500
          formats : "QR_CODE,PDF_417", // default: all but PDF_417 and RSS_EXPANDED
          orientation : "landscape", // Android only (portrait|landscape), default unset so it rotates with the device
          disableAnimations : true, // iOS
          disableSuccessBeep: false // iOS and Android
      }
   );
```

## Encoding a Barcode ##

The plugin creates the object `cordova.plugins.barcodeScanner` with the method `encode(type, data, success, fail)`.

Supported encoding types:

* TEXT_TYPE
* EMAIL_TYPE
* PHONE_TYPE
* SMS_TYPE

```
A full example could be:

   cordova.plugins.barcodeScanner.encode(cordova.plugins.barcodeScanner.Encode.TEXT_TYPE, "http://www.nytimes.com", function(success) {
            alert("encode success: " + success);
          }, function(fail) {
            alert("encoding failed: " + fail);
          }
        );
```

## Windows quirks ##

* Windows implementation currently doesn't support encode functionality.

* On Windows 10 desktop ensure that you have Windows Media Player and Media Feature pack installed.

## Windows Phone 8 quirks ##
Windows Phone 8 implementation currently doesn't support encode functionality.

## BlackBerry 10 quirks
BlackBerry 10 implementation currently doesn't support encode functionality.
Cancelling a scan on BlackBerry 10 is done by touching the screen.

## Thanks on Github ##

So many -- check out the original [iOS](https://github.com/phonegap/phonegap-plugins/tree/DEPRECATED/iOS/BarcodeScanner),  [Android](https://github.com/phonegap/phonegap-plugins/tree/DEPRECATED/Android/BarcodeScanner) and
[BlackBerry 10](https://github.com/blackberry/WebWorks-Community-APIs/tree/master/BB10-Cordova/BarcodeScanner) repos.

