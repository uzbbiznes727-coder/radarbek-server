# RADARBEK — boshlang‘ich loyiha

## Fayllar
- `index.html` — mobil web ilova
- `server.js` — Node.js/Express custom API
- `radars.json` — radarlar bazasi (hozircha bo‘sh)

## Ishga tushirish
Node.js 18+ o‘rnating, loyiha papkasida:
```bash
npm install
# Linux/macOS:
ADMIN_KEY='uzun-maxfiy-kalit' npm start
# Windows PowerShell:
$env:ADMIN_KEY='uzun-maxfiy-kalit'; npm start
```
Brauzerda `http://localhost:3000` ni oching. Telefon GPS uchun HTTPS kerak (localhost istisno); internetga joylaganda HTTPS domen ishlating.

## Radar qo‘shish (administrator)
```bash
curl -X POST http://localhost:3000/api/radars \
 -H 'Content-Type: application/json' \
 -H 'x-admin-key: SIZNING_MAXFIY_KALITINGIZ' \
 -d '{"name":"Tekshirilgan radar","lat":41.3111,"lng":69.2797,"speedLimit":60}'
```
Yangi radarlar `verified:false` sifatida saqlanadi. Joylashuv va limitni rasmiy/ishonchli manbadan tekshirmasdan ommaga chiqarmang.

## Hozirgi bosqich chegaralari
- Radarlar bazasi bo‘sh; ilova o‘zi radarlarni avtomatik topmaydi. Admin tasdiqlangan koordinatalarni kiritishi yoki litsenziyali ma’lumot manbai ulanishi kerak.
- Uchta bepul ogohlantirish va Premium UI hozircha interfeys ko‘rinishi. Ishonchli obuna uchun serverdagi foydalanuvchi hisobi, ma’lumotlar bazasi, Click/Payme merchant shartnomasi, payment webhook imzo tekshiruvi va Google Play Billing (APK bo‘lsa) kerak. Brauzer localStorage bilan to‘lovni himoyalab bo‘lmaydi.
- 100 m/10 m ogohlantirishlari GPS joylashuvi va aniqligiga bog‘liq; 10 m aniqlik kafolatlanmaydi. Telefon qulflanganda fon GPS uchun keyinchalik native Android ilova/PWA imkoniyatlari kerak bo‘lishi mumkin.
- OSM standart tile serveri sinov va kam trafik uchun; ishlab chiqarishda tile siyosatiga mos tijoriy yoki o‘z tile hostingini tanlang. Manba: https://operations.osmfoundation.org/policies/tiles/
- Xarita Leaflet kutubxonasida qurilgan: https://leafletjs.com/examples/quick-start/
