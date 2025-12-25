# Masuru Webshop – GitHub + Stripe Beállítás

## 1️⃣ GITHUB FELTÖLTÉS (GitHub Desktop)

### 1. lépés: Mappa előkészítése

1. Csomagold ki a `masuru-webshop.zip` fájlt valahova, pl:
   ```
   C:\Users\[Neved]\Documents\masuru-webshop
   ```
   vagy Mac-en:
   ```
   /Users/[Neved]/Documents/masuru-webshop
   ```

2. A mappában ezeknek kell lennie:
   ```
   masuru-webshop/
   ├── index.html
   ├── admin.html
   ├── TELEPITES.md
   └── images/
       ├── IMG_5051.jpg
       ├── ... (többi kép)
       └── timi.jpg
   ```

---

### 2. lépés: GitHub repo létrehozása

1. Nyisd meg a **GitHub Desktop** appot
2. Kattints: **File → New Repository...**
3. Töltsd ki:
   - **Name:** `masuru-webshop`
   - **Local Path:** Válaszd ki a **szülőmappát** (pl. Documents)
     - ⚠️ NE a masuru-webshop mappát, hanem ami TARTALMAZZA
   - **Initialize with README:** ❌ NE pipáld be
4. Kattints: **Create Repository**

---

### 3. lépés: Fájlok hozzáadása

**Ha üres repo jött létre:**

1. Nyisd meg a Finder/Explorer-ben a repo mappáját
2. Másold be az összes fájlt a kicsomagolt `masuru-webshop` mappából
3. GitHub Desktop-ban látni fogod a változásokat

**VAGY ha már meglévő mappát akarsz hozzáadni:**

1. **File → Add Local Repository...**
2. Válaszd ki a `masuru-webshop` mappát
3. Ha kéri, kattints "create a repository" linkre

---

### 4. lépés: Commit és Push

1. GitHub Desktop bal oldalán látod a fájlokat
2. Alul írd be:
   - **Summary:** `Initial commit - Masuru webshop`
3. Kattints: **Commit to main**
4. Kattints: **Publish repository** (jobb felső sarok)
   - **Keep this code private:** Pipáld be, ha nem akarod, hogy publikus legyen
   - ⚠️ Ha GitHub Pages-t akarsz (ingyenes hosting), akkor legyen **publikus**
5. Kattints: **Publish Repository**

---

### 5. lépés: GitHub Pages bekapcsolása (INGYENES HOSTING!)

1. Menj a böngészőben: `https://github.com/[felhasználóneved]/masuru-webshop`
2. Kattints: **Settings** (fogaskerék ikon)
3. Bal oldalt kattints: **Pages**
4. **Source** résznél:
   - Branch: `main`
   - Folder: `/ (root)`
5. Kattints: **Save**
6. Várj 1-2 percet, majd frissíts
7. Megjelenik a link: `https://[felhasználóneved].github.io/masuru-webshop`

🎉 **A webshopod ONLINE!**

---

## 2️⃣ STRIPE FIZETÉS BEÁLLÍTÁSA

### 1. lépés: Stripe regisztráció

1. Menj: **https://stripe.com/hu**
2. Kattints: **Ingyenes regisztráció** vagy **Start now**
3. Add meg:
   - Email
   - Jelszó
   - Ország: Magyarország
4. Erősítsd meg az email címedet

---

### 2. lépés: Fiók aktiválása

1. Stripe Dashboard-on kattints: **Activate your account**
2. Töltsd ki az űrlapot:
   - **Vállalkozás típusa:** Egyéni vállalkozó / Magánszemély
   - **Személyes adatok:** Név, cím, születési dátum
   - **Banki adatok:** IBAN (ide érkeznek a kifizetések)
   - **Vállalkozás leírása:** "Kézzel készített gyertyák értékesítése"
3. Küldj be egy igazolványt (személyi/jogsi)
4. Várj a jóváhagyásra (általában 1-2 nap)

⚠️ **Addig is tesztelhetsz!** A Stripe "Test mode"-ban működik, amíg nincs aktiválva.

---

### 3. lépés: Termékek létrehozása a Stripe-ban

1. Stripe Dashboard → **Products** (bal menü)
2. Kattints: **+ Add product**
3. Töltsd ki minden terméknél:

| Mező | Példa |
|------|-------|
| **Name** | Karácsonyi Álom gyertya |
| **Description** | Téli varázslat havas fenyőfákkal. Fahéjas-narancs illat. |
| **Image** | Töltsd fel a termékképet |
| **Price** | 5900 HUF (One time) |

4. Kattints: **Save product**
5. Ismételd meg minden terméknél

---

### 4. lépés: Payment Links létrehozása

**Egyszerű megoldás - EGY LINK MINDEN TERMÉKHEZ:**

