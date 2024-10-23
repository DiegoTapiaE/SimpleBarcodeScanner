# Barcode Scanner Web App
This project is a simple barcode scanner that uses a web camera (or mobile camera) to detect barcodes. It leverages the ZXing library to scan various barcode formats using the device's camera. This app works on modern browsers for desktop and mobile devices.
## Table of Contents
1. [Features](#Features "Features")
3. [How It Works](#How_It_Works "How It Works")
4. [Supported Barcode Formats](#Supported_Barcode_Formats "Supported Barcode Formats")
	- [Limiting to Specific Barcode Formats](#Limiting_to_Specific_Barcode_Formats "Limiting to Specific Barcode Formats")
6. [Getting Started](#Getting_Started "Getting Started")
	- [Prerequisites](#Prerequisites "Prerequisites")
	- [Installation](#Installation "Installation")
	- [Usage](#Usage "Usage")
10. [Customization](#Customization "Customization")
11. [Considerations](#Considerations "Considerations")
	- [HTTPS Requirement](#HTTPS_Requirement "HTTPS Requirement")
	- [Using ngrok for Testing](#Using_ngrok_for_Testing "Using ngrok for Testing")
14. [Contributing](#Contributing "Contributing")
15. [License](#License "License")

## Features
- Start/Stop Barcode Scanning using the device's camera.
- Supports multiple barcode formats (1D and 2D barcodes).
- Vibration feedback when a barcode is detected.
- Delay mechanism to avoid multiple scans of the same barcode.

## How It Works
The web app uses the user's camera to scan for barcodes. When a barcode is detected, it displays the detected code, adds it to a list, and vibrates the device for 200ms (on supported devices).

## Supported Barcode Formats
By default, the app can scan multiple barcode formats, including:

- 1D Barcodes (Code 128, Code 39, EAN-13, UPC-A, etc.)
- 2D Barcodes (QR Code, Data Matrix, PDF417)

### Limiting to Specific Barcode Formats
If you want to limit the scanner to specific barcode formats, you can modify the scanner initialization like this:

```javascript
codeReader = new ZXing.BrowserBarcodeReader({
    formats: [ZXing.BarcodeFormat.CODE_128, ZXing.BarcodeFormat.EAN_13]
});

```
This example restricts scanning to only Code 128 and EAN-13 formats.

## Getting Started
### Prerequisites
To run the project locally, all you need is a browser that supports WebRTC and camera access (like Google Chrome, Firefox, or Safari).

### Installation
1.- Clone this repository:
```bash
git clone https://github.com/your-username/barcode-scanner-webapp.git

```
2.- Open the index.html file in your browser, or serve it using any local server like [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer "Live Server") for Visual Studio Code.

### Usage
1. Open the web app in your browser.
2. Click Start Scanning to initiate the camera.
3. Point the camera at a barcode to scan.
4. The detected barcode will be displayed and added to the list of scanned barcodes.
5. Click Stop Scanning to stop the scanner and camera stream.

###  Customization
You can easily customize the barcode formats or adjust the camera feed size by editing the source code:

- Barcode formats: Modify the formats option in the ZXing library as shown above.
- Camera settings: Change the facingMode to use the front camera instead of the back camera by modifying the initCamera() function:

```javascript
const stream = await navigator.mediaDevices.getUserMedia({
    video: { facingMode: 'user' }  // Use the front camera
});
```
## Considerations
### HTTPS Requirement
Most modern browsers block access to certain features, such as the camera and vibration API, unless the page is served over HTTPS or accessed via localhost. If you are testing this project over a non-secure (HTTP) connection, you may encounter issues where:

- The camera feed does not start.
- Vibration feedback is not triggered on supported devices.

### Using ngrok for Testing
If you need to test this project over a secure HTTPS connection during development, you can use a tool like ngrok to create a secure tunnel to your local server.

1. Install ngrok from [ngrok.com.](https://ngrok.com/ "ngrok.com.")
2. Run your local server (e.g., using Live Server).
3. Start ngrok and point it to your local server (usually running on port 5500 or 8080):
```bash
ngrok http 5500
```
7. Ngrok will provide you with an HTTPS URL that you can use to access the app securely from any device.

This will allow you to test the barcode scanner with full camera and vibration support even on external devices, like mobile phones.

## Contributing
Contributions are welcome! Please open an issue or submit a pull request with any updates or improvements.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
