# 📱 HTML File එක APK එකක් බවට හරවන්නේ කෙසේද

## ක්‍රමය 1: Website2APK Builder (වඩාත් පහසු!) ⭐

### පියවර 1: HTML File එක Host කරන්න

ඔබට 2 options තියෙනවා:

#### Option A: GitHub Pages භාවිතා කරන්න (නිදහස්)

1. https://github.com වෙබ් අඩවියට යන්න
2. Account එකක් හදාගන්න (නොමැති නම්)
3. "New Repository" click කරන්න
4. Repository name: `autoreload-app`
5. "Public" select කරන්න
6. "Add a README file" check කරන්න
7. "Create repository" click කරන්න
8. "Add file" → "Upload files" click කරන්න
9. `autoreload-simple.html` file එක upload කරන්න
10. File name එක `index.html` බවට rename කරන්න
11. "Commit changes" click කරන්න
12. Settings → Pages → Source: "main" branch select කරන්න
13. Save click කරන්න
14. ඔබේ website URL එක ලැබේ: `https://yourusername.github.io/autoreload-app/`

#### Option B: Netlify Drop භාවිතා කරන්න (ඉතා පහසු!)

1. https://app.netlify.com/drop වෙබ් අඩවියට යන්න
2. `autoreload-simple.html` file එක rename කරන්න → `index.html`
3. File එක drag & drop කරන්න browser එකට
4. ඔබේ URL එක ලැබේ: `https://random-name.netlify.app/`

### පියවර 2: APK Builder Tool එකක් භාවිතා කරන්න

#### Website2APK Builder භාවිතා කරන්න:

1. https://www.websitetoapk.com වෙබ් අඩවියට යන්න
2. "Website URL" field එකේ ඔබේ hosted URL එක paste කරන්න
3. App Name: `Auto Reload App`
4. Package Name: `com.autoreload.app`
5. Icon upload කරන්න (optional)
6. "Build APK" click කරන්න
7. APK file එක download වේ (2-5 minutes)

---

## ක්‍රමය 2: AppsGeyser (තව් පහසු option එකක්) 🎯

1. https://www.appsgeyser.com වෙබ් අඩවියට යන්න
2. "Create Free App" click කරන්න
3. "Website" template එක select කරන්න
4. ඔබේ hosted URL එක paste කරන්න
5. App details fill කරන්න:
   - App Name: Auto Reload App
   - Description: Auto reload website app
   - Icon upload කරන්න
6. "Create App" click කරන්න
7. APK download කරන්න

---

## ක්‍රමය 3: Android Studio සමඟ (Advanced) 🔧

### HTML File එක Android WebView App එකක් බවට හරවන්න

1. Android Studio install කරන්න
2. "New Project" → "Empty Activity" select කරන්න
3. Project එක configure කරන්න:
   - Name: AutoReloadApp
   - Package: com.autoreload.app
   - Language: Java/Kotlin

4. `app/src/main/assets` folder එක create කරන්න
5. `autoreload-simple.html` file එක assets folder එකට copy කරන්න

6. `MainActivity.java` file එක edit කරන්න:

```java
package com.autoreload.app;

import android.os.Bundle;
import android.webkit.WebView;
import android.webkit.WebSettings;
import android.webkit.WebViewClient;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    private WebView webView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        webView = new WebView(this);
        setContentView(webView);

        WebSettings webSettings = webView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        webSettings.setDomStorageEnabled(true);
        
        webView.setWebViewClient(new WebViewClient());
        webView.loadUrl("file:///android_asset/autoreload-simple.html");
    }

    @Override
    public void onBackPressed() {
        if (webView.canGoBack()) {
            webView.goBack();
        } else {
            super.onBackPressed();
        }
    }
}
```

7. `AndroidManifest.xml` file එකට permissions add කරන්න:

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

8. Build → Generate Signed Bundle / APK
9. APK select කරන්න → Next
10. Keystore create කරන්න
11. Build click කරන්න

---

## ක්‍රමය 4: Cordova භාවිතා කරන්න 📦

```bash
# Cordova install කරන්න
npm install -g cordova

# Project එකක් create කරන්න
cordova create AutoReloadApp com.autoreload.app AutoReloadApp
cd AutoReloadApp

# Android platform add කරන්න
cordova platform add android

# HTML file එක copy කරන්න
# autoreload-simple.html → www/index.html

# APK build කරන්න
cordova build android --release

# APK file එක:
# platforms/android/app/build/outputs/apk/release/app-release-unsigned.apk
```

---

## ඉක්මන් සංසන්දනය 📊

| ක්‍රමය | පහසුව | කාලය | මිල |
|--------|--------|------|-----|
| Website2APK | ⭐⭐⭐⭐⭐ | 5 min | නිදහස් |
| AppsGeyser | ⭐⭐⭐⭐⭐ | 3 min | නිදහස් |
| Android Studio | ⭐⭐ | 30 min | නිදහස් |
| Cordova | ⭐⭐⭐ | 10 min | නිදහස් |

## නිර්දේශය 💡

**ආරම්භකයින් සඳහා**: Website2APK හෝ AppsGeyser භාවිතා කරන්න
**Advanced users සඳහා**: Cordova හෝ Android Studio භාවිතා කරන්න

---

## APK Install කිරීම

1. Phone එකේ Settings → Security → "Unknown sources" enable කරන්න
2. APK file එක download කරන්න
3. File එක open කර install කරන්න
4. App එක enjoy කරන්න! 🎉
