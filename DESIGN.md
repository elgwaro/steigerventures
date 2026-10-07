# Steiger Ventures website: Design System (v1)

This file covers the visual language of the Steiger Ventures LTD website and how to rebuild every section in **WordPress + Elementor (free)**. All the content comes from the company's *Project Financing Profile* and the supplied screenshots.

---

## 1. Design direction

**"Apple-calm, Steiger-blue."** The site borrows the UX patterns people already know from iOS and Apple product pages:

| Apple / iOS pattern | How it appears on the site |
|---|---|
| Huge, tight-tracked headlines with lots of white space | `display` / `h1` / `h2` type scale, centred section heads |
| One clear action per screen | The hero has a single primary button: **Book a free consultation** |
| Frosted-glass navigation bar | Sticky header with `backdrop-filter: blur(20px)` |
| Soft rounded cards (22–32px radius) | Service cards, bento grid, stats, case studies |
| Bento grid | Home page "What we do" section |
| iOS segmented control | Services page "Core competencies" switcher |
| Pill buttons with a press-down effect | `.btn`: fully rounded, scales to 97% on tap |
| Glass "notification" cards over imagery | Floating stat cards on the home hero image |
| Gentle fade-up on scroll | `.reveal`, which maps to Elementor's *Fade In Up* entrance animation |
| Full-screen mobile menu with large type | Mobile nav sheet below 860px |

Throughout, light sections alternate with deep-navy "statement" sections, so the page reads like a product keynote: headline, proof, next step.

---

## 2. Colour palette

Colours were sampled straight from the company profile PDF (logo, headings, page accents) and from the logo screenshots.

| Token | Hex | Source | Use |
|---|---|---|---|
| **Royal Blue** `--royal` | `#1346C7` | Logo chain in the PDF | Primary buttons, links, icon tiles, highlights |
| **Navy** `--navy` | `#153D63` | PDF section headings | Logo on light backgrounds, stat numbers, gradients |
| **Ink** `--ink` | `#0B1B2E` | Deepened navy | Dark sections, CTA banner |
| **Steel Blue** `--steel` | `#3075A4` | PDF hexagon accents | Eyebrow labels, secondary accents |
| **Sky Blue** `--sky` | `#A6CAEC` | PDF page side bars | Hero glow, accents on dark backgrounds |
| **Mist** `--mist` | `#EAF2FB` | Sky tint | Chips, soft panels, icon backgrounds |
| Background | `#FBFBFD` | Apple neutral | Page background |
| Gray | `#F5F5F7` | Apple neutral | Alternate sections, form fields, footer |
| Text | `#1D1D1F` | Apple neutral | Body and headings |
| Muted | `#6E6E73` | Apple neutral | Secondary text |

**Signature gradient** (used on headline highlights):
`linear-gradient(100deg, #153D63 0%, #1346C7 55%, #3075A4 100%)`

**Elementor:** go to *Site Settings → Global Colors* and add the colours as follows: Primary = `#1346C7`, Secondary = `#153D63`, Text = `#1D1D1F`, Accent = `#A6CAEC`. Add Ink, Steel, Mist, Gray and Muted as custom colours.

---

## 3. Typography

- **Font:** Inter (Google Fonts, weights 400/500/600/700/800). It's the closest free match to Apple's SF Pro. The font stack falls back to `-apple-system`, so Apple devices render SF if Inter fails to load.
- **Letter-spacing:** negative on headings (−0.025em to −0.045em), which gives the tight Apple look.

| Role | Size (desktop → mobile) | Weight | Tracking |
|---|---|---|---|
| Display (home hero) | 96 → 44px (`clamp`) | 800 | −0.045em |
| H1 (page heroes) | 72 → 40px | 700 | −0.04em |
| H2 (section titles) | 56 → 32px | 700 | −0.035em |
| H3 (cards) | 22–28px | 700 | −0.02em |
| Lead | 24 → 19px | 400, muted | −0.01em |
| Body | 17 → 16px | 400 | 0 |
| Eyebrow | 13px, UPPERCASE | 600, steel | +0.14em |

