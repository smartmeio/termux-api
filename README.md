# Termux API

[![Build status](https://github.com/termux/termux-api/workflows/Build/badge.svg)](https://github.com/termux/termux-api/actions)
[![Join the chat at https://gitter.im/termux/termux](https://badges.gitter.im/termux/termux.svg)](https://gitter.im/termux/termux)

This is an app exposing Android API to command line usage and scripts or programs.

When developing or packaging, note that this app needs to be signed with the same
key as the main Termux app for permissions to work (only the main Termux app are
allowed to call the API methods in this app).

## Installation

Termux:API application can be obtained from [F-Droid](https://f-droid.org/en/packages/com.termux.api/).

Additionally we provide per-commit debug builds for those who want to try
out the latest features or test their pull request. This build can be obtained
from one of the workflow runs listed on [Github Actions](https://github.com/termux/termux-api/actions)
page.

Signature keys of all offered builds are different. Before you switch the
installation source, you will have to uninstall the Termux application and
all currently installed plugins.

## License# Termux API

[![Build status](https://github.com/termux/termux-api/workflows/Build/badge.svg)](https://github.com/termux/termux-api/actions)
[![Join the chat at https://gitter.im/termux/termux](https://badges.gitter.im/termux/termux.svg)](https://gitter.im/termux/termux)

This is an app exposing Android API to command line usage and scripts or programs.

When developing or packaging, note that this app needs to be signed with the same
key as the main Termux app for permissions to work (only the main Termux app are
allowed to call the API methods in this app).

## Installation

Termux:API application can be obtained from [F-Droid](https://f-droid.org/en/packages/com.termux.api/).

Additionally we provide per-commit debug builds for those who want to try
out the latest features or test their pull request. This build can be obtained
from one of the workflow runs listed on [Github Actions](https://github.com/termux/termux-api/actions)
page.

Signature keys of all offered builds are different. Before you switch the
installation source, you will have to uninstall the Termux application and
all currently installed plugins.

## License

Released under the [GPLv3 license](http://www.gnu.org/licenses/gpl-3.0.en.html).

## How API calls are made through the termux-api helper binary

The [termux-api](https://github.com/termux/termux-api-package/blob/master/termux-api.c)
client binary in the `termux-api` package generates two linux anonymous namespace
sockets, and passes their address to the [TermuxApiReceiver broadcast receiver](https://github.com/termux/termux-api/blob/master/app/src/main/java/com/termux/api/TermuxApiReceiver.java)
as in:

```
/system/bin/am broadcast ${BROADCAST_RECEIVER} --es socket_input ${INPUT_SOCKET} --es socket_output ${OUTPUT_SOCKET}
```

The two sockets are used to forward stdin from `termux-api` to the relevant API
class and output from the API class to the stdout of `termux-api`.

## Client scripts

Client scripts which processes command line arguments before calling the
`termux-api` helper binary are available in the [termux-api package](https://github.com/termux/termux-api-package).

## Ideas

- Wifi network search and connect.
- Add extra permissions to the app to (un)install apps, stop processes etc.


## Permission request

To remember the permission of USB device after reboot tablet or Unplug/plug USB device you have to create another activity to manage these permissions, in particular "UsbEventReceiverActivity".

In Androidmanifest.xml add the activity in this way:
```xml

        <activity
            android:name="com.termux.api.util.UsbEventReceiverActivity"
            android:label="Termux-API:SmartME.io"
            android:theme="@style/Theme.Transparent"
            android:noHistory="true"
            android:excludeFromRecents="true"
            android:taskAffinity="com.example.taskAffinityUsbEventReceiver"
            android:process=":UsbEventReceiverActivityProcess"
            android:exported="false"
            android:directBootAware="true"
            >
            <intent-filter>
                <action android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED" />
            </intent-filter>
            <meta-data android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED" android:resource="@xml/usb_device_filter" />
        </activity>

```
```<intent-filter>``` tag's are used to to filter particular devices attaced by metadata, in this case PID and VID.

On ```usb_device_filter.xml``` there is a list of device.

```xml 

<resources>
    <!--ARANCINO MIGNON -->
    <usb-device vendor-id="####" product-id="######" />
    <!--ARANCINO -->
   <usb-device vendor-id="####" product-id="######" />
</resources>

```


## Automatically power on when charger is connected.

To enable this feature on Android device follow these steps:

1- Enable USB-Debugging.

2- Turn on device on fastboot mode.

3- Connect device to pc.
 
4- Run this command from pc on SDK/platforms-tools folder:
    ```bash
        ./fasboot oem off-mode-charge 0
    ```.


Released under the [GPLv3 license](http://www.gnu.org/licenses/gpl-3.0.en.html).

## How API calls are made through the termux-api helper binary

The [termux-api](https://github.com/termux/termux-api-package/blob/master/termux-api.c)
client binary in the `termux-api` package generates two linux anonymous namespace
sockets, and passes their address to the [TermuxApiReceiver broadcast receiver](https://github.com/termux/termux-api/blob/master/app/src/main/java/com/termux/api/TermuxApiReceiver.java)
as in:

```
/system/bin/am broadcast ${BROADCAST_RECEIVER} --es socket_input ${INPUT_SOCKET} --es socket_output ${OUTPUT_SOCKET}
```

The two sockets are used to forward stdin from `termux-api` to the relevant API
class and output from the API class to the stdout of `termux-api`.

## Client scripts

Client scripts which processes command line arguments before calling the
`termux-api` helper binary are available in the [termux-api package](https://github.com/termux/termux-api-package).

## Ideas

- Wifi network search and connect.
- Add extra permissions to the app to (un)install apps, stop processes etc.