1. Stripe Dashboard → **Payment links** (bal menü)
2. Kattints: **+ New**
3. Válaszd ki: **Products from your catalog**
4. Pipáld be az ÖSSZES terméket
5. **Beállítások:**
   - ✅ Let customers adjust quantity
   - ✅ Collect shipping address
   - Shipping: Add hozzá a szállítási díjakat (lásd lent)
6. Kattints: **Create link**
7. Másold ki a linket, pl: `https://buy.stripe.com/abc123xyz`

**Szállítási díjak hozzáadása:**

A Payment Link szerkesztőben:
1. Kattints: **Delivery** fül
2. **+ Add shipping rate**
3. Add hozzá:
   - "GLS futár" - 1590 Ft
   - "Foxpost automata" - 1290 Ft
   - "Személyes átvétel" - 0 Ft

---

### 5. lépés: Webshop frissítése a Stripe linkkel

1. Nyisd meg az `index.html` fájlt egy szerkesztővel (Notepad++, VS Code, stb.)

2. Keresd meg ezt a részt (kb. 850. sor körül):
```javascript
// Checkout
function checkout() {
    // ... sok kód ...
    
    // Option 1: Email
    window.location.href = `mailto:hello@masuru.hu?subject=...
```

3. Cseréld ki ERRE:
```javascript
// Checkout
function checkout() {
    // Stripe Payment Link - CSERÉLD KI A SAJÁT LINKEDRE!
    window.location.href = 'https://buy.stripe.com/IDE_MASOLD_A_TE_LINKED';
}
```

4. Mentsd el a fájlt

---

### 6. lépés: Változtatások feltöltése GitHub-ra

1. Nyisd meg a **GitHub Desktop**-ot
2. Látni fogod: `index.html` - modified
3. Alul írd be:
   - **Summary:** `Add Stripe payment link`
4. Kattints: **Commit to main**
5. Kattints: **Push origin**

🎉 **1-2 perc múlva a weboldalon is működik a fizetés!**

---

## 3️⃣ ÖSSZEFOGLALÓ - ELLENŐRZŐLISTA

### GitHub
- [ ] Repo létrehozva: `masuru-webshop`
- [ ] Fájlok feltöltve (commit + push)
- [ ] GitHub Pages bekapcsolva
- [ ] Weboldal él: `https://[user].github.io/masuru-webshop`

### Stripe
- [ ] Stripe fiók regisztrálva
- [ ] Banki adatok megadva (aktiváláshoz)
- [ ] Termékek létrehozva
- [ ] Payment Link létrehozva
- [ ] Szállítási díjak beállítva
- [ ] Link beillesztve az `index.html`-be
- [ ] Változtatások push-olva

### Saját domain (opcionális)
- [ ] Domain megvásárolva (masuru.hu)
- [ ] DNS beállítva a GitHub Pages-hez

---

## 4️⃣ STRIPE KÖLTSÉGEK

| Tétel | Díj |
|-------|-----|
| Regisztráció | **0 Ft** |
| Havi díj | **0 Ft** |
| EU bankkártya | **1.4% + 0.25€** (~1.5% + 100 Ft) |
| Nem-EU kártya | **2.9% + 0.25€** |

**Példa:** 5.900 Ft-os gyertya eladása
- Stripe díj: ~190 Ft
- Te kapod: ~5.710 Ft

---

## 5️⃣ TESZTELÉS

### Test mode (amíg nincs aktiválva)

A Stripe Dashboard-on bal felül van egy **"Test mode"** kapcsoló.
Teszt bankkártyaszám: `4242 4242 4242 4242`
Lejárat: bármilyen jövőbeli dátum
CVV: bármilyen 3 számjegy

### Élesítés előtt

1. Kapcsold ki a Test mode-ot
2. Csinálj egy próbarendelést saját magadnak
3. Ellenőrizd, hogy megérkezik-e az email értesítés
4. Ellenőrizd a Stripe Dashboard-on a rendelést

---

## 6️⃣ HASZNOS LINKEK

- **Stripe Dashboard:** https://dashboard.stripe.com
- **Stripe dokumentáció:** https://stripe.com/docs
- **GitHub repo:** https://github.com/[te-neved]/masuru-webshop
- **Webshop:** https://[te-neved].github.io/masuru-webshop
- **Admin:** https://[te-neved].github.io/masuru-webshop/admin.html

---

## 🆘 GYAKORI PROBLÉMÁK

### "A GitHub Pages nem működik"
- Ellenőrizd, hogy public-e a repo
- Várj 5 percet és frissíts
- Settings → Pages → ellenőrizd a beállításokat

### "A Stripe fizetés nem indul el"
- Ellenőrizd, hogy jó linket másoltál-e be
- Nézd meg, hogy nincs-e Test mode bekapcsolva
- Ellenőrizd a böngésző konzolt (F12) hibákért

### "A képek nem jelennek meg"
- Ellenőrizd, hogy az `images/` mappa is fel van-e töltve
- A fájlnevek nagybetű-érzékenyek!

---

*Sok sikert a Masuru webshophoz! 🕯️✨*