**Elementor:** go to *Site Settings → Global Fonts* and set Primary = Inter 800, Secondary = Inter 700, Text = Inter 400, Accent = Inter 600. In *Site Settings → Typography*, set H1–H3 sizes using the table above, with tablet and mobile values.

---

## 4. Layout and spacing

- **Container:** 1180px max width with a 22px side gutter. In *Elementor → Site Settings → Layout*, set Content Width to 1180.
- **Section padding:** 128px desktop, about 72px mobile (`clamp(72px, 10vw, 128px)`).
- **Grid gaps:** 20px between cards, 18px for stats.
- **Radii:** 14px (inputs), 22px (cards), 32px (hero image, CTA banner, large media), 999px (buttons, chips).
- **Shadows:** very soft and navy-tinted: `0 10px 30px rgba(21,61,99,.08)`.
- **Breakpoints:** these match Elementor's defaults. Tablet ≤ 1024px, mobile ≤ 767px, plus 860px for the burger menu.

---

## 5. Components → Elementor (free) widgets

Every component uses widgets that come with **Elementor free**, and nothing requires Pro.

| Component | CSS class | Elementor free build |
|---|---|---|
| Section | `.section`, `.bg-gray`, `.bg-ink` | **Container** (Flexbox) with background colour and padding |
| Eyebrow + heading + lead | `.eyebrow`, `.h2`, `.lead` | **Heading** (eyebrow, H6 styled), **Heading** (H2), **Text Editor** |
| Primary button | `.btn-primary` | **Button**: border-radius 999px, padding 0/28px, height 50px, Royal Blue background, hover `#0F3AA8` |
| Light / ghost button | `.btn-light`, `.btn-ghost` | **Button** with white background, or a transparent one with a 1px border |
| Frosted nav | `.nav` | Theme header (Hello Elementor / Astra) plus Custom CSS: `backdrop-filter: blur(20px); background: rgba(251,251,253,.72)` |
| Hero with image | `.hero`, `.hero-visual` | **Container** (column) → Heading, Text, Button, **Image** (radius 32px 32px 0 0) |
| Floating glass card | `.float-card` | **Icon Box** inside a Container set to *Position: Absolute* (Advanced tab), with a white 78% background |
| Stats | `.stat` | **Counter** widget inside white Containers (radius 22px) |
| Bento grid | `.bento` | **Grid Container** (6 columns, large tile spans 4) or nested Flex Containers at 66% and 33% width |
| Service card | `.card` | **Icon Box** widget (icon on top, left aligned) inside a Container with radius 22px and a 1px border; link set on the Container |
| Feature (dark) card | `.card.feature` | Same as the service card, with a gradient background `#0B1B2E → #153D63 → #1E5A8C` |
| Industries row | `.industries` | **Icon Box** × 6 inside a 6-column Grid Container |
| Image + text split | `.split` | 2-column Container → **Image** (radius 32px) and Heading, Text, Button |
| Chips | `.chip` | **Text Editor** with inline `<span>` tags or several small **Button** widgets (pill, Mist background) |
| Check list | `.checks` | **Icon List** widget with a check-circle icon in Royal Blue |
| Segmented control | `.segmented` | **Tabs** widget (horizontal): style the tab titles as pills, with a gray track and a white active tab |
| Process steps | `.steps` | 4-column Container → Heading ("01"), Heading, **Icon List** |
| Case study card | `.case` | **Image Box** widget, or a Container with Image, Heading and Text |
| Testimonials | `.quote` | **Testimonial** widget (free), or **Text Editor** plus Heading |
| CTA banner | `.cta-banner` | Container (radius 32px, Ink background with a radial gradient), Heading, Text, Button |
| Contact cards | `.contact-card` | **Icon Box** with links (`tel:`, `mailto:`, WhatsApp) |
| Map | `.map-card` | **Google Maps** widget (free, no API key needed) |
| FAQ | `.faq` | **Accordion** or **Toggle** widget |
| Footer | `.footer` | Theme footer, or a Container with **Image**, **Icon List** × 3 and Text |
| Scroll animation | `.reveal` | *Advanced → Motion Effects → Entrance Animation: Fade In Up* |
| Contact form | `#contact-form` | ⚠ Elementor's Form widget is Pro only. Use **WPForms Lite** or **Contact Form 7** and paste its shortcode into a **Shortcode** widget, then style it with the CSS in `styles.css` §16 |

