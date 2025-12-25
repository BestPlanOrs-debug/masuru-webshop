# Masuru Candle Webshop - Telepítési Útmutató

## 📁 A csomag tartalma

```
masuru-webshop/
├── index.html          # A teljes weboldal
├── admin.html          # 🔒 Rejtett admin felület
├── TELEPITES.md        # Ez a fájl
└── images/             # Termékképek
    ├── IMG_5051.jpg    # Karácsonyi Álom
    ├── IMG_5052.jpg    # Karácsonyfa
    ├── IMG_5053.jpg    # Halloween
    ├── IMG_5054.jpg    # Őszi Tökök
    ├── IMG_5055.jpg    # Őszi Harmónia
    ├── IMG_5056.jpg    # Teknős Kert
    ├── IMG_5057.jpg    # Zen Kert
    ├── IMG_5058.jpg    # Buddha Kert
    └── timi.jpg        # Bemutatkozó fotó
```

---

## 🔐 ADMIN FELÜLET

### Belépés

1. Nyisd meg: `https://te-domain.hu/admin.html`
2. Jelszó: `masuru2024`

⚠️ **FONTOS:** Változtasd meg a jelszót! Nyisd meg az `admin.html` fájlt, és keresd meg:
```javascript
const ADMIN_PASSWORD = 'masuru2024';
```
Írd át a saját jelszavadra!

### Admin funkciók

| Funkció | Leírás |
|---------|--------|
| ➕ Új termék | Kép feltöltés, név, ár, leírás, badge |
| ✏️ Szerkesztés | Meglévő termék módosítása |
| 🗑️ Törlés | Termék eltávolítása |
| 📤 Exportálás | Adatok mentése JSON fájlba |
| 📥 Importálás | Adatok visszatöltése JSON-ból |
| 🔄 Szinkronizálás | Kód generálás a webshophoz |

### Hogyan működik?

Az admin felület a böngésző **localStorage**-ját használja. Ez azt jelenti:
- A módosítások azonnal megjelennek a webshopon (ugyanazon a gépen/böngészőben)
- Ha más gépen nyitod meg, ott az alapértelmezett termékek lesznek
- **Exportáld rendszeresen az adatokat** biztonsági mentésként!

### Képfeltöltés

**1. lehetőség:** Fájl feltöltés
- Kattints a képterületre
- Válassz képet (max 2MB)
- A kép base64 formátumban tárolódik

**2. lehetőség:** URL megadás
- Írd be a kép URL-jét
- Pl: `https://example.com/image.jpg`
- Ajánlott külső képtárhelyekhez

---

## 🚀 Ingyenes Hosting Lehetőségek

### 1. Netlify (Legegyszerűbb) ⭐ AJÁNLOTT

1. Menj a [netlify.com](https://netlify.com) oldalra
2. Regisztrálj (ingyenes)
3. Húzd be a `masuru-webshop` mappát a "Drag and drop" mezőbe
4. Kész! Kapsz egy linket, pl: `masuru-candle.netlify.app`
5. Később saját domain-t is beállíthatsz (masuru.hu)

**Előny:** Automatikusan HTTPS, gyors, egyszerű

### 2. GitHub Pages (Ingyenes)

1. Regisztrálj a [github.com](https://github.com) oldalon
2. Hozz létre egy új repository-t (pl. `masuru-webshop`)
3. Töltsd fel a fájlokat
4. Settings → Pages → Source: main branch
5. Kapsz egy linket: `username.github.io/masuru-webshop`

### 3. Vercel (Ingyenes)

1. Menj a [vercel.com](https://vercel.com) oldalra
2. Regisztrálj GitHub-bal
3. "New Project" → Import Git Repository
4. Kész!

---

## 💳 Fizetés Beállítása (Stripe)

### 1. lépés: Stripe regisztráció

1. Menj a [stripe.com](https://stripe.com) oldalra
2. Regisztrálj és add meg a cégadatokat
3. Aktiváld a fiókot (bankkártya szükséges a kifizetésekhez)

### 2. lépés: Payment Link létrehozása

1. Stripe Dashboard → Products → Add Product
2. Add meg minden terméket:
   - Név: "Karácsonyi Álom"
   - Ár: 5900 Ft
   - One-time payment
3. Product → "Create payment link"
4. Máskold ki a linket (pl: `https://buy.stripe.com/abc123`)

### 3. lépés: Weboldal frissítése

Keresd meg az `index.html`-ben ezt a részt:

```javascript
// Option 1: Email
window.location.href = `mailto:hello@masuru.hu...

// Option 2: When you have Stripe Payment Link, use:
// window.location.href = 'https://buy.stripe.com/YOUR_PAYMENT_LINK';
```

Cseréld ki erre:

```javascript
window.location.href = 'https://buy.stripe.com/YOUR_ACTUAL_LINK';
```

### Stripe Költségek

- Nincs havi díj!
- EU kártyák: 1.4% + 0.25€ / tranzakció
- Nem-EU kártyák: 2.9% + 0.25€ / tranzakció

---

## 🌐 Saját Domain (masuru.hu)

### Domain vásárlás

- [domain.hu](https://domain.hu) - ~3.000 Ft/év .hu domain
- [namecheap.com](https://namecheap.com) - ~$10/év .com domain

### Domain beállítása Netlify-on

1. Netlify Dashboard → Domain settings
2. Add custom domain → `masuru.hu`
3. Kövesd az utasításokat (DNS rekordok átirányítása)
4. ~24 óra alatt működik

---

## ✏️ Termékek Módosítása

A termékek a `index.html` fájlban találhatók, a `products` tömbben:

```javascript
const products = [
    {
        id: 1,
        name: "Karácsonyi Álom",
        desc: "Téli varázslat havas fenyőfákkal...",
        price: 5900,
        image: "images/IMG_5051.jpg",
        badge: "Szezonális"  // vagy null, ha nincs badge
    },
    // ... további termékek
];
```

### Új termék hozzáadása:

1. Tedd be a képet az `images/` mappába
2. Add hozzá a terméket a `products` tömbhöz
3. Töltsd fel újra a Netlify-ra (húzd be újra)

### Ár módosítása:

Csak írd át a `price` értéket (Forintban, pont és vessző nélkül)

---

## 📱 Tesztelés

A weboldal automatikusan:
- ✅ Mobilbarát (responsive)
- ✅ Kosár működik (localStorage-ban tárolódik)
- ✅ HTTPS (Netlify automatikusan)
- ✅ Gyors (nincs szerver, statikus)

---

## 📞 Teendők összefoglaló

1. ☐ Feltöltés Netlify-ra
2. ☐ Domain vásárlás (masuru.hu)
3. ☐ Domain beállítás
4. ☐ Stripe regisztráció
5. ☐ Payment Links létrehozás
6. ☐ Weboldal frissítése Stripe linkekkel
7. ☐ Email beállítás (hello@masuru.hu)

---

## 🆘 Segítség

Ha elakadsz, keress meg bátran!

**Költség összesítő:**
- Hosting: 0 Ft (Netlify)
- Domain: ~4.000 Ft/év
- Fizetés: ~1.5% + 70 Ft / vásárlás

**Összesen induláshoz: ~4.000 Ft/év** 🎉
