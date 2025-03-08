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

To properly upload crash logs and symbols, you need to add a new build phase:

- Go to the `Build Phases` section in Xcode.
- Add a new **Run Script Phase** and place it at the end of the build phases.
- The script should export the dSYM file, which is required for symbolication of crashes.

### 5. Export and Upload the dSYM File

Before publishing your app to the App Store, export the dSYM file from the archive:

1. **Build Your App** in Xcode and create an archive (`Product > Archive`).
2. Once the archive is ready, go to the **Organizer** window in Xcode.
3. **Right-click** on the archive in the Organizer and select **Show in Finder**.
4. In Finder, **right-click** the `.xcarchive` file and select **Show Package Contents**.
5. Locate the **dSYM file** (it will have the `.dSYM` extension) inside the package.
6. **Compress** the dSYM file (right-click and select **Compress**).
7. Upload this compressed dSYM file to Firebase for symbolication.

<br>
<p> Please add it to with the build phases </p>
In the **Input Files** section of your build script, add the following path:

```bash
${DWARF_DSYM_FOLDER_PATH}/${DWARF_DSYM_FILE_NAME}/Contents/Resources/DWARF/${PRODUCT_NAME}.debug.dylib
