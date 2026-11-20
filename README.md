# RADARBEK server — Render uchun tayyor

## 1) GitHub orqali joylash
1. ZIP faylni telefoningizga yuklab, oching.
2. https://github.com saytiga kiring va hisob yarating/kiring.
3. `New repository` → nomini `radarbek-server` deb yozing → `Create repository`.
4. `Add file` → `Upload files` orqali ZIP ichidagi FAYLLARNI (ZIPning o‘zini emas) yuklang. `render.yaml`, `server.js`, `package.json`, `index.html`, `radars.json` va `.gitignore` hammasi repo ildizida tursin.
5. `Commit changes` ni bosing.

## 2) Render serverini yaratish
1. https://render.com saytiga kiring va GitHub bilan ro‘yxatdan o‘ting.
2. Dashboard → `New` → `Blueprint` (yoki repo uchun `New` → `Web Service`) ni tanlang.
3. `radarbek-server` repozitoriyasini ulang. `render.yaml` avtomatik sozlamalarni beradi.
4. `ADMIN_KEY` uchun kamida 32 belgili tasodifiy maxfiy kalit yarating va Render Environment bo‘limiga kiriting. Uni hech kimga yubormang va chatga yozmang.
5. Deploy tugashini kuting. Render sizga `https://...onrender.com` manzil beradi.
6. Tekshirish: brauzerda `https://SIZNING-MANZILINGIZ/api/health` oching. `{"ok":true,"app":"RADARBEK"}` chiqishi kerak.

## 3) Muhim
- Hozircha free Render serveri sinov uchun: 15 daqiqa so‘rov bo‘lmasa uxlaydi va fayl tizimi doimiy emas. `radars.json` ga kiritilgan o‘zgarishlar restart/deploydan keyin yo‘qolishi mumkin. Haqiqiy foydalanishdan oldin PostgreSQL bazasini ulash zarur.
- Radar koordinatalari hozir bo‘sh. Faqat tekshirilgan va qonuniy ravishda foydalanish mumkin bo‘lgan radar ma’lumotlarini admin qo‘shishi kerak.
- Premium to‘lovlari hali faol emas. Click/Payme merchant hisob, webhook imzo tekshiruvi va serverdagi obuna nazorati kerak. Foydalanuvchi pulini hozircha qabul qilmang.
- GPS brauzerda odatda HTTPS talab qiladi; Render URL HTTPS bo‘ladi.
- OSM xarita qatlamidan foydalanishda tile server siyosatiga rioya qiling.

## API
- `GET /api/health` — server holati
- `GET /api/radars` — faol radarlar
- `POST /api/radars` — radar qo‘shish; `x-admin-key` sarlavhasi kerak
- `DELETE /api/radars/:id` — radar o‘chirish; `x-admin-key` kerak

Radar qo‘shish namuna:
```bash
curl -X POST https://SIZNING-MANZILINGIZ/api/radars \
 -H 'Content-Type: application/json' \
 -H 'x-admin-key: ADMIN_KALIT' \
 -d '{"name":"Tekshirilgan radar","lat":41.3111,"lng":69.2797,"speedLimit":60}'
```
