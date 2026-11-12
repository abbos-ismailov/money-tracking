# Pul hisobi: Vercel + Firebase

Kirim-chiqim, doimiy amallar va qarzlarni hisoblaydigan ilova. Maʼlumotlar Google hisobingiz bilan bogʻlanadi va telefon bilan kompyuterda bir xil koʻrinadi.

Firebase loyihasi: **money-tracking-c004b** (`firebaseConfig` `index.html` ichiga joylangan).

## Papka tarkibi

| Fayl | Vazifasi |
|---|---|
| `index.html` | Butun ilova (yagona fayl) |
| `firestore.rules` | Firestore xavfsizlik qoidasi (pastda matni ham bor) |
| `README.md` | Shu qoʻllanma |

## 1. Firebase sozlamalari

1. **Authentication**: Get started, Sign-in method, **Google**, Enable, email tanlang, Save.
2. **Firestore Database**: yaratilgan boʻlishi kerak (Production mode).
3. Firestore, **Rules** tabi: eski matnni oʻchirib, quyidagini qoʻying va **Publish** bosing:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

Bu qoida har kimga faqat oʻz maʼlumotini oʻqish va yozishga ruxsat beradi.

## 2. Vercel ga joylash

### A) Terminal orqali (tez)
1. `index.html` ni alohida papkaga qoʻying (masalan `pul-hisobi`).
2. Node.js oʻrnatilgan boʻlishi kerak. Terminalda:
   ```
   npm i -g vercel
   cd pul-hisobi
   vercel --prod
   ```
3. Savollarga Enter bosib javob bering. Oxirida `https://....vercel.app` manzil chiqadi.

### B) GitHub orqali
1. GitHub da yangi repo oching, `index.html` ni yuklang.
2. vercel.com/new, repoyni tanlang, **Framework Preset: Other**, Deploy.

Keyingi oʻzgarishlarda faylni yangilab, A usulida yana `vercel --prod`, B usulida repoga yuklash kifoya.

## 3. Domenni Firebase da ruxsat berish (majburiy)

Firebase, **Authentication, Settings, Authorized domains, Add domain**: Vercel manzilingizni qoʻshing (masalan `pul-hisobi.vercel.app`, `https://` siz).

Qoʻshmasangiz, Google bilan kirish xato beradi.

## 4. Eski maʼlumotlarni koʻchirish

1. Claude ichidagi eski ilovada Bosh sahifa pastiga tushing, **Zaxira nusxa va tiklash** ni oching va **Nusxalash** ni bosing.
2. Yangi saytga Google bilan kiring, shu boʻlimni oching.
3. Matnni **Tiklash** maydoniga qoʻying, **Tiklash** tugmasini ikki marta bosing (ikkinchisi tasdiqlash).

Tiklash hozirgi maʼlumotlarni almashtiradi.

## 5. Kundalik foydalanish

- Telefonda: saytni oching, brauzer menyusidan **Bosh ekranga qoʻshish** ni tanlang. Ilova belgisi paydo boʻladi.
- Chiqish: Bosh sahifa pastidagi **Chiqish** tugmasi.
- Internet boʻlmasa ham ishlaydi, ulanganda maʼlumotlar oʻzi yuboriladi.
- Ikki qurilmada bir vaqtda internetsiz oʻzgartirsangiz, oxirgi saqlangani yutadi.
- Qarz ogohlantirishlari faqat ilova ochiq paytda koʻrinadi (bildirishnoma yuborilmaydi).

## Muammolar

| Belgi | Sabab va yechim |
|---|---|
| Sahifa boʻsh | Fayl nomi `index.html` ekanini tekshiring. Claude ichida koʻrsatilsa boʻsh chiqadi, bu normal |
| «Kirishda xato: auth/unauthorized-domain» | 3-qadam bajarilmagan: Vercel domenini Authorized domains ga qoʻshing |
| «Kirishda xato: auth/popup-blocked» | Brauzer oynani blokladi. Ruxsat bering yoki qayta urining |
| «Bulutga ulanishda xato: permission-denied» | Firestore Rules qoʻyilmagan yoki Publish qilinmagan |
| Kirish tugmasi ishlamaydi, xabar chiqadi | `firebaseConfig` toʻliq emas |
| Maʼlumotlar yoʻq | Boshqa Google hisobi bilan kirgansiz. Har hisobning maʼlumoti alohida |
