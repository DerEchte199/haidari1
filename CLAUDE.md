# CLAUDE.md – Boden & Stil Haidari Website

## Projektübersicht

Statische HTML/CSS-Website für **Boden & Stil Haidari**, ein Bodenleger-Betrieb aus Würzburg.
Inhaber: Mohammad Haidari · Bronnbachergasse 21, 97070 Würzburg · +49 160 5639398

**Domain:** www.bodenstil-haidari.de
**Hosting:** GitHub Pages (CNAME konfiguriert)
**Sprache:** Deutsch (de)

---

## Repository-Struktur

```
haidari1/
├── index.html          # Startseite (Homepage)
├── leistungen.html     # Leistungsübersicht (alle Services im Detail)
├── ueber-uns.html      # Über-uns-Seite
├── kontakt.html        # Kontaktseite mit Formular
├── faq.html            # FAQ – Häufig gestellte Fragen
├── impressum.html      # Impressum (§5 TMG – gesetzlich vorgeschrieben)
├── datenschutz.html    # Datenschutzerklärung (DSGVO – gesetzlich vorgeschrieben)
├── style.css           # Haupt-Stylesheet (einzige CSS-Datei)
├── CNAME               # Domain-Konfiguration für GitHub Pages
├── README.md           # Repository-Readme
└── assets/             # Bildordner
    ├── hero-bodenleger.jpg         # Hero-Hintergrundbild (Startseite)
    ├── before1.jpg – before3.jpg   # Vorher-Fotos (Referenzen)
    ├── after1.jpg – after3.jpg     # Nachher-Fotos (Referenzen)
    ├── logo.jpg                    # Firmenlogo
    ├── ueber-uns-innenraum.jpg     # Hintergrundbild Über-uns / Innen-Seiten
    ├── kontakt-atmosphaere.jpg     # Hintergrundbild Kontakt-Sektion
    ├── hintergrund-holz-textur.jpg # Holztextur für Sektionen
    └── section-divider-textur.jpg  # Trennleisten-Textur
```

---

## Technologie-Stack

- **Nur HTML5 + CSS3** – kein Framework, kein Build-Tool, kein npm
- **Minimal JavaScript** – nur für das mobile Hamburger-Menü (IIFE, kein Framework)
- **Google Fonts** – Inter (400/500/600/700/800/900) via CDN-Link in jedem `<head>`
- **Keine Cookies, kein Tracking, kein Analytics** – bewusste Design-Entscheidung (DSGVO-konform)
- **Deployment:** GitHub Pages via `main`-Branch und CNAME-Datei

---

## Design-System (style.css)

### CSS-Variablen (`:root`)

```css
--bg:        #F5EDE3   /* Warmes Creme – Haupthintergrund */
--alt:       #EAD9C9   /* Leicht dunkleres Beige – Wechselsektionen */
--card:      rgba(255,255,255,.92)  /* Karten-Hintergrund */
--text:      #2B1A0F   /* Dunkles Braun – Fließtext */
--muted:     rgba(43,26,15,.66)     /* Gedämpfter Text */
--line:      rgba(43,26,15,.12)     /* Trennlinien / Rahmen */
--brown:     #6B3F1D   /* Primärfarbe – Buttons, Links, Highlights */
--brownDark: #3D2210   /* Dunkles Braun – Footer, Hero-Gradient */
--accent:    #C4822A   /* Goldener Akzent (für zukünftige Nutzung) */

--radius:    16px       /* Standard-Abrundung */
--radius-sm: 10px       /* Kleinere Abrundung (Buttons, Inputs) */
--shadow:    0 4px 24px rgba(0,0,0,.08)
--shadow-lg: 0 12px 40px rgba(0,0,0,.15)

--font: 'Inter', -apple-system, BlinkMacSystemFont, ...
```

### Wichtige CSS-Klassen

| Klasse | Beschreibung |
|---|---|
| `.container` | Zentrierter Inhaltsbereich, max. 1200px, 92vw auf kleinen Bildschirmen |
| `.section` | Standard-Sektion (80px padding) |
| `.section-sm` | Kompaktere Sektion (48px padding) |
| `.section-alt` | Wechselhintergrund (var(--alt)) |
| `.section-texture` | Holztextur-Hintergrund (semi-transparent) |
| `.section-dark` | Dunkelbrauner Hintergrund mit weißem Text |
| `.cards` | CSS Grid, 4 Spalten (responsive auf 2 und 1) |
| `.cards-3` | CSS Grid, 3 Spalten (responsive) |
| `.cards-2` | CSS Grid, 2 Spalten (responsive) |
| `.card` | Weiße Karte mit Schatten + Hover-Effekt |
| `.service-detail-card` | Größere Karte für Leistungsseite |
| `.btn` | Primärer Button (braun) |
| `.btn-ghost` | Transparenter Button (für dunkle Hintergründe) |
| `.btn-outline` | Outline-Button (braun auf hell) |
| `.page-hero` | Hero für Unterseiten (dunkelbrauner Hintergrund) |
| `.highlight-box` | Dunkelbrauner CTA-Block mit Gradient |
| `.faq-item` | `<details>`-Element mit CSS-Animation |
| `.contact-page-grid` | 2-Spalten-Grid für Kontaktseite (Form + Sidebar) |
| `.contact-sidebar` | Braune Sidebar auf der Kontaktseite |
| `.footer` | Dunkler Footer mit 3-Spalten-Grid |
| `.wa-float` | Fixierter WhatsApp-Button (grün, unten rechts) |

