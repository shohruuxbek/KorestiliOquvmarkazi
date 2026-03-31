# O'quv Markazi Boshqaruv Tizimi (BOYGI Loyihasi)

## 📋 Loyiha Haqida
O'quv markazlari uchun to'liq boshqaruv tizimi. Backend (NestJS) va Frontend (React) dan iborat.

## ✨ Imkoniyatlar
- 👨🎓 **Talabalar boshqaruvi** - Ro'yxatga olish, ma'lumotlarini saqlash
- 👨🏫 **O'qituvchilar boshqaruvi** - O'qituvchilar ro'yxati va ma'lumotlari
- 📚 **Kurslar boshqaruvi** - Kurslar yaratish va taqsimlash
- 💰 **To'lovlar boshqaruvi** - To'lovlarni kuzatish va hisobot
- ✅ **Davomat nazorati** - Talabalar davomatini yuritish
- 🏆 **Reyting tizimi** - O'quvchilarga ball berish va eng yaxshilarni aniqlash
- 📊 **Dashboard** - Umumiy statistika va daromad

## 🚀 Ishga Tushirish

### Backend (NestJS)
```bash
cd backend
npm install
npm run start:dev
```
Backend `http://localhost:3000` da ishlaydi.

### Frontend (React)
```bash
cd frontend
npm install
npm run dev
```
Frontend `http://localhost:5173` da ishlaydi.

## 🔐 Demo Accountlar

| Role | Username | Password |
|------|----------|----------|
| 👑 Admin | admin | admin123 |
| 👨🏫 Teacher | teacher1 | teacher1 |
| 👨🎓 Student | student1 | student123 |

**Muhim:** Birinchi marta kirishda "Demo foydalanuvchilarni yaratish" tugmasini bosing!

## 📁 Loyiha Tuzilishi
```
KOOREST TRILI/
├── backend/              # NestJS backend
│   ├── src/
│   │   ├── students/    # Talabalar moduli
│   │   ├── teachers/    # O'qituvchilar moduli
│   │   ├── courses/     # Kurslar moduli
│   │   ├── payments/    # To'lovlar moduli
│   │   ├── attendance/  # Davomat moduli
│   │   ├── auth/        # Autentifikatsiya moduli
│   │   └── main.ts      # Asosiy fayl
│   └── package.json
├── frontend/            # React frontend
│   ├── public/         # Static files
│   ├── src/
│   │   ├── pages/      # Sahifalar
│   │   ├── api.js      # API so'rovlar
│   │   └── App.jsx     # Asosiy komponent
│   └── package.json
└── BOYGI_loyihasi.md   # Hujjat
```

## 🔧 Texnologiyalar

**Backend:**
- NestJS 11
- TypeScript
- TypeORM
- SQLite (ma'lumotlar bazasi)
- Express platform

**Frontend:**
- React 18
- Vite
- React Router DOM
- Axios

## 📝 API Endpoints

### Authentication
- `POST /auth/login` - Login
- `POST /auth/register` - Registration
- `GET /auth/users` - Barcha foydalanuvchilar
- `POST /auth/init-demo` - Demo foydalanuvchilarni yaratish

### Students
- `GET /students` - Talabalar ro'yxati
- `POST /students` - Yangi talaba qo'shish
- `PUT /students/:id` - Talabani tahrirlash
- `DELETE /students/:id` - Talabani o'chirish

### Teachers
- `GET /teachers` - O'qituvchilar ro'yxati
- `POST /teachers` - Yangi o'qituvchi qo'shish
- `PUT /teachers/:id` - O'qituvchini tahrirlash
- `DELETE /teachers/:id` - O'qituvchini o'chirish

### Courses
- `GET /courses` - Kurslar ro'yxati
- `POST /courses` - Yangi kurs qo'shish
- `PUT /courses/:id` - Kursni tahrirlash
- `DELETE /courses/:id` - Kursni o'chirish

### Payments
- `GET /payments` - To'lovlar ro'yxati
- `POST /payments` - Yangi to'lov qo'shish
- `PUT /payments/:id` - To'lovni tahrirlash
- `DELETE /payments/:id` - To'lovni o'chirish

### Attendance
- `GET /attendance` - Davomat ro'yxati
- `POST /attendance` - Yangi davomat qo'shish
- `DELETE /attendance/:id` - Davomatni o'chirish

## 🖼️ Rasm Qo'shish

Agar sidebar va login sahifasi uchun logo qo'shmoqchi bo'lsangiz:

**Sidebar Logo:**
- Fayl nomi: `logo.png`
- Joylashuv: `frontend/public/logo.png`
- O'lchami: 50x50 piksel (tavsiya etiladi)

**Login Emblem:**
- Fayl nomi: `emblem.png`
- Joylashuv: `frontend/public/emblem.png`
- O'lchami: 80x80 piksel (tavsiya etiladi)

Rasmlar qo'yilmasa, avtomatik ravishda emoji ko'rinadi.

## 💡 Xususiyatlar
- ✅ Zamonaviy va qulay interfeys
- ✅ Tezkor va ishonchli backend
- ✅ Responsive dizayn (mobil qurilmalar uchun ham mos)
- ✅ O'zbek tilida interfeys
- ✅ Real-time statistika
- ✅ SQLite ma'lumotlar bazasi
- ✅ CRUD operatsiyalari to'liq amalga oshirilgan

## 🎯 Keyingi Rivojlantirish
- [ ] Reyting tizimini qo'shish
- [ ] SMS integratsiya
- [ ] Email xabarnomalar
- [ ] Export to CSV/PDF
- [ ] Mobile ilova
- [ ] Online to'lov integratsiya

## 📞 Aloqa
Loyiha ochiq kodli va bepul foydalanish uchun.

---
**Yaratilgan sana:** 28 Mart, 2026
**Versiya:** 1.0.0
