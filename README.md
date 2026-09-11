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

## همگام‌سازی پیشرفت بین دستگاه‌ها (اختیاری)

پیشرفت اپ به‌صورت پیش‌فرض فقط تو `localStorage` همون مرورگر ذخیره می‌شه (per-device). دو راه برای یکی‌کردنش هست، هر دو از داشبورد اپ (بخش «☁️ همگام‌سازی بین دستگاه‌ها») در دسترسن:

### روش ساده — فایل پشتیبان
دکمه «خروجی گرفتن از پیشرفت» یه فایل JSON دانلود می‌کنه؛ همون فایل رو با دکمه «وارد کردن از فایل» تو دستگاه دیگه بارگذاری کنید. دستی‌ست، ولی نیازی به هیچ سرویس بیرونی نداره.

### روش زنده — Firebase (رایگان)
1. به [console.firebase.google.com](https://console.firebase.google.com/) برید، با یه اکانت گوگل وارد بشید و **Add project** بزنید (نیازی به کارت اعتباری نیست، پلن رایگان Spark کافیه).
2. تو پروژه جدید، از منوی سمت چپ **Build → Firestore Database** برید و **Create database** بزنید (هر منطقه‌ای، mode مهم نیست چون قوانین امنیتی رو دستی می‌نویسیم).
3. تو تب **Rules** همون Firestore، قوانین رو با این جایگزین کنید و **Publish** بزنید:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /sync/{code} {
         allow read, write: if true;
       }
     }
   }
   ```
   (این قانون عمداً بازه — امنیتش با «کد همگام‌سازی» طولانی و تصادفی تأمین می‌شه، نه با لاگین؛ کد رو مثل یه رمز عبور جایی share نکنید.)
4. به **Project settings** (⚙️ کنار Project Overview) برید، پایین صفحه تو بخش **Your apps** روی آیکون وب (`</>`) بزنید، یه اسم دلخواه بدید، **Register app** کنید.
5. یه شیء `firebaseConfig` بهتون نشون می‌ده (چیزی شبیه `{ apiKey: "...", authDomain: "...", projectId: "...", ... }`) — دقیقاً همون رو کپی کنید.
6. تو اپ، داشبورد → «☁️ همگام‌سازی بین دستگاه‌ها» رو باز کنید، همون شیء رو تو باکس «پیکربندی Firebase» پیست کنید و ذخیره کنید.
7. یه «کد همگام‌سازی» بسازید (یا دستی وارد کنید) و «اتصال» بزنید.
8. تو دستگاه دوم، همین ۶ و ۷ رو تکرار کنید — تو مرحله ۷ **همون کد دقیقاً** رو وارد کنید (نه ساختن کد جدید) تا به همون پیشرفت وصل بشه.

از اون به بعد، هر تغییری (تیک‌زدن جلسه، لغت جدید، فلش‌کارت، و غیره) با یه تأخیر کوتاه خودکار به Firestore push می‌شه، و هر بار که اپ باز می‌شه آخرین نسخه رو می‌کشه پایین.

## نکات

- `appId` و `appName` تو `capacitor.config.json` هستن — قبل از `cap add android` قابل تغییرن.
- داده‌های کاربر (پیشرفت، واژگان، کلید API) با `localStorage` داخل خود وب‌ویو/مرورگر ذخیره می‌شن؛ پاک کردن داده‌های اپ یا حذف اپ، این‌ها رو هم پاک می‌کنه (مگراینکه همگام‌سازی ابری وصل باشه).
- آیکون فعلی (`docs/icons/`) یه پلیس‌هولدر ساده‌ست — هر وقت خواستید عوضش کنید.