### Breakpoints

```
max-width: 1024px  → Footer 2-Spalten, Kontakt-Grid 1-Spaltig
max-width: 768px   → 2er Karten-Grid, Hamburger-Menü sichtbar
max-width: 580px   → 1er Karten-Grid, vertikale Hero-Buttons, 2er Stats
```

---

## Seitenstruktur / Navigation

### Navigation auf jeder Seite

```html
Start | Leistungen | Über uns | FAQ | [Kontakt] (CTA)
```

- Die aktive Seite bekommt `class="active"` auf dem entsprechenden `<a>`.
- Der Kontakt-Link hat immer `class="nav-cta"`.
- Mobile: Hamburger-Button (`#navBurger`) togglet `.nav-open` auf `#mainNav`.

### Footer auf jeder Seite

Drei Spalten:
1. **Marke + Kurzbeschreibung**
2. **Navigation** (alle Seiten)
3. **Kontakt** (Tel, E-Mail, Adresse) oder **Rechtliches** (Impressum, Datenschutz)

Footer-Bottom-Leiste: Copyright + Links zu Impressum & Datenschutz.

---

## JavaScript (Mobile Menü)

Jede Seite enthält am Ende des `<body>` dieses minimale Script-Snippet:

```javascript
(function () {
  var burger = document.getElementById('navBurger');
  var nav = document.getElementById('mainNav');
  var overlay = document.getElementById('navOverlay');
  function close() {
    nav.classList.remove('nav-open');
    overlay.classList.remove('show');
    burger.setAttribute('aria-expanded', 'false');
  }
  burger.addEventListener('click', function () {
    var open = nav.classList.toggle('nav-open');
    overlay.classList.toggle('show', open);
    burger.setAttribute('aria-expanded', open);
  });
  overlay.addEventListener('click', close);
  document.addEventListener('keydown', function (e) {
    if (e.key === 'Escape') close();
  });
})();
```

Das Script erfordert diese HTML-Elemente: `#navBurger`, `#mainNav`, `#navOverlay`.

---

## Neue Seite hinzufügen

1. Bestehende Seite als Vorlage kopieren (z.B. `faq.html`)
2. `<title>`, `<meta name="description">` anpassen
3. Im `<nav>` die aktive Seite mit `class="active"` markieren
4. `.page-hero` anpassen (Hintergrundbild, Überschrift, Untertitel)
5. Inhalt in `<main>` einfügen (CSS-Klassen aus dem Design-System nutzen)
6. Footer unverändert lassen (nur Nav-aktiv-State anpassen)
7. Link in ALLEN anderen Seiten zur Navigation hinzufügen

---

## Bilder (assets/)

- Alle Bilder sind **JPG**, einige sehr groß (1–5 MB).
- Bilder sollten für Web optimiert werden (< 400 KB empfohlen).
- `loading="lazy"` ist bei allen Bildern unterhalb des sichtbaren Bereichs gesetzt.
- Hero-Bilder haben kein `loading="lazy"` (werden sofort gebraucht).
- Alt-Texte sind auf Deutsch und beschreibend.

---

## Rechtliche Pflichtseiten

| Seite | Rechtsgrundlage | Pflicht |
|---|---|---|
| `impressum.html` | § 5 TMG | **Ja – gesetzlich vorgeschrieben** |
| `datenschutz.html` | DSGVO Art. 13/14 | **Ja – gesetzlich vorgeschrieben** |

Beide Seiten haben `<meta name="robots" content="noindex,follow">`.

**Zuständige Datenschutzbehörde:** Bayerisches Landesamt für Datenschutzaufsicht (BayLDA), Ansbach.

---

## Kontaktdaten (für Inhalte)

```
Betrieb:    Boden & Stil Haidari
Inhaber:    Mohammad Haidari
Adresse:    Bronnbachergasse 21, 97070 Würzburg
Telefon:    +49 160 5639398
WhatsApp:   https://wa.me/491605639398
E-Mail:     support@bodenstil-haidari.de
Servicegebiet: Würzburg + 50 km Umgebung
```

---

## Entwicklungs-Workflow

Da kein Build-System vorhanden ist:

1. HTML/CSS direkt bearbeiten
2. Im Browser testen (kein Server nötig, `file://` funktioniert)
3. Per Git committen und auf GitHub pushen → GitHub Pages deployed automatisch

**Branch-Strategie:** Entwicklung auf Feature-Branches, Merge in `main` = Live-Deployment.

---

## Konventionen

- **HTML-Entities** für Sonderzeichen: `&amp;` statt `&`, `&nbsp;` wenn nötig
- **Semantic HTML5**: `<main>`, `<header>`, `<footer>`, `<nav>`, `<section>`, `<article>`, `<aside>`, `<figure>`, `<figcaption>`
- **Barrierefreiheit**: `aria-label`, `aria-expanded`, `aria-controls`, Skip-Link auf jeder Seite, `alt`-Texte auf allen Bildern
- **Kein Inline-CSS** außer für einmalige Ausnahmen (z.B. Hintergrundbild-URL in `style=""`-Attribut)
- **Kein externes JavaScript** – kein jQuery, kein Framework
- **Google Fonts** per `<link>` im `<head>` mit `preconnect`-Optimierung
- **Floatender WhatsApp-Button** (`class="wa-float"`) auf allen Seiten außer ggf. Datenschutz/Impressum
