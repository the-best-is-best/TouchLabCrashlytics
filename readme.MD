# How to Implement CrashKiOS - Crash Reporting for Kotlin/iOS

For more information, visit the [CrashKiOS Documentation](https://crashkios.touchlab.co/).

## Steps to Integrate CrashKiOS with Your iOS Project

### 1. Open Your Xcode Project

Start by opening your Xcode project where you want to integrate CrashKiOS.

### 2. Add Firebase SDK to Your Project

To add the Firebase SDK for iOS, follow these steps:

- Navigate to `File > Add Packages...` in Xcode.
- In the prompt, enter the Firebase repository URL: `https://github.com/firebase/firebase-ios-sdk`.
- Follow the on-screen instructions to complete the integration.

For more details, refer to the [Firebase Crashlytics iOS Setup Guide](https://firebase.google.com/docs/crashlytics/get-started?platform=ios).

### 3. Configure Firebase Crashlytics

Make sure to configure Firebase Crashlytics in your iOS project by following the instructions provided by Firebase.

### 4. Add a New Build Phase for dSYM File Export

To properly upload crash logs and symbols, you must add a new build phase:

- Go to the `Build Phases` section in Xcode.
- Add a new **Run Script Phase** and place it at the end of the build phases.
- The script should export the dSYM file, which is required for symbolication of crashes.

### 5. Export and Upload dSYM File

Before publishing your app to the App Store, export the dSYM file from the archive:

- Go to the archive in Xcode.
- Right-click the dSYM file and select **Show in Finder**.
- In Finder, you can view the contents of the dSYM file and ensure that it is properly included in the build.

In the **Input Files** section of your build script, add the following path:

```bash
${DWARF_DSYM_FOLDER_PATH}/${DWARF_DSYM_FILE_NAME}/Contents/Resources/DWARF/${PRODUCT_NAME}.debug.dylib
```