---

## 6. Page structure

### Home (`index.html`)
1. **Hero**: "From concept to creation." with one CTA (*Book a free consultation*), plus a team image with glass stat cards
2. **Stats**: 2016 · $4.6M+ · 10 SMEs · 6 industries (animated counters)
3. **About**: building photo, the established-2016 story and industry chips
4. **What we do**: a bento grid of the five core services (Project Financing is the hero tile)
5. **Industries served**: six icon tiles
6. **Why work with us**: dark section with the vision statement and differentiators
7. **Testimonials**: three client quotes
8. **CTA banner** and footer

### Services (`services.html`)
1. Page hero: "Built for delivery. Structured for funding."
2. Six service cards (each has an anchor: `#project-management`, `#consultancy`, `#procurement`, `#agribusiness`, `#value-chain`, `#project-financing`)
3. Core competencies in a segmented control (Management / Industry / Finance)
4. The four-step Project Financing process (dark section)
5. SME and youth enterprise support
6. CTA banner

### Portfolio (`portfolio.html`)
1. Page hero: "Results that speak in numbers."
2. Three case-study cards: USD 4.5M, USD 50K, 10 × USD 5K
3. Impact stats
4. Industries served (handshake image)
5. Why clients choose us (four cards)
6. Testimonials and CTA

### Contact (`contact.html`)
1. Page hero: "Get in touch."
2. Four contact cards: Call · Email · WhatsApp · Visit
3. Consultation form and Google Map
4. Managing Director card (Steve Denis Kimani)
5. FAQ accordion

---

## 7. Imagery

All imagery comes from the client's own materials (`assets/img/`):

| File | Source | Used on |
|---|---|---|
| `team-meeting.jpg` | Profile PDF p.1 | Home hero, portfolio case |
| `growth-jar.jpg` | Profile PDF p.2 | Home "Why us", portfolio case |
| `time-value.jpg` | Profile PDF p.3 | Services tab, portfolio case |
| `tablet-plan.png` | Profile PDF p.3 | Services tab |
| `building.jpg` | Screenshot 2 | Home about |
| `handshake.jpg` | Screenshot 4 | Services tab, portfolio industries |
| `idea-bulb.jpg` | Screenshot 5 | Services SME section |
| `logo-*.png`, `mark-*.png` | Profile PDF logo, recoloured | Navigation, footer, CTA watermark, favicon |

For v2, swap in real project photos (sites, teams, signings) at **1600px wide or more**, keeping these aspect ratios: hero 16:8, split images 4:5 or 1:1, case cards 16:10.

---

## 8. Accessibility and quality

- Semantic landmarks (`header`, `nav`, `main`, `footer`), a skip link, and `aria-current` on the active page
- Body text contrast meets WCAG AA. Muted `#6E6E73` on `#FBFBFD` has a ratio of 4.9:1
- Keyboard-operable tabs (arrow keys), native `<details>` FAQ, visible focus rings
- `prefers-reduced-motion` turns off all animation
- Lazy-loaded images and no framework: one CSS file and one small JS file

---

## 9. Content notes to confirm with the client

- **Stats** are derived from the case studies in the profile. **$4.6M+** = 4.5M + 50K + 10 × 5K. **12+ businesses** = the 10 SMEs, the creative and beauty businesses, and the fleet company. Confirm these, or replace them with official totals.
- The testimonial authors have no titles or companies yet. Add these if the clients agree.
- **Email:** `info@steigerventures.com` is the main address (from the screenshot), and `steve@steigerventures.com` is listed for the MD. The profile also lists `steigerventures83@gmail.com`, which the site leaves out on purpose so it looks professional.
- Office hours on the "Call us" card say "Monday to Friday, business hours". Confirm the exact times.
