# nguyen0xhieu Design System v4 (Bento)

The reference for designing and coding every nguyen0xhieu product. **The original palette stays**, with two web densities by purpose and one consistent component set. Updated 2026-11-08: **v4 makes Bento the default web style** (next section). The v3 sections below remain correct on color, tokens and data patterns, but on surfaces, radius, type size and spacing **Bento wins**.

## Using it

1. Read this doc and `tokens.json` before designing.
2. Choose a **pattern**: editorial/landing, data table or task list.
3. Choose a profile per page/region: `spacious` or `compact`.
4. Use `web.css` exported from tokens. Don't invent colors or cut spacing arbitrarily.
5. Record approved exceptions in `products` and the product docs. A product exception takes priority only within its scope.

| File | Role |
|---|---|
| `tokens.json` | Light/Dark colors, typography, spacing, components, two profiles, product exceptions |
| `web.css` | CSS variables auto-exported from tokens (color/type/profile/product) |
| `export_web.py` | `python export_web.py` regenerates the CSS; no dependencies |
| `README.md` | Design decisions, how to choose a pattern, acceptance criteria |

In HTML: `<body data-ds-product="0xhieu-xyz" data-ds-profile="compact">`. Theme: `data-ds-theme="dark"` where supported. Profile changes by page, not just because the viewport is small.

## Bento v4: default web style (decided 2026-11-08)

Source: the 0xhieu.xyz UI approved 2026-11-07. Full tokens in `tokens.json → bento`, CSS in `web.css` (`--ds-bento-*`).

**Figma:** https://www.figma.com/design/V0GuQUwipow6yFqNi4y7qg/hieu
- Variables: `Primitives`, `Bento` (Light/Dark), `Spacing & Radius`.
- 24 functional text styles (`Mobile/…` and `Desktop/…`).
- Bento components.
- **Icons** page: 328 Lucide 1.59.0 icons shared by all products.
- **Brand** group (`Brand/x`, `Brand/discord`, `Brand/telegram`, `Brand/github`): Lucide 1.x removed brand icons, so these are drawn with the same 2 stroke as the icons on 0xhieu.xyz.

### Primitives

Only the shades the Bento semantic colors use (26): neutral 0/100/200/400/600/800/900/950/1000, red 50/300/600/950, amber 50/300/800/950, yellow 500, green 50/300/700/950, blue 50/300/600/950.
- **Code:** `--ds-palette-<family>-<shade>`, e.g. `--ds-palette-yellow-500`.
- **Figma:** collection `Primitives`. UI uses the Bento semantic colors, not primitives directly.

### Surfaces

| Item | Value | Use |
|---|---|---|
| Canvas | `#F2F2F0` | Page background. Page titles and group labels sit directly on canvas, with **no** white band. |
| Tile | `#FFFFFF` | All readable content goes in tiles. No border, no shadow. |
| Hair | `#ECECEA` | 1 px line between rows in a tile. |
| Dark tile | `#161616` | Contrast block (warning, second key block). White text, numbers in accent. |
| Accent tile | product accent | Main metric/block. Black text; buttons inside are black with accent text. |
| Chip | canvas color | Tags, chips, icon boxes, secondary buttons inside white tiles. |

- Each screen has **at most 1 accent tile and 1 dark tile**; the rest are white.
- **Tags:** important = black with white/accent text; normal = canvas with black text. No outlined tags.
- **Status:** next task = accent chip; overdue/danger = `red-soft` chip with `red-text`; done = muted strikethrough. Status color always comes with text.
- **Only 3 radii:** **20** for tiles and popups; **10** for chips, tags, logos, icon boxes, small buttons, inputs; **Pill** for navbar, tabs, toggles, counters, floating buttons, avatars.
- **Shadow:** only **floating** things get `shadow-y2`: sticky navbar, page toolbar buttons, floating buttons, popups. Tiles and links/buttons inside tiles are flat.
- **Only 3 weights:** **400** reading text; **600** labels, names, buttons, tile titles; **700** page titles and big numbers. No 500 or 800.

### Type: named by function

Every piece of text belongs to **exactly one functional style**. Code uses names only, via `--ds-type-<name>-size`, `-line`, `-weight`, `-tracking`; never hand-typed px. Each style has mobile and desktop sizes, and the variables switch at ≤640.

