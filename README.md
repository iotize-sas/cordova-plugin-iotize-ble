# IMPORTANT NOTE

This library is **deprecated**. To keep using BLE for IoTize Cordova Apps, see the new plugin here:
[@iotize/device-com-ble.cordova](https://www.npmjs.com/package/@iotize/device-com-ble.cordova)

# Bluetooth Low Energy (BLE) for IoTize devices Plugin for Apache Cordova

This plugin enables communication between a mobile and a BLE enabled IOTIZE device.

The plugin provides a simple [JavaScript API](#api) for iOS, Android and Windows.

 * Scan for ble iotize devices
 * Connect to a device
 * Send a Request and returns the reponse from the device


## Supported Platforms

* iOS
* Android ()
* Windows (10) 

# Installing

### Cordova

    $ cordova plugin add @iotize/cordova-plugin-iotize-ble
    $ ionic cordova plugin add @iotize/cordova-plugin-iotize-ble
    for iOS since the plugin is in swift language, before using iotize-ble plugin , cordova-plugin-add-swift-support:https://github.com/akofman/cordova-plugin-add-swift-support should be installed. 

# API

## Methods

- [iotize-ble.checkAvailable](#checkAvailable)
- [iotize-ble.startScan](#startScan)
- [iotize-ble.stopScan](#stopScan)
- [iotize-ble.connect](#connect)
- [iotize-ble.disConnect](#disConnect)
- [iotize-ble.isConnected](#isConnected)
- [iotize-ble.send](#send)

## checkAvailable

Check availability of BLE.

    iotize-ble.checkAvailable(success, failure);

### Description

Function `checkAvailable` returns true or false upon the availability of BLE on device.  

For Android, BLE is available from version 4.3.  
iOS platform has had support for BLE since iPhone 4s and iOs 5. 
For Windows, BLE GATT and GAP roles have been introduced in Windows 10 version 1703.

## startScan

Start scanning for Iotize BLE devices.

    iotize-ble.startScan(success, failure);

### Description

Function `startScan` scans for IoTize BLE devices. Scanning will continue until `stopScan` is called or a connection is established. The success callback is called each time a new peripheral is discovered. 

Advertising information is different depending on your platform. For Android and Windows, the device is identified with its MAC address and for iOS the device is identified with a unique UUID. The success callback is called at each discovery with returning an object containing the following information:
- name: name of the peripheral.
- address: UUID or MAC address of the peripheral.
- rssi: the threshold RSSI in dBm.          
 

### Parameters

- __success__: Success callback function that is invoked upon each discovery. The callback is called with the device information as parameter.
- __failure__: Error callback function, invoked when error occurs. The error string is passed as a parameter. 


## stopScan

Stop scanning for BLE peripherals.

    iotize-ble.stopScan(success, failure);

### Description

Function `stopScan` stops scanning for BLE devices.

### Parameters

- __success__: Success callback function, invoked when scanning is stopped. 
- __failure__: Error callback function, invoked when error occurs.

### Quick Example

    iotize-ble.startScan([], function(device) {
        console.log(device);
    }, failure);

    setTimeout(function() {
        iotize-ble.stopScan(
            function() { console.log("Scan complete"); },
            function() { console.log("stopScan failed"); }
        );
    }, 2000);
    
## connect

Connect to a peripheral.

    iotize-ble.connect(device_id, connectCallback, connectionErrorCallback);

### Description

Function `connect` connects to an iotize BLE peripheral. The connectCallback callback will be called when the connection is successful. 

The connectionErrorCallback callback is called if the connection fails, or later if the peripheral disconnects for any reason. The connectionErrorCallback callback is only called when the peripheral initates the disconnection. 

### Scanning before connecting

Devices should be scanned before connection. Please note that for this version only one device at a time could be connected.

### Parameters

- __device_id__: Mac address or UUID of the ble device.
- __connectCallback__: Connect callback function that is invoked when the connection is successful.
- __connectionErrorCallback__: Disconnect callback function, invoked when the peripheral disconnects or an error occurs.

## disconnect

Disconnect.

    iotize-ble.disConnect(device_id, success, failure);

### Description

Function `disConnect` disconnects the selected device.

### Parameters

- __device_id__: Mac address or UUID of the device.
- __success__: Success callback function that is invoked when the connection is successful.
- __failure__: Error callback function, invoked when error occurs.

## send

sends a frame of byte to ioTize device using SPP characteristic.

    iotize-ble.send(device_id, __data__, success, failure);

### Parameters
- __device_id__: Mac address or UUID of the device.
- __data__: binary data as a string ex:"A2CA000007010003FFFF0002"
- __success__: Success callback function that is invoked when the connection is successful. The result parameter is the response as a string :"45496F547A50723030343130303030313039429000"
- __failure__: Error callback function, invoked when error occurs. 

### Quick Example

    // read data from a characteristic, do something with received data
    iotize-ble.send(
               name,
               data,
               function successHandler(result) {
                   console.log("received result " + result);            
                   observer.complete();
               },
               function errorHandler(err) {
                   observer.error(err);
               });
       });


# Testing the Plugin


# License

MIT

# Feedback

Try the code. If you find an problem or missing feature pluease contact Iotize support team .
