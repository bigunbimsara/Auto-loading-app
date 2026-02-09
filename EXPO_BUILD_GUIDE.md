# APK එකක් හදන්නේ කෙසේද - Expo භාවිතයෙන් (පහසුම ක්‍රමය)

## පියවර 1: Node.js Install කරන්න

1. https://nodejs.org/ වෙබ් අඩවියට යන්න
2. LTS version එක download කරන්න
3. Install කරන්න (Next, Next click කරන්න)

## පියවර 2: Expo CLI Install කරන්න

Command Prompt හෝ Terminal එක open කර මෙය type කරන්න:

```bash
npm install -g expo-cli
npm install -g eas-cli
```

## පියවර 3: Expo Account එකක් හදාගන්න

```bash
expo register
# හෝ දැනටමත් account එකක් ඇත්නම්:
expo login
```

## පියවර 4: Project එක සාදන්න

```bash
# නව folder එකක්
expo init AutoReloadApp

# Template එක select කරන්න:
# → blank (TypeScript නොවේ නම්)

cd AutoReloadApp
```

## පියවර 5: Dependencies Install කරන්න

```bash
npx expo install react-native-webview
```

## පියවර 6: App.js File එක Replace කරන්න

Project folder එකේ `App.js` file එක open කර, ඉහත මම දුන් `AutoReloadApp.jsx` එකේ සියලු code එක copy කර paste කරන්න.

## පියවර 7: app.json File එක සකසන්න

`app.json` file එක මෙසේ වෙනස් කරන්න:

```json
{
  "expo": {
    "name": "Auto Reload App",
    "slug": "autoreloadapp",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "userInterfaceStyle": "light",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "android": {
      "package": "com.autoreloadapp",
      "versionCode": 1,
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#ffffff"
      },
      "permissions": [
        "INTERNET",
        "ACCESS_NETWORK_STATE",
        "WAKE_LOCK"
      ]
    },
    "plugins": [
      [
        "expo-build-properties",
        {
          "android": {
            "usesCleartextTraffic": true
          }
        }
      ]
    ]
  }
}
```

## පියවර 8: APK Build කරන්න

### විකල්පය A: EAS Build (Cloud එකේ build වේ - පහසුයි)

```bash
# EAS configure කරන්න
eas build:configure

# Android APK build කරන්න
eas build --platform android --profile preview

# Build එක complete වුණාම download link එකක් ලැබේ
```

### විකල්පය B: Local Build (ඔබේ computer එකේ build වේ)

```bash
# Android Studio install කර ඇති විට පමණක්
npx expo run:android --variant release
```

## පියවර 9: APK File එක Download කරන්න

1. EAS build complete වුණාම email එකක් එයි
2. හෝ `eas build:list` command එකෙන් බලන්න
3. Download link එක copy කර browser එකෙන් download කරන්න
4. APK file එක phone එකට transfer කරන්න (USB හෝ Google Drive)

## පියවර 10: Phone එකේ Install කරන්න

1. Phone එකේ Settings → Security → "Unknown sources" enable කරන්න
2. APK file එක open කරන්න
3. "Install" click කරන්න
4. App එක open කරන්න!

---

## ⚡ ඉක්මන් Build (Test සඳහා)

Phone එකේම test කරන්න APK එකක් නොමැතිව:

```bash
npx expo start
```

Phone එකේ "Expo Go" app එක install කර QR code එක scan කරන්න!
- Android: https://play.google.com/store/apps/details?id=host.exp.exponent
- iOS: App Store එකෙන් "Expo Go" search කරන්න

---

## ගැටළු විසඳීම

### Build Error වුණොත්:
```bash
# Cache clear කරන්න
expo start -c
```

### EAS Account නැත්නම්:
```bash
# නිදහස් account එකක් හදාගන්න
expo register
```

### APK Size වැඩියි නම්:
```bash
# AAB file එකක් හදන්න (Google Play සඳහා)
eas build --platform android --profile production
```