- **Mobile is small and airy:** clear but not shouting.
- **Desktop is large:** enough for screenshots used as banners, covers, slides.

| Style | Code name | Mobile | Desktop | Weight | Use |
|---|---|---|---|---|---|
| **Display** | `display` | 28/32 | 56/60 | 700 | Big numbers in accent/dark tiles, CV tagline, checklist counts. Max 2 per screen. |
| **Page title** | `page` | 20/26 | 32/40 | 700 | One page title per screen. |
| **Header** | `header` | 16/22 | 20/28 | 600 | Titles of tiles, boxes, dropdowns, popups; person name; job role. |
| **Content** | `content` | 14/20 | 16/24 | 400 | Main reading text: task/row text, paragraphs, list items. Names in a row use weight 600. |
| **Secondary** | `secondary` | 13/18 | 14/20 | 400 | Supporting text under content: row meta, location, stat caption, sub-lines. Grey. |
| **Data** | `data` | 13/18 | 14/20 | 400 | Table cells and numeric values in lists. tabular-nums. |
| **Label** | `label` | 12/16 | 13/18 | 600 | Tags, chips, table headers, group labels, small box labels, counters. |
| **Button** | `button` | 14/20 | 15/20 | 600 | Buttons, nav tabs, toggles, link chips. |
| **Note** | `note` | 12/16 | 13/18 | 400 | Captions, hints, helper/error text, empty states, footnotes. |
| **Input** | `input` | 16/24 | 16/24 | 400 | Form inputs and selects (16 on mobile prevents iOS zoom). |
| **Hero** | `hero` | 32/36 | 72/76 | 700 | Spacious pages only (landing, cover): one line per page. |

**Rules:**
- **Weights only 400 · 600 · 700.** 800 looks less refined.
- Project or row names use **Content** at weight 600; no new size.
- If no style fits new text, **add a style to this table**, named by function. Never hand-type px.
- All numbers use `tabular-nums`.

### Layout

- **Frame:** max width 1280, side margin 24 desktop and 16 mobile.
- **Navbar:** copy the **Web shell** spec below exactly. Don't redesign it per product.
- **Page header:** title left, controls right, directly on canvas. Controls are white pills with shadow.
- **Tool page (editor + options, e.g. Creator Hub Ảnh):** preview big on the left, sized to fit the screen; options in one sticky 320 column on the right, one 40-high row per setting (label 72 + control), hair lines between groups, no group titles or long hints. Must fit 1440×900 without scrolling. Mobile: preview first, options below.
- **Grid:** desktop 4 columns, ≤1024 2 columns, mobile 2 columns for metric and feature tiles.
  - Lists, checklists and tables take a full row.
  - Expandable tiles (`details`) take 2 columns when open, a full row on mobile.

### Web shell: copy 0xhieu.xyz (decided 2026-11-14)

**0xhieu.xyz is the reference implementation.** Every new web product (e.g. Creator Hub, hub.0xhieu.xyz) copies its shell 1:1, not "something similar". Source: `website_personal_0xhieu/index.html`, `header` / `.header-inner` / `.header-home` / `nav` / `.nav-btn`.

```
[ (photo) Name          ( [Tab on] Tab  Tab ) ]
  └ brand = link home     └ grey track, pill
```

| Part | Desktop | Mobile ≤640 |
|---|---|---|
| Bar | sticky, 12 from top; height 56; padding 0 8 0 16; gap 16; pill; `rgba(255,255,255,.9)` + `backdrop-filter: saturate(1.8) blur(12px)`; shadow `0 1px 2px rgba(0,0,0,.06)` | 8 from top; height 52; padding 0 6 0 12; gap 8 |
| Brand | `<a>` to the product home; icon + name, gap 8; Header type, weight **700**, ink | gap 6; **name stays visible** |
| Icon | 32, **circle** (`border-radius: 50%`), never a rounded square | 28 |
| Tab track | canvas `#F2F2F0` pill, padding 4, gap 0 | padding 3 |
| Tab | height 40, padding 0 16, Button type 600, grey; hover ink | height 34, padding 0 10 |
| Active tab | accent fill, ink text | same |
| Brand hover | marker: accent fill behind the name (margin 0 −4, padding 0 4) | same |

