# English B1 Tracker

اپ ردیابی مسیر دوماهه یادگیری انگلیسی (Reading/Listening/Speaking/Writing), سطح B1.
یه اپ استاتیک HTML/CSS/JS هست (`docs/index.html`) با مانیفست PWA و آیکون، که به دو روش می‌تونه APK بشه.

- **ریپو:** https://github.com/777para2x777-Cs/Language-Learning
- **لینک زنده (GitHub Pages):** https://777para2x777-cs.github.io/Language-Learning/

## روش ۱ — PWABuilder (ساده‌تر)

1. به [pwabuilder.com](https://www.pwabuilder.com/) برید.
2. لینک زنده بالا رو وارد کنید و Start بزنید.
3. تب Android رو انتخاب کنید و پکیج APK/AAB رو بسازید و دانلود کنید.

هر بار که `docs/` رو عوض و push کردید، GitHub Pages خودش ظرف چند دقیقه آپدیت می‌شه و PWABuilder نسخه جدید رو می‌گیره.

## روش ۲ — Capacitor (برای کنترل بیشتر روی پروژه نیتیو اندروید)

### پیش‌نیاز
- [Node.js LTS](https://nodejs.org/) (شامل npm)
- [Android Studio](https://developer.android.com/studio) (برای SDK/Gradle)

### نصب و ساخت
```powershell
cd C:\Users\Paradox\Desktop\Language
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap add android
```

این دستور یه پوشه `android/` (پروژه نیتیو اندروید) می‌سازه — بعدش به گیت اضافه و کامیت کنید.

هر بار که `docs/index.html` رو عوض کردید:
```powershell
npx cap sync
npx cap open android
```

از Android Studio، منوی **Build → Build Bundle(s) / APK(s) → Build APK(s)** رو بزنید (خروجی زیر `android/app/build/outputs/apk/`).

## نکات

- `appId` و `appName` تو `capacitor.config.json` هستن — قبل از `cap add android` قابل تغییرن.
- داده‌های کاربر (پیشرفت، واژگان، کلید API) با `localStorage` داخل خود وب‌ویو/مرورگر ذخیره می‌شن؛ پاک کردن داده‌های اپ یا حذف اپ، این‌ها رو هم پاک می‌کنه.
- آیکون فعلی (`docs/icons/`) یه پلیس‌هولدر ساده‌ست — هر وقت خواستید عوضش کنید.
