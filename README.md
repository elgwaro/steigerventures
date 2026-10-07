# Steiger Ventures LTD website (v1)

This is a static four-page website for **Steiger Ventures LTD**, a Nairobi project management and project financing consultancy. The design is modelled on iOS and Apple product pages and uses the brand colours from the company profile.

**Pages:** Home · Services · Portfolio · Contact
**Tech:** plain HTML, CSS and JavaScript. There's no build step, no framework and no database.

---

## Folder structure

```
steiger-site/
├── index.html          Home
├── services.html       Services
├── portfolio.html      Portfolio (case studies)
├── contact.html        Contact (form, map, FAQ)
├── assets/
│   ├── css/styles.css  All styles (design tokens at the top)
│   ├── js/main.js      Menu, scroll animations, counters, tabs, form
│   └── img/            Logo variants, favicon, photos
├── DESIGN.md           Design system and Elementor build guide
└── README.md           This file
```

Every link is **relative**, so the site works in any folder: the domain root, a subfolder like `/demo/steiger/`, or opened straight from your computer.

---

## Preview locally

- **Quickest:** double-click `index.html`. Everything works except the embedded Google Map, which some browsers block on `file://`.
- **Local server (recommended):**
  ```bash
  cd steiger-site
  python3 -m http.server 8080
  # open http://localhost:8080
  ```

---

## Upload to your server

### Option A: cPanel File Manager
1. Log in to cPanel and open **File Manager**.
2. Go to `public_html` (or a subfolder such as `public_html/steiger`).
3. Click **Upload** and choose `steiger-site-v1.zip`.
4. Right-click the zip, choose **Extract**, then move the *contents* of `steiger-site/` into the target folder.
5. Visit `https://yourdomain.com/` (or `/steiger/`).

### Option B: FTP (FileZilla)
1. Connect with your FTP details.
2. Drag the **contents** of `steiger-site/` (the HTML files and the `assets` folder) into `public_html/` or a subfolder.

### Option C: free instant hosting for a client demo
Drag the `steiger-site` folder onto **Netlify Drop** (app.netlify.com/drop) to get a live URL within seconds.

> Keep the `assets/` folder next to the HTML files. The site breaks if they get separated.

---

## What works out of the box

| Feature | Status |
|---|---|
| Navigation between all 4 pages, with the active page highlighted | ✅ |
| In-page links (e.g. Home → *Services › Project Financing*) | ✅ |
| Mobile menu (burger opens a full-screen sheet) | ✅ |
| Click-to-call `tel:` and click-to-email `mailto:` links | ✅ |
| WhatsApp chat link (`wa.me/254729470803`) | ✅ |
| Google Map embed and "Get directions" link | ✅ (needs internet) |
| Animated counters, scroll fade-ins, segmented tabs, FAQ accordion | ✅ |
| Contact form | ✅ Opens the visitor's email app with the enquiry pre-filled and addressed to `info@steigerventures.com` |

### About the contact form
A static site can't send email by itself, so the form opens the visitor's own email app with every field already filled in. That works on any host with no setup. To have enquiries arrive in your inbox automatically instead:

- **Static hosting:** sign up at Formspree or Web3Forms, then in `contact.html` change `<form id="contact-form" ...>` to `<form action="https://formspree.io/f/YOUR_ID" method="POST">` and remove the `id` so the JS handler doesn't run.
- **WordPress:** use WPForms Lite or Contact Form 7 (see below).

---

## Quick edits

| To change | Edit |
|---|---|
| Brand colours | `assets/css/styles.css`, the `:root` tokens at the top |
| Phone, email, address | Search and replace in the four HTML files (they appear in the header, footer and contact page) |
| Contact form recipient | `data-email="info@steigerventures.com"` in `contact.html` |
| Stats numbers | The `data-count` attributes on `index.html` and `portfolio.html` (the number in the tag is the no-JS fallback) |
| Images | Replace files in `assets/img/` and keep the same names |

---

## Rebuilding in WordPress + Elementor (free)

Every section was designed to be rebuilt with **Elementor free** widgets. **DESIGN.md §5** maps each component to its widget. In short:

1. **Install:** the *Hello Elementor* theme (or Astra), *Elementor*, and *WPForms Lite* for the contact form.
2. **Global settings:** in *Elementor → Site Settings*, add the colours and the Inter font from DESIGN.md §2–3, and set Content Width to 1180px.
3. **Pages:** create Home, Services, Portfolio and Contact. Set Home as the front page in *Settings → Reading*.
4. **Menu:** in *Appearance → Menus*, add the four pages to the header menu.
5. **Build the sections** top to bottom using DESIGN.md §6. Use *Motion Effects → Fade In Up* for the scroll animations.
6. **Frosted header:** add this CSS in *Appearance → Customize → Additional CSS*:
   ```css
   .site-header { position: sticky; top: 0; z-index: 99;
     background: rgba(251,251,253,.72);
     -webkit-backdrop-filter: saturate(180%) blur(20px);
     backdrop-filter: saturate(180%) blur(20px); }
   ```
7. **Shortcut:** to copy the exact styling, paste sections of `styles.css` into *Additional CSS* and add the same class names (e.g. `card`, `btn-primary`) under each widget's *Advanced → CSS Classes*.

---

## Browser support
Latest Chrome, Safari (macOS and iOS), Edge and Firefox. Older browsers without `backdrop-filter` get a solid header instead of the frosted one.

## Credits
The content and photography come from the Steiger Ventures *Project Financing Profile* and the supplied company screenshots. The font is Inter (SIL Open Font License) via Google Fonts, and the icons are custom inline SVG.