- The product icon is the photo or logo **exactly as the user gives it**: no crop, no zoom, only resize. If it isn't square, ask before cropping. Shown as a circle. Favicon is the same image cut to a circle with transparent corners.
- Clicking the brand goes home. If already home, re-render it.
- The frame below the bar follows **Layout → Frame**.

**How to check:** load both sites in headless Chrome at 1440, 393 and 360. Diff the computed style of bar, brand, icon, track, active tab and idle tab: height, padding, gap, background, shadow, radius, font size, line height, weight, color, top. Everything must match except width. Creator Hub keeps such a script (`navdiff.mjs`). Rerun it after any navbar change.

### Data pages: tight and clean (`data-ds-profile="compact"`)

Valuation, Work, dashboards, admin, trackers, screeners.

| | Desktop | Mobile |
|---|---|---|
| Tile gap | 12 | 12 |
| Block gap | 12 | 12 |
| Tile padding | 20 | 16 |
| Minimum row | 40 | 44 (touch) |
| Row vertical padding | 12 | 12 |

- **One 12 gap for everything**, so the page reads as one continuous board.
- Rows in tiles separate with hair lines. **No card in card.**
- **Mobile tables never scroll horizontally.** In order: (1) hide secondary columns; (2) shorten composite values to the main number (e.g. ATH becomes `peak (×N)`); (3) never shrink text.
- **Reference lists** (project lists, guides) go in **one dropdown tile, collapsed by default**. Daily content stays open.
- **Checklist:** one hero tile (date, task count, progress ring) directly above one white list tile. Ticks reset on a new day or week. Timed tasks appear in the "Lịch hôm nay" box.
- **Toolbar** on one row. Controls that no longer do anything are **removed**, not left floating.
- No `bento-hero` size.

### Presentation pages: room to breathe (`data-ds-profile="spacious"`)

CV, portfolio, landing, marketing, about pages.

| | Desktop | Mobile |
|---|---|---|
| Tile gap | 16 | 12 |
| Section gap | 48 | 32 |
| Tile padding | 32 | 20 |
| Hero tile | 2 of 4 columns, min height 320, padding 40 | padding 24 |

- One strong hero beside an accent metric tile and a contact tile.
- Sections separate with large gaps; tiles in a section use the tile gap.
- Paragraphs max 680 wide.
- Images in their own tile with a caption, no text over images.
- Contact buttons are flat canvas chips.

### Sample components

- **Metric tile:** accent or dark background; small 600 label on top, display-size number in the middle, small caption below.
- **List tile:** title row with title and a canvas pill counter; rows separated by hair lines.
- **Dropdown tile:** summary row with title (`bento-title`), counter and chevron; opens into row groups.
- **Row:** start: logo or 36 check box; middle: main text (body) and meta line (small, grey); end: 32 icon button, canvas, radius 10.
- **Checkbox:** circle 24, 2 px grey border. Ticked: black fill, white check; text becomes muted and struck through.
- **Progress ring:** 92 desktop, 80 mobile. Black on an accent tile, accent on a dark tile. `n/total` in the center.
- **Pill button:** white with shadow, 40 high on desktop. On a mobile toolbar 32 high with a full 44 touch target.
- **Table:** in a white tile; small grey 600 headers; rows separated by hair lines; numbers right-aligned.

### Pre-delivery check

1. **Count type sizes:** every text belongs to a style in the **Type** table, and CSS has no hand-typed `font-size` px.
2. **Count radii:** only 20, 10 and pill.
3. **At 390, 360 and 320:** nothing scrolls horizontally and no text is below 12.
4. **Tile colors:** at most 1 accent tile and 1 dark tile per screen.
5. **Look at real screenshots**, not only lint.

## Foundations and references

This is **a synthesized rule set for these products**; no single library defines all the numbers:

- [Radix spacing](https://www.radix-ui.com/themes/docs/theme/spacing): 4/8/12/16/24… scale, systematic density.
- [Radix Table source](https://github.com/radix-ui/themes/blob/main/packages/radix-ui-themes/src/components/table.css): compact cell padding 8 px, aligned content, separators and one shared surface.
- [shadcn Tasks source](https://github.com/shadcn-ui/ui/blob/main/apps/v4/app/%28app%29/examples/tasks/components/data-table.tsx): task workspace organized as rows/tables with shared actions, not one card per fact.
- [Carbon data table](https://www.carbondesignsystem.com/building-blocks/core/components/data-table/guidelines): density levels, 32 px dense desktop and 40 px default. Valuation's 56 px header is a product requirement, **not** derived from Carbon.

## Two web profiles

| | `spacious`: presentation | `compact`: work/data |
|---|---|---|
| Use | CV, portfolio, landing, about | Valuation, Work/Airdrop, dashboards, Admin, data tables |
| Goal | Read the story, clear CTA | Scan, compare, act fast |
| Base rhythm | 8 px | 4 px |
| Mobile margin | 16 px | 16 px |
| Desktop margin | 1200 px frame, min margin 48 px | 24 px; 1200 frame not required |
| Content groups | 64 desktop / 32 mobile | 16 px |
| Panel | Padding 16–32, gaps 16–24 | Cell/main padding 8, secondary panels 8–12 |
| Text | Body 16/24, lead 18/28 | Body 16/24; numbers/tasks/metadata 14/20 |
| Panel header | 20/28 for emphasis | 16/24, mobile may be 14/20 |
| Rows | By content, list min 56 | Default 40; dense desktop 32; touch 44 |
| Height | By content | By content, except panels explicitly fixed |
| Surface | Clear content blocks; deliberate whitespace | One surface per group, few background/border layers; row lines, not nested cards |

Don't apply landing section spacing to a workspace, or 22 px native-app text to web tables. A page can have a spacious hero and a compact data area, with a clear boundary.

## Palette: unchanged

- Global brand: **0x Blue `#1E6DF7`** in Light and Dark. Primary uses `blue` + `on-blue`; small text on tinted backgrounds uses `blue-strong`.
- Text has only three levels: `ink` (main), `grey` (secondary), `muted` (metadata/disabled). Don't use muted for what the user must read to act.
- Background `ground`, group `mist`, lines `line`. No fourth grey.
- Each status color has base / `-text` / `-soft`: green success, red error/danger, yellow pending/warning, orange attention, cyan info, purple secondary chain/new feature. Status color must come with text or a clear symbol.
- Text on yellow is always black. Solid fills by default; at most one large gradient per screen, none on text, small icons or data tables.
- Disabled: line background, muted text, no shadow, no reduced opacity.
- 0xhieu.xyz keeps black primary and cat-eye yellow `#FFA111`. That is an approved override in `products.0xhieu-xyz` and does not change the global palette.

## Typography

Inter for design/Figma/slides; Apple system/SF Pro with system fallback for web/app code. Full values and letter-spacing in `type.groups`.

| Web role | Style | Specs |
|---|---|---|
| Metadata/data | web-caption | 14/20, 400 |
| Label | web-label | 14/20, 600 |
| Content | web-body | 16/24, 400 |
| Panel/toolbar | web-nav-button | 16/24, 600 |
| Lead | web-lead | 18/28, 400 |
| Small heading | web-h4 | 20/28, 600 |
| Screen/section heading | web-h3 | 24/32, 600 |
| Display | web-h2/h1/hero | 40/48, 56/64, 72/80, 700; mobile uses its own styles |

Data text is never below 14. Numbers use `tabular-nums`; labels left-aligned, numbers in columns. Tasks/names/tags wrap and never lose text. Hover never shifts layout by weight. Body text may limit to 680 px; tables don't.

## Components and surfaces

- Radius: panel 16, small control 8, data row 0, pill/circle 9999. Don't wrap each label/number in a rounded box.
- Flat/line border is default. `shadow-y2` only for overlays, floating menus or justified raised surfaces; not on every button/card.
- Buttons: 40 compact, visible toolbar 32, spacious 48. Touch targets at least 44 and non-overlapping. Product toolbar exceptions must be documented.
- Inputs: compact 40, touch 44; mobile input text 16 to prevent zoom. Forms have labels, 2 px focus and error text.
- Focus is clearly visible, offset 2 px. Hover uses stable color/indicators; no card lift or text width change. No decorative motion.
- Popups fit content, with viewport max-height and scroll; background locked while open. Escape/backdrop as defined; long forms don't vanish on a stray click.
- Icons: Lucide 1.59.0, stroke 2, sizes 16/20/24/32. No emoji as action icons.

## Pattern: data table

One table surface with aligned header and body. Widths follow content, with room for long fields; don't divide all columns equally by percent. Header and body share measurement rules and scroll direction. The table scrolls internally when total minimum width exceeds the viewport; never overflow the page or overlap columns.

Don't break a composite value that must be read together just to keep a column narrow. Don't shrink fonts to hide width bugs. Only long list regions need a height limit. Don't add empty rows to fill a box. Headers with the same role share a token.

## Pattern: task workspace

Each group has one shared surface; each project is a row. Desktop separates project info and tasks. **Phase is a label column beside the task**, not a large heading taking an extra row per task. Mobile moves project info to the top, keeping phase and task together.

Keep all tasks/links; don't add scores, checklists or AI features. No repeating Daily color bands; color only for meaningful groups/statuses. Rank can be metadata; avoid multiple layers of labels, separators and badges for one idea.

## Pattern: CV/landing

Pick one alignment axis and content hierarchy. A CV is an editorial portfolio: avatar, name and identity message form one clear hero; experience is easy to read; images have captions. CTA is sufficient and doesn't compete with the title. Marketing landings may use larger display; a CV need not have a 72 px hero.

## 0xhieu.xyz rules

- `/` spacious; `/valuation` and `/work` compact. `/airdrop` redirects 301 to `/work`, with a client fallback.
- Old black/yellow brand. Navbar aligns to the current profile's frame.
- Valuation: 8 tokens on desktop and mobile; rows 40, table/popup/box headers **56**; header text 16/24 desktop, 14/20 mobile, 600. Three boxes **328 px fixed**, long content scrolls; mobile uses 2 equal columns and no box spans a row.
- Box label/value left/right, min-height 56, growing to show full text. Tickers under $300M bold black; from $300M bold orange, no dot. ATH `start → end (×N)` on one line, ratio from raw numbers, bold orange.
- Work: project column 240 desktop; phase 104; padding 8; task 40 desktop/44 touch; group gap 16. These serve the pattern and aren't general spacing.
- CV: frame 1200; hero top 96/48, block gap 64/32; portrait 112/72. CV content stays English, tagline verbatim.
- One-row mobile toolbar is a specific requirement: title 20/18/16/14, visible control 32. Don't make this exception a general touch standard.

## Native app and slides

Keep existing dedicated tokens: app scale 14/16/18/22/28/34/48, body 22/28, input/button 48; device safe areas. Slides 1920×1080 keep margin 128, gutter 64 and slide type. They aren't replaced by compact web geometry. Grid/type tables in `tokens.json` are authoritative.

## Export, QA and changes

Run `python export_web.py`; commit tokens and exported CSS together. Hashes use canonical JSON (sorted keys, no whitespace), independent of Windows/Linux CRLF/LF. Websites must sync the CSS and record the version, never read remote CSS at runtime. Use the JSON source to verify colors didn't change out of scope.

Minimum QA: desktop 1440/1024/768 and mobile 640/390/360/320; languages; empty/long data; no clipped text or column overflow; all links/actions; hover/focus; touch targets; popups; navbar and back/forward. Look at real screenshots, not only lint. Component tests check role/layout, not just one isolated number.

Original Figma: https://www.figma.com/design/IPyKVg7ylGw1mjMRyYVrL7/hieu. v3 tokens and new patterns are **not yet synced to Figma**; do not claim the file contains these changes.

## 0xhieu.xyz — workspace alignment approved 2026-11-01

Valuation and Work share the product workspace tokens: max frame1280px including padding, radius8, neutral white card headers, line border, horizontal card padding12, section padding8 and card gap12. Work uses independent cards: desktop2 columns, mobile1 (<=900px), DAILY yellow-soft with orange-text label. Reference chosen by user: [Linear Board](https://linear.app/docs/board-layout). Valuation retains 8 visible rows, 56px headers, fixed328px panels and its existing panel column counts. These product decisions supersede earlier product list/fluid-layout guidance; do not apply them to unrelated products without approval.

### Shared component identity across all three pages

For 0xhieu.xyz, `sharedComponents` applies to CV as well as Valuation and Work: card/control/badge radius8, white surface, line border, no decorative card shadow. Spacious and compact control spacing/type density, not separate card styles. CV keeps its spacious hero, section gaps and 16px body text. Circular avatars/language switches and radius16 overlays retain their distinct roles. CV social buttons, Highlights and Available-for labels must consume the same product component tokens; do not leave legacy radius16/pill surfaces in those components.

### Approved action elevation

User requires drop shadow on clickable button surfaces across CV/Valuation/Work: existing black32%, y2px, blur8px token. Read-only cards/badges/content and disabled controls stay flat. Text navigation/inline links keep their text treatment. This supersedes the earlier overlay-only shadow restriction.

### Approved orange headers

User overrides neutral header surfaces: Work card headers, Valuation panel/table headers and matching table popup headers use solid product accent #FFA111 with ink/black text. Bodies remain white; DAILY remains soft yellow. Source: product workspace/headerSurface=accent. This supersedes earlier white-header guidance; dimensions stay unchanged.

### Approved accent text

0xhieu.xyz accent text uses the same product orange #FFA111, weight600. Do not substitute earth-orange #B84A0C for emphasis. Orange header backgrounds use black text. Global palette tokens for other products remain unchanged.

## Current 0xhieu.xyz blue theme — user decision 2026-11-01

Supersedes previous orange rules: black normal text, grey secondary text, blue important text. Use existing cobalt #1E6DF7 for primary actions/header fills and blue-strong #0F3DB2 for small important text on grey/tinted surfaces. White page, grey mist card/popup bodies, cobalt headers with on-blue/white text, blue-soft DAILY. Header interactive text remains white on hover; use underline instead of same-color blue text. Cards/labels remain flat, buttons keep approved drop shadows. Red is only semantic danger/destructive feedback. Preserve approved geometry, all source data/formulas, and original logo/photo artwork.

## Current product decision: black/orange + stronger DAILY + single language switch

Supersedes blue product theme: regular orange #FFA111 for button/header fills, black text on those fills, dark orange #B84A0C for important text, normal text black, secondary grey, card bodies grey. DAILY uses yellow-soft with a4px orange left border and dark-orange bold task text. VI/EN is one native accessible switch with a single translating thumb and two labels, not two circular buttons. Dimensions/data/formulas remain unchanged.

## 2026-11-02: softer headers and continuous rank slider

User requires pale orange `orange-soft` box/table headers with black text. Keep saturated orange for smaller buttons/selection highlights rather than large header fills. Work rank is one continuous bar with one sliding orange selected region, native range keyboard/drag support and scroll-spy synchronization; five independent circular buttons are prohibited.

## 2026-11-02: header matches DAILY

Supersedes the pale orange header rule: product box/table headers use the exact DAILY background `yellow-soft` #FEF5D9, black text.

## 2026-11-02: shared horizontal frame

CV, Work, Valuation and navigation/footer share max1280 border-box, horizontal inset24 desktop/16 mobile. CV spacious density does not change the common horizontal frame.

## Current 0xhieu.xyz tone — user decision 2026-11-04

Supersedes every earlier orange/blue/cream rule above for this product. White-grey-black: white page and card bodies, mist `#ECF0F8` table/box headers and popups, black text, grey secondary text. Orange `#FFA111` only on buttons, selected controls and highlights (accent text weight 600; black text on orange fills). Button hover is black with white text; input focus is black. Earth orange `#B84A0C` and cream `#FEF5D9` are banned on this product; the global palette for other products is unchanged. Red stays semantic danger only.

## 0xhieu.xyz DAILY and rank label — user decision 2026-11-04

Supersedes earlier DAILY rules: DAILY stands out through a mist section surface, without an orange border. Task text is black weight 400 at rest and weight 600 on hover, the same as every clickable item. The Work-to-Earn position in the rank bar is labelled `w2e`, because `$` looked like `S`.

## 0xhieu.xyz neutral surface, marker highlight and Work tags — user decision 2026-11-06

Supersedes the mist and orange-text rules above for this product. Headers, popups and DAILY use the product token `--ds-color-surface` `#E5E5E5` (neutral, slightly darker than mist); the global `mist` for other products is unchanged. Highlighted text is a marker: black text weight 600 on an `#FFA111` fill, never orange text on white. Work header tags: rank w2e/S, high-potential and narratives in the Valuation Trending Narratives top 5 are black fill with white text; rank A/B/C, low-potential and other narratives are white with a line border and black text. Hero or Zero values use the same marker; red stays for danger badges (table ×ATM≥15) only.
