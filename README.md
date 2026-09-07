# 🎓 SchoolPass AI - Aqlli Maktab Davomat va Ruxsat Tizimi

**SchoolPass AI** — maktab o‘quvchilarining dars qoldirishini nazorat qilish, ota-onadan ruxsat olish, sinf rahbari tomonidan tasdiqlash/rad etish, davomatni avtomatlashtirish hamda Google Gemini AI yordamida rasmiy tushuntirish xatlarini shakllantirish uchun mo‘ljallangan to‘liq, professional, real ishlaydigan web-platforma.

---

## 🌟 Asosiy Imkoniyatlar va Yangiliklar

1. **3 Ta Mustaqil Rol & Dynamic Permissions**:
   - **Ota-ona (Parent)**: Farzandlarini tizimga kiritish yoki kod orqali bog‘lash, dars qoldirish uchun ruxsat so‘rash (butun kun yoki ma'lum darslar), Gemini AI orqali sababni rasmiylashtirish, so‘rovlar tarixini kuzatish, rasmiy tushuntirish xatlarini yaratish va davomatni ko‘rish.
   - **Sinf Rahbari (Teacher)**:
     - Mustaqil ro‘yxatdan o‘tish (`/register`).
     - Yangi o‘qituvchi hisobi dastlab **`PENDING VERIFICATION`** holatida bo‘ladi.
     - Admin tasdiqlaganidan so‘ng (`VERIFIED`) sinfiga to‘liq kirish huquqiga ega bo‘ladi. (Agar maktab bergan maxsus `TEACH-2026` kodi kiritilsa, hisob avtomatik tasdiqlanadi).
     - Kelgan ruxsat so‘rovlarini 1-klik bilan **TASDIQLASH** yoki sabab yozib **RAD ETISH**, kunlik davomatni (Present, Absent, Excused, Late) kiritish, haftalik interaktiv grafiklar va Gemini AI Davomat tahlili.
   - **Administrator (Admin)**: Maktablar, sinflar yaratish, yangi o‘qituvchilarni tekshirish (**Tasdiqlash**, **Rad etish**, **Bloklash**, **Sinfga biriktirish**), o‘quvchilar va o‘qituvchilar ma'lumotlar bazasi, barcha so‘rovlar va xavfsizlik audit loglari.

2. **Qat'iy Zero Shadow Dizayn (NO SHADOWS)**:
   - Hech bir joyda `box-shadow` yoki `text-shadow` ishlatilmagan!
   - Chuqurlik: qirrali chegaralar (`border border-slate-800`), shaffof qatlamlar (`backdrop-blur-xl`), gradientlar, yuqori kontrast va ranglar ierarxiyasi orqali hosil qilingan.

3. **Motion Design & Animatsiyalar (Framer Motion)**:
   - Smooth 60 FPS page transitions, modal ochilishlari, kartalar animatsiyasi.
   - AI Chatbotda interaktiv typing indicator (jonli yozish effekti).
   - Tizim bo‘ylab suzuvchi Toast bildirishnomalari.
   - `prefers-reduced-motion` qo‘llab-quvvatlanishi.

4. **Dark / Light Mode**:
   - Navbarda animatsion Quyosh / Oy (Sun / Moon) tugmasi.
   - Ikkala rejimda ham Zero Shadow qoidasi 100% saqlanadi.

5. **Google Gemini AI Integratsiyasi**:
   - **SchoolPass AI Chatbot**: Pastki o‘ng burchakdagi suzuvchi AI yordamchi — maktab tartib-qoidalari, davomat va ruxsat qoidalari bo‘yicha savollarga o‘zbek tilida javob beradi.
   - **Tushuntirish Xati Generatori**: Ota-ona qisqacha sabab yozsa, Gemini AI rasmiy, odobli ariza matnini tayyorlab beradi.
   - **Sababni Rasmiylashtirish (Inline AI)**: Ruxsat formasida sababni rasmiy shaklga keltiradi.
   - **AI Davomat Tahlili**: Sinfdagi dars qoldirish dinamikasi va o‘quvchilar intizomi bo‘yicha xolis tahlil.

6. **Avtomatlashtirilgan Ish Oqimi (Business Logic)**:
   - Ota-ona so‘rov yuborgan zahoti sinf rahbariga bildirishnoma boradi.
   - Sinf rahbari tasdiqlasa $\rightarrow$ o‘quvchining davomati avtomatik ravishda **`EXCUSED` (Uzrli)** holatiga o‘tadi.
   - Rad etilsa $\rightarrow$ ota-onaga rad etish sababi bilan bildirishnoma boradi.

---

## 🔑 Demo Sinov Akkountlari

Tizimda sinab ko‘rish uchun tayyor 3 ta rol mavjud (shuningdek, Login sahifasida 1-klik bilan kirish tugmalari ham bor):

| Rol | Email | Parol | Mas'uliyati |
|---|---|---|---|
| **Ota-ona** | `otaona@schoolpass.uz` | `parent123` | Jamshid Valiyev (Farzandlari: Ali va Madina Valiyeva) |
| **Sinf Rahbari** | `oqituvchi@schoolpass.uz` | `teacher123` | Dilrabo Karimova (9-A sinf rahbari - Verified) |
| **Admin** | `admin@schoolpass.uz` | `admin123` | Sardor Aliyev (Maktab Administratori) |

---

## 🚀 O‘rnatish va Ishga Tushirish

### 1. Talablar
- Node.js v18.17+
- npm yoki pnpm

### 2. Kutubxonalarni O‘rnatish
```bash
npm install
```

### 3. Muhit O‘zgaruvchilari (`.env`)
```env
DATABASE_URL="file:./dev.db"
JWT_SECRET="schoolpass_ai_super_secret_jwt_key_2026_production"
NEXT_PUBLIC_APP_URL="http://localhost:3000"

# Google Gemini API kaliti (ixtiyoriy, kiritilmasa mustahkam fallback ishlaydi):
GEMINI_API_KEY=""
```

### 4. Ma’lumotlar Bazasini Ishga Tushirish & Seed
```bash
npx prisma db push
node prisma/seed.js
```

### 5. Dasturni Ishga Tushirish
```bash
npm run dev
```
Brauzerda oching: **[http://localhost:3000](http://localhost:3000)**

---

## 🧪 Sinov Ketma-ketligi (E2E Test)

1. **O‘qituvchi Ro‘yxatdan O‘tishi va Admin Tasdiqlashi**:
   - `/register` sahifasiga o‘tib, "Sinf Rahbari Ro‘yxati" tabini tanlang.
   - Ism, familiya va sinf ma'lumotlarini kiriting va ro‘yxatdan o‘ting.
   - Tizim sizga hisob "PENDING VERIFICATION" holatidaligini bildiradi.
   - `/login` ga kiring va "Admin sifatida kirish" tugmasini bosing.
   - "O‘qituvchilar" sahifasiga o‘ting — yangi ro‘yxatdan o‘tgan o‘qituvchini ko‘rasiz.
   - **[TASDIQLASH]** tugmasini bosing. Endi o‘qituvchi tizimga kirishi mumkin!
2. **Ota-ona Ruxsat So‘rovi**:
   - `/login` dan Ota-ona sifatida kiring.
   - "Ruxsat so‘rash" sahifasida sabab yozing, "AI bilan rasmiylashtirish" tugmasini bosing va yuboring.
3. **Sinf Rahbari Qarori va Davomat**:
   - Sinf rahbari sifatida kiring.
   - "Ruxsat so‘rovlari" bo‘limida yangi so‘rovni ochib **[TASDIQLASH]** ni bosing.
   - "Kunlik davomat" sahifasiga o‘ting — o‘quvchining davomati avtomatik **"Uzrli"** deb belgilanganini ko‘rasiz!
4. **Gemini AI Chatbot & Xat Yozish**:
   - Pastki o‘ng burchakdagi "SchoolPass AI" tugmasini bosing va AI bilan suhbatlashing.
   - "Tushuntirish xatlari" bo‘limida AI yordamida rasmiy xat yaratib ko‘ring.
5. **Theme Switcher**:
   - Navbardagi Quyosh/Oy tugmasini bosib Yorug‘ va Tungi rejimlarni sinab ko‘ring.

---
© 2026 SchoolPass AI. Clean Architecture & Strict Zero Shadow Framework.
