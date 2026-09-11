# English B1 Tracker

اپ ردیابی مسیر دوماهه یادگیری انگلیسی (Reading/Listening/Speaking/Writing), سطح B1.
یه اپ استاتیک HTML/CSS/JS هست (`www/index.html`) که با Capacitor به Android بسته‌بندی می‌شه.

این محیط فعلاً Git و Node.js نصب نداره، پس مراحل زیر رو خودتون روی سیستم‌تون اجرا کنید.

## ۱) پیش‌نیازها

- [Git](https://git-scm.com/downloads)
- [Node.js LTS](https://nodejs.org/) (شامل npm)
- [Android Studio](https://developer.android.com/studio) (برای SDK/Gradle و ساخت APK)

## ۲) گیت

```powershell
cd C:\Users\Paradox\Desktop\Language
git init
git add .
git commit -m "Initial commit: English B1 tracker + Capacitor scaffold"
```

بعد یه ریپوی خالی روی گیت‌هاب بسازید و:

```powershell
git remote add origin <URL ریپو>
git branch -M main
git push -u origin main
```

## ۳) نصب Capacitor

```powershell
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap add android
```

این دستور یه پوشه `android/` (پروژه نیتیو اندروید) می‌سازه و باید بعد از این به گیت اضافه و کامیت بشه.

## ۴) هر بار که `www/index.html` رو عوض کردید

```powershell
npx cap sync
```

## ۵) ساخت APK

```powershell
npx cap open android
```

این Android Studio رو با پروژه باز می‌کنه؛ از منوی **Build → Build Bundle(s) / APK(s) → Build APK(s)** خروجی رو بگیرید (فایل زیر `android/app/build/outputs/apk/` قرار می‌گیره).

## نکات

- `appId` و `appName` رو تو `capacitor.config.json` قبل از `cap add android` می‌تونید عوض کنید — بعد از ساخت پروژه اندروید، تغییرش سخت‌تره.
- داده‌های کاربر (پیشرفت، واژگان، کلید API) با `localStorage` داخل خود وب‌ویو ذخیره می‌شن؛ پاک کردن داده‌های اپ از تنظیمات اندروید یا حذف اپ، این‌ها رو هم پاک می‌کنه.
