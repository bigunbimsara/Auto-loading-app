# APK එකක් හදන්නේ කෙසේද - React Native CLI භාවිතයෙන්

⚠️ **මෙය වඩාත් අපහසුයි. Expo ක්‍රමය භාවිතා කිරීම නිර්දේශිතයි!**

## පූර්ව අවශ්‍යතා

### Windows සඳහා:

1. **Node.js** - https://nodejs.org/ (LTS version)
2. **JDK 17** - https://adoptium.net/
3. **Android Studio** - https://developer.android.com/studio

### පියවර 1: Android Studio Setup

1. Android Studio install කරන්න
2. "SDK Manager" open කරන්න
3. Install කරන්න:
   - Android SDK Platform 33
   - Android SDK Build-Tools
   - Android Emulator
   - Android SDK Platform-Tools

4. Environment Variables සකසන්න:
   ```
   ANDROID_HOME = C:\Users\YourName\AppData\Local\Android\Sdk
   Path එකට add කරන්න:
   - %ANDROID_HOME%\platform-tools
   - %ANDROID_HOME%\tools
   - %ANDROID_HOME%\tools\bin
   ```

### පියවර 2: React Native CLI Install කරන්න

```bash
npm install -g react-native-cli
```

### පියවර 3: Project එක සාදන්න

```bash
npx react-native init AutoReloadApp
cd AutoReloadApp
```

### පියවර 4: WebView Install කරන්න

```bash
npm install react-native-webview
cd android
./gradlew clean
cd ..
```

### පියවර 5: App.tsx/App.js Replace කරන්න

Project folder එකේ `App.tsx` හෝ `App.js` file එක AutoReloadApp.jsx code එකෙන් replace කරන්න.

### පියවර 6: Android Permissions සකසන්න

`android/app/src/main/AndroidManifest.xml` file එක open කර:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />

    <application
      android:name=".MainApplication"
      android:label="@string/app_name"
      android:icon="@mipmap/ic_launcher"
      android:roundIcon="@mipmap/ic_launcher_round"
      android:allowBackup="false"
      android:theme="@style/AppTheme"
      android:usesCleartextTraffic="true">
      
      <!-- Rest of the file... -->
    </application>
</manifest>
```

### පියවර 7: Build Configuration (build.gradle)

`android/app/build.gradle` file එකේ:

```gradle
android {
    ...
    defaultConfig {
        ...
        versionCode 1
        versionName "1.0"
    }
    
    signingConfigs {
        release {
            // Keystore details (පියවර 8 බලන්න)
        }
    }
    
    buildTypes {
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
            signingConfig signingConfigs.release
        }
    }
}
```

### පියවර 8: Signing Key එකක් Generate කරන්න

```bash
cd android/app
keytool -genkeypair -v -storetype PKCS12 -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000

# Password එකක් type කරන්න (මතක තබාගන්න!)
```

### පියවර 9: Gradle Properties සකසන්න

`android/gradle.properties` file එකට add කරන්න:

```
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=your-password-here
MYAPP_RELEASE_KEY_PASSWORD=your-password-here
```

### පියවර 10: Release APK Build කරන්න

```bash
cd android
./gradlew assembleRelease

# Windows එකේ:
gradlew.bat assembleRelease
```

### පියවර 11: APK File එක සොයාගන්න

APK file එක මෙතන තිබේ:
```
android/app/build/outputs/apk/release/app-release.apk
```

### පියවර 12: Phone එකට Install කරන්න

1. APK file එක phone එකට copy කරන්න
2. Phone එකේ Settings → Security → "Install unknown apps" enable කරන්න
3. File manager එකෙන් APK එක open කර install කරන්න

---

## AAB File එකක් Build කරන්නේ කෙසේද (Google Play සඳහා)

```bash
cd android
./gradlew bundleRelease
```

AAB file එක: `android/app/build/outputs/bundle/release/app-release.aab`

---

## Common Errors

### Error: SDK location not found
```bash
# android/local.properties file එකක් හදන්න:
sdk.dir = C:\\Users\\YourName\\AppData\\Local\\Android\\Sdk
```

### Error: Execution failed for task ':app:packageRelease'
```bash
cd android
./gradlew clean
./gradlew assembleRelease
```

### Build එක fail වුණොත්:
```bash
# Cache clear කරන්න
cd android
./gradlew clean
cd ..
rm -rf node_modules
npm install
cd android
./gradlew assembleRelease
```
