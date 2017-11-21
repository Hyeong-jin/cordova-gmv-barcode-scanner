
cordova-gmv-barcode-scanner
===========================

Purpose of this Project
-----------------------

The purpose of this project is to provide a barcode scanner utilizing the Google Mobile Vision library for the Cordova framework on iOS and Android. The GMV library is incredibly performant and fast in comparison to any other barcode reader that I have used that are free. Additionally, I built it to perform live validity checks on VIN numbers for use as a VIN scanner. 

Installation
------------

To install, simply run the `cordova plugin add ` command on this git repository.

###Android

If you are using this plugin for the Android platform, it is important that you place the following code inside the `config.xml` file in the root of your Cordova project. This is a preference that will be utilized by the [`cordova-custom-config`](https://github.com/dpa99c/cordova-custom-config) library so that the theming is provided to Android. If you do not do this then the plugin will crash the application.

````xml
<preference name="android-manifest/application/@android:theme" value="@style/Theme.AppCompat" />
````

Usage
-----

To use the plugin simply call `CDV.scanner.scan(options, callback)`. See the sample below.

````javascript
CDV.scanner.scan({vinDetector: true}, function(err, result) {
    
    //Handle Errors
	if(err) return;
	
	//Do something with the data.
	alert(result);
	
	});
````

###Plugin Options

The default options are shown below. Note that the `detectorSize.width` and `detectorSize.height` values must be floats. If the values are greater than 1 then they will not be visible on the screen. Use them as decimal percentages to determine how large you want the scan area to be.
````javascript
var options = {
	types: {
		Code128: true,
		Code39: true,
		Code93: true,
		CodaBar: true,
		DataMatrix: true,
		EAN13: true,
		EAN8: true,
		ITF: true,
		QRCode: true,
		UPCA: true,
		UPCE: true,
		PDF417: true,
		Aztec: true
	},
	detectorSize: {
		width: .5,
		height: .7
	},
	vinDetector: false
}
````


###Android Quirks

The `detectorSize` option does not currently exclude the area around the detector from being scanned, which means that anything shown on the preview screen is up for grabs to the barcode detector. On iOS this is done automatically.

###VIN Scanning

VIN scanning works on both iOS and Android and utilizes both Code39 and Data Matrix formats. The scanner has a VIN checksum validator that ensures that the 9th VIN digit is correctly calculated. If it is not, the barcode will simply be skipped and the scanner will continue until it finds a valid VIN.

Project Info
------------

I am not a native developer and basically hacked both of the implementations together. That being said, in testing the plugins look fantastic, significantly more modern than other scanners, and they scan incredibly quickly. Please send @forrestmid a private message if you have any inclination towards assisting the development of this project!