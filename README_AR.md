# Attendance Pro Web (Firebase + VS Code) — مجاني 100%

هذا مشروع موقع حضور/انصراف ورواتب **Premium UI** مبني بـ:
- React + Vite
- Tailwind (تصميم فخم)
- Firebase Auth + Firestore + Hosting (Spark plan مجاني)
- PWA (ينفع تثبيته على الموبايل)

## 1) المتطلبات
- Node.js (عندك بالفعل)
- VS Code
- حساب Google (لإنشاء Firebase Project)

## 2) تشغيل محليًا
1) فك الضغط وافتح المجلد في VS Code
2) افتح Terminal ثم:
```bash
npm install
npm run dev
```
سيفتح على: http://localhost:5173

## 3) إعداد Firebase (مجاني)
### (أ) إنشاء Project
- افتح Firebase Console
- Create project (Spark)

### (ب) تفعيل Authentication
- Authentication → Sign-in method → Email/Password → Enable

> ملاحظة: نحن ندخل بـ **Username + Password**، لكن داخليًا يتم تحويله إلى Email بالشكل:
`username@attendancepro.local`

### (ج) Firestore
- Firestore Database → Create database (Production mode)
- ثم ضع Rules من الملف: `firestore.rules`

### (د) إنشاء أول Owner
1) من Firebase Console → Authentication → Add user
   - Email: `owner@attendancepro.local`
   - Password: اختر كلمة مرور قوية
2) شغل الموقع، سجّل دخول:
   - Username: `owner`
   - Password: (الذي وضعته)
3) افتح: `/bootstrap` لإكمال البيانات
   - أول مستخدم سيأخذ role=owner تلقائيًا (إذا لم يوجد meta/system)

### (هـ) إنشاء الموظفين
- Firebase Console → Authentication → Add user
  - Email: `emp1@attendancepro.local`
  - Password: ...
- الموظف أول ما يسجّل دخول: يفتح `/bootstrap` وسيتم إنشاء ملفه role=employee
- بعد ذلك Owner/HR يمكنه تعديل بياناته من صفحة Employees (قريبًا نضيف تعديل كامل).

## 4) نشر على Firebase Hosting (مجاني)
### تثبيت Firebase CLI
```bash
npm i -g firebase-tools
firebase login
```

### ربط المشروع
داخل مجلد المشروع:
```bash
firebase init
```
اختر:
- Hosting
- Firestore

> يمكنك استخدام الملفات الموجودة `firebase.json` و `firestore.rules` و `firestore.indexes.json`

### Build + Deploy
```bash
npm run build
firebase deploy
```

## 5) ملاحظات أمان (مهم)
- الموظف/المدير لا يرى إلا بياناته
- Owner/HR يمكنهم رؤية الموظفين
- Owner فقط يعدّل سياسة الدوام

## 6) إضافات مقترحة لاحقًا
- إدارة موظفين كاملة (تعديل رواتب/دور/active من داخل الموقع)
- تقارير PDF/Excel
- بصمة/QR/Geofencing (عبر Progressive enhancement)
