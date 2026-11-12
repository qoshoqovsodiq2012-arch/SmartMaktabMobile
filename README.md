# SmartMaktab Mobile

Boshlang'ich ishlaydigan Android loyiha manbasi:
- `mobile/` — Flutter Android ilovasi
- `backend/` — FastAPI + SQLite REST API
- `admin/README.md` — admin panelni keyingi bosqichda kengaytirish bo'yicha yo'riqnoma
- `.github/workflows/build-android.yml` — GitHub Actions orqali APK yig'ish

## Muhim
Bu ZIP — loyiha manba kodi, tayyor APK emas. APK yig'ish uchun Flutter SDK va Android SDK kerak.
Ilova muammolarni backendga yuboradi. Backendni kompyuterda ishga tushirib, telefon bilan bir Wi-Fi tarmog'ida sinash mumkin.

## 1. Backendni ishga tushirish (Windows)
```powershell
cd backend
py -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```
API hujjatlari: `http://127.0.0.1:8000/docs`

Telefon emulatorida API manzili `http://10.0.2.2:8000`.
Haqiqiy telefonda kompyuterning LAN IP manzilini ishlating, masalan `http://192.168.1.10:8000`.
Render yoki boshqa hostingga joylaganda HTTPS manzilini kiriting.

## 2. Flutter ilova
Flutter SDK o'rnatilgach:
```powershell
cd mobile
flutter create . --platforms=android
flutter pub get
flutter run
```
`lib/main.dart` dagi `apiBaseUrl` qiymatini backend manzilingizga moslang.
APK:
```powershell
flutter build apk --release
```
APK manzili: `build/app/outputs/flutter-apk/app-release.apk`

## 3. GitHub Actions
Loyihani GitHub repozitoriyasiga joylang. `main` branchga push qilinganda workflow APK yig'ishga urinadi va APKni artifact sifatida saqlaydi.

## Xavfsizlik va keyingi ishlar
Bu birinchi ishlaydigan MVP. Ommaviy ishga tushirishdan oldin quyidagilarni qo'shish shart:
- haqiqiy login/ro'yxatdan o'tish va parolni xavfsiz xeshlash;
- rollar va server tomonda ruxsat tekshiruvi;
- rasm yuklash uchun fayl turi/hajmi tekshiruvi va antivirus/saqlash siyosati;
- HTTPS, rate limiting, CSRF (web admin uchun), audit log;
- moderator tasdig'i va shaxsiy ma'lumotlarni himoyalash;
- PostgreSQL migratsiyasi va backup.

Hozircha backendda muammo yaratish va ko'rish APIlari ishlaydi. Haqiqiy foydalanuvchi akkauntlari va push-bildirishnomalar hali ulanmagan.
