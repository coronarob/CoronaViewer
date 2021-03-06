# CoronaViewer (for CoronaCards)

CoronaViewer lets you edit the contents of a `CoronaView` instance and preview those code changes in __real-time__ on your __device__. 

In this workflow, your native app does not have to be recompiled/relinked/reinstalled onto the device. You can edit your Lua code from your desktop editor/IDE and your Corona-related project files will automatically sync and update in the corresponding `CoronaView` in your native app. (This also works with apps you build in the Xcode Simulator.)

NOTE: [Corona SDK/Enterprise](http://coronalabs.com/products/corona-sdk/) developers should go [here](https://github.com/coronalabs/CoronaViewer).

## Getting Started

### Installation

The `CoronaViewer.framework` should be installed so that its path is:

`/Users/Shared/CoronaLabs/ios/CoronaViewer.framework`

### Code Integration

There are several simple steps:

1. Add `CoronaViewer.framework` to your Xcode project.
2. Use `CoronaViewerController` instead of `CoronaViewController`. The former is a drop-in replacement for the latter. Note that the two differ in spelling just slightly — there is an '<strong>er</strong>' in 'CoronaView<strong>er</strong>Controller'.
3. Disable your call to the `run` or `runWithPath:parameters:` selector of your `CoronaView` instance.
4. Instead, you run via the controller. Specifically, call `CoronaViewerController`'s `run` selector.
5. Ensure that launch url's are handled correctly by adding the following to your implementation of the  `UIApplicationDelegate`:

    ```
    - (BOOL)application:(UIApplication *)app openURL:(NSURL *)url sourceApplication:(NSString *)source annotation:(id)annotation
    {
    	return [CoronaViewerController handleOpenURL:url];
    }
    ```
6. Modify your `Info.plist` so that Dropbox can interact with CoronaViewer properly:

    ```
    <key>CFBundleURLTypes</key>
    <array>
    	<dict>
    		<key>CFBundleURLSchemes</key>
    		<array>
    			<string>db-l1q0pln8qsi8qyp</string>
    		</array>
    	</dict>
    </array>
    ```


### Dropbox

CoronaViewer requires a [Dropbox](https://db.tt/uQgIqtPN) account. You'll also want to install Dropbox on your desktop computer so that you can sync edits from your desktop to the device.

### Where Files Go

Your Corona project files (e.g. `main.lua`) should go in the following location in order to be shared:

	${DROPBOX_FOLDER}/Apps/CoronaViewer

NOTE: Only files in this location will be synchronized with your device. The rest of your Dropbox folder is __not__ visible to CoronaViewer.

### Running on device

Build the Corona project in this repo and install it on your device. ([Corona Enterprise](http://coronalabs.com/products/enterprise/) users, see below for additional info.)

You'll be prompted with Dropbox's standard login interface:

![Dropbox Login UI iOS](README/dropbox-login-ios.png)

This enables the app to synchronize with your Corona project files (i.e. files that are in the above location.)

#### Xcode Simulator

You can also build this app for the Xcode Simulator instead of for your device.


## Limitations

### File Updates

Files are updated based on modification time. To get the device to update the file, you must make sure the modification time is newer.


## Availability

### Supported Platforms

* iOS
* Android (TBD)

### Product Tiers

CoronaViewer is available to the following subscriptions/tiers:

* __Corona SDK (Pro)__ uses a slightly different workflow. [Learn more](https://github.com/coronalabs/CoronaViewer)
* __Corona Enterprise__ uses a slightly different workflow. [Learn more](https://github.com/coronalabs/CoronaViewer)
* __CoronaCards__

