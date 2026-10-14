# LIS-SKINS 2.0 — Design Foundations

Source: Figma file **LIS-SKINS — 2.0 Main Tests** (`EVxUMxDli8t4nDrc6D7nMZ`)
- Page `0. Sevice` (cover, navigation, breakpoints, fonts)
- Page `🎨 Icons & Colors` (colors, icons, images, rarity system)

Extracted 2026-10-07. Values are taken directly from the file's local variables and styles.

---

## Rules
- Every interactive component (buttons, inputs, cards, links, tabs, etc.) MUST have:
  default, hover, active, focused, disabled, loading, error states
- Auto Layout on ALL components, no exceptions
- Detachment rate target: <5%
- Use only existing components (instances) from the 🛠️ UI kit page. Create a new component
  only if no suitable one exists — and always ask before creating it

---

## Mockup naming

A mockup (screen frame) must be named in the format:

**[Section] / [Page] / [State] / [Variant] — [Platform]**

### 1. Platforms

| Value | When to use |
|---|---|
| `Desktop` | Main desktop version |
| `Mobile` | Mobile version |
| `Tablet` | Tablet version |
| `Large` | Wide screens 1920+ |

The platform goes **at the end**, after a dash `-`, so that the essence of the screen — not the platform — is visible at a glance.

### 2. Name segments

#### 2.1 Section
Top-level section of the site. Short, capitalized. Hint: see the page name in Figma.

`Index` · `Sell` · `Market` · `Profile` · `Content`

#### 2.2 Page or subsection
A specific page or feature within the section.

- `Market / Skin page`
- `Sell / Confirm`

If a page is specific to a domain or locale, the URL is given in parentheses after the name. For example, the Sell page for CS2 skins can exist in two variants depending on the URL — they differ by the presence of breadcrumbs and the heading wording:

| Name | Meaning |
|---|---|
| `Index / Guest (lis-skins.com/ru/) - Desktop` | Site home page for a logged-out user |
| `Index / Auth (lis-skins.com/ru/) - Desktop` | The home page turns into Sell after the user logs in |
| `Sell (lis-skins.com/ru/cs2) - Desktop` | Same page as `Index / Auth (lis-skins.com/ru/) - Desktop`, but with breadcrumbs and a different heading |

#### 2.3 State (if needed)
Shows a specific UI state on this screen.

| Value | When to use |
|---|---|
| `Default` | Base state of the page |
| `Empty` | Empty state (no data) |
| `Fill` | Filled state (input, form) |
| `Error` | Error state |
| `Loading` | Loading state |
| `Success` | Action completed successfully |
| `Disabled` | Unavailable element |

Examples:
- `Sell / Search / Empty - Desktop`
- `Sell / Search / Fill - Desktop`
- `Sell / Search / Error - Desktop`

#### 2.4 Variant (if needed)
Used for regional/currency variants or sequential numbers of popups.

**Currencies and locales** — comma-separated:
- `Sell / Default / EUR, KZT, UAH - Desktop`

**Popups** — with a sequential number:
- `Sell / Instant Payout / Step 1 - Desktop`
- `Sell / Instant Payout / Step 2 - Desktop`

#### 2.5 Nesting depth
Maximum **4 segments** before the platform dash:

`[Section] / [Page] / [State] / [Variant] - [Platform]`

If you want to add a fifth segment, reconsider the structure and merge one of the levels.

### 3. Examples

| Examples |
|---|
| `Index / Guest (lis-skins.com/ru/) - Desktop` |
| `Sell / Account is Frozen - Mobile` |
| `Sell / Sell skins (site.com/ru/rust) - Desktop` |
| `Sell / Search / Fill - Desktop` |
| `Sell / Default / EUR, KZT, UAH - Desktop` |
| `Sell / Instant Payout / Step 1 - Desktop` |

### 4. General formatting rules

- Every segment starts with a **capital letter**
- Separator between segments — `/` (with spaces)
- Separator before the platform — `–` (long dash with spaces)
- Names are **in English and readable**, without technical abbreviations
- Long descriptive names are **shortened** — the meaning is clear from the path
- A URL in the name is written **in parentheses**, in lowercase

---

## Component naming

### 1. Case and writing style

Everything in **kebab-case**. No spaces, capital letters, underscores or mixed styles.

- ✅ `skin-card/sticker-charm`
- ❌ `Skin Card - Sticker/Charm`, `skinCard/StickerCharm`

### 2. Grouping with `/`

Every component belongs to a group. The slash is the separator between hierarchy levels. Maximum **3 levels**, no deeper.

In Figma, a slash in the name automatically creates a folder: all components with the prefix `notification/` are collected into one `notification` folder, with a `bottom` subfolder inside it. This makes the library easy to navigate — no need to scroll through hundreds of components, just open the right folder.

- ✅ `notification/bottom/row`
- ❌ `sell-skins/confirm/deal-bottom/rows` (4 levels — too deep)

### 3. No standalone names without a group

Every component belongs to a group. The base component of a group is called `main`. Specific variants get a meaningful name within the same group.

- ✅ `select/main` — base select
- ✅ `select/bank`, `select/crypto` — specific variants
- ❌ `Counter`, `crypto`, `wear`, `filters` — no group

When all variants of a component are in one group, they are collected into one folder in the Figma panel. This lets a designer quickly find the right variant without scrolling the whole list, and lets a developer immediately see that all `select/*` are one entity with different configurations.

### 4. Sizes in words

`small`, `medium`, `large` — no `S`, `M`, `L` or numbers.

- ✅ `search/small`, `switcher/medium`
- ❌ `search/s`, `Switcher M`, `Float - M`

### 5. Platform is always the `-mobile` suffix

The mobile version of a component is always marked with the `-mobile` suffix at the end of the name. The desktop version has no suffix — it is considered the default base.

- ✅ `header` + `header-mobile`
- ✅ `footer` + `footer-mobile`
- ✅ `popup/welcome` + `popup/welcome-mobile`
- ✅ `skin-page/table-row-float` + `skin-page/table-row-float-mobile`

The platform **never** creates a hierarchy level with `/`:
- ❌ `popup/mobile/header` → ✅ `popup/header-mobile`
- ❌ `header/mobile` → ✅ `header-mobile`

And it is never moved to the start of the name or into parentheses:
- ❌ `Mobile Header`, `Mobile / Skin Page / Table / Row / Float`, `Popup - Need auth (Mobile)`

### 6. No utility words `old`, `new`, `2`

Instead — `legacy` for outdated components, a specific description for new ones.

- ✅ `tooltip/legacy`, `tooltip/main`
- ❌ `Tooltip old`, `tooltip-new`, `Popup - KYC 2`

### 7. Popups — single `popup/` hierarchy

All popups live in the `popup/` group. Mobile versions of popups use the `-mobile` suffix.

- ✅ `popup/welcome`, `popup/welcome-mobile`, `popup/header-mobile`
- ❌ `Popup - Need auth`, `Popup-mobile/Title`, `Popup - Need auth (Mobile)`

### 8. Sizes and themes — inside the component as properties, not in the name

**Ideally:** size and theme are exposed as component properties, not duplicated as separate components.

- ✅ One component `textarea/main` with property `Theme=Dark | Light`

**If they can't be separated** — use a `theme-*` or `size-*` suffix:

| Situation | Naming |
|---|---|
| Theme split into a separate component | `textarea/theme-dark`, `textarea/theme-light` |
| Size split into a separate component | `button/size-small`, `button/size-large` |
| Platform split into a separate component | `header`, `header-mobile` |

The `theme-` and `size-` suffixes are a signal of technical debt.

### 9. Name by entity, not by place of use

The name should say **what it is**, not **where it is** in the file. If a component logically belongs to a section (e.g. elements that exist only inside sell skins), grouping by section is justified. But if a component is used in different places, naming it after a specific page creates a false binding.

- ✅ `sell-skins/deal-info` — exists only in sell skins, grouping by section is justified

**Component used in several sections** → name it by entity, not by one of the places:
- ✅ `deal/status` (not `transactions/deal-status` and not `sell-skins/deal-status`)
- ✅ `avatar/main`, `pagination/main`

**Component used everywhere** → lives in a root group named by its entity, without `all-pages/`:
- ✅ `avatar/main`, `badge/count`, `tag/main`
- ❌ `all-pages/avatar`, `all-pages/count-badge`

---

## Component description structure — desired result

**Component name — General description**

A short explanation: what the component is, what problem it solves, and in what context it is used in the interface.

*Example: Component X is used for… and is applied in the context of…*

**Usage**

List of screens/pages/components where this component appears (found via search with the Instance filter):

- **Page / Screen 1** — short explanation of the usage context
- **Page / Screen 2** — short explanation of the usage context
- **Parent component** — short explanation of the usage context

**Behavior**

Description of how the component works during user interaction:

**States:**

- **Default** — description of the default state
- **Hover** — description of the reaction on hover
- **Focus** — description of the focus state
- **Active / Pressed** — description on press
- **Disabled** — description of the unavailable state
- **Loading** — description of the loading state
- **Error** — description of the error state

---

## 1. Token architecture

Tokens are Figma variables organised in 5 collections:

| Collection | Modes | Vars | Role |
|---|---|---|---|
| `primitivesColors` | Mode | 253 | Raw palette — never referenced by meaning |
| `semanticColors` | **Dark** (default), **Light** | 29 | Theme tokens, alias primitives |
| `primitivesSizes` | Mode | 53 | Spacing, radius, icon sizes |
| `typography` | **Desktop**, **Mobile** | 39 | Font family, weight, size, line-height, tracking, case |
| `copy` | **Ru**, **Eng** | 2216 | Localized UI strings, grouped by product area |

Layering rule: **primitive → semantic → component**. UI should consume semantic tokens; primitives are used directly only where no semantic token exists yet (e.g. surfaces, status colors).

The product is **dark-first**: Dark is the default mode, Light is a secondary theme.

---

## 2. Color

### 2.1 Primitive palettes

#### Grey (neutral) — `color/grey/*`
| Step | Hex | Typical use |
|---|---|---|
| 10 | `#FFFFFF` | Text on dark / Light BG |
| 20 | `#E6E6E6` | Light popup BG |
| 30 | `#CECECE` | Light stroke, links on dark |
| 40 | `#B6B6B6` | Secondary text (dark) |
| 50 | `#9E9E9E` | Hover/open stroke |
| 60 | `#878787` | Disabled text (dark) |
| 70 | `#717171` | Disabled links |
| 80 | `#5A5A5A` | |
| 90 | `#444444` | Default stroke (dark) |
| 100 | `#2E2E2E` | Elevated surface / secondary text (light) |
| 110 | `#232323` | Popup / card surface (dark) |
| 120 | `#161616` | Page background (dark) |

#### Orange (brand) — `color/orange/*`
| Step | Hex |
|---|---|
| 10 | `#FFF5EE` |
| 20 | `#FFC8A9` |
| 30 | `#F89E71` |
| 40 | `#FC9148` |
| **50** | **`#FF831F`** — brand / accent |
| 55 | `#FF5F00` — saturated accent (off-scale) |
| 60 | `#954000` |
| 70 | `#702900` |
| 80 | `#481800` |
| 85 | `#442C1B` — muted brown (off-scale) |
| 90 | `#220901` |
| 100 | `#050100` |

#### Red (danger) — `color/red/*`
`10 #FEE2E2` · `20 #FECACA` · `30 #FCA5A5` · `40 #F87171` · **`50 #F05252`** · `60 #DC2626` · `70 #B91C1C` · `80 #991B1B` · `90 #7F1D1D` · `100 #450A0A`

#### Single-step accents (`/50` only)
| Token | Hex | Meaning |
|---|---|---|
| `color/green/50` | `#3FDCA1` | Success |
| `color/yellow/50` | `#FFDB54` | Warning / attention, Souvenir |
| `color/purple/50` | `#AC94FA` | Decorative |
| `color/violet/50` | `#8585FF` | Decorative / info |
| `color/lightCyan/50` | `#78E8FF` | Info, Factory New |
| `color/blue/50` | `#3D78F5` | Blue % pattern filter (Case Hardened blue gem). Scoped to fills, strokes, effects |

#### Alpha ramps — `alpha/<color>/<opacity>`
Opacity steps (subset per color): `0, 2, 4, 6, 8, 10, 12, 20, 30, 40, 50, 60, 70, 80, 90`.

| Ramp | Base | Steps |
|---|---|---|
| `alpha/white` | `#FFFFFF` | 0, 2, 4, 6, 8, 10, 12, 20–90 |
| `alpha/black` | `#161616` | 0, 4, 6, 8, 10, 12, 20–90 |
| `alpha/orange` | `#FF831F` | 0, 4, 6, 8, 10, 12, 20–90 |
| `alpha/red` | `#F05252` | 0, 4, 10–90 |
| `alpha/green` | `#3FDCA1` | 0, 10–90 |
| `alpha/yellow` | `#FFDB54` | 0, 10–90 |
| `alpha/purple` | `#AC94FA` | 0, 10–90 |
| `alpha/violet` | `#8585FF` | 0, 10–90 |
| `alpha/lightCyan` | `#78E8FF` | 0, 10–90 |
| `alpha/grey100` | `#2E2E2E` | 0, 10–90 |
| `alpha/grey110` | `#232323` | 0, 10–90 |

Low white alphas (`alpha/white/4–12`) are used for hover fills, dividers and subtle surfaces on dark; tinted alphas (`alpha/orange/10`, `alpha/red/10`, …) for status backgrounds and badges.

### 2.2 Semantic colors — `semanticColors`

| Token | Dark | Light |
|---|---|---|
| `BG` | grey/120 `#161616` | grey/10 `#FFFFFF` |
| `popup/background` | grey/110 `#232323` | grey/20 `#E6E6E6` |
| `text/primary` | grey/10 `#FFFFFF` | grey/120 `#161616` |
| `text/secondary` | grey/40 `#B6B6B6` | grey/100 `#2E2E2E` |
| `text/disable` | grey/60 `#878787` | grey/100 `#2E2E2E` |
| `text/accent/default` | orange/50 `#FF831F` | orange/50 `#FF831F` |
| `text/accent/hover` | orange/30 `#F89E71` | orange/60 `#954000` |
| `text/accent/disable` | orange/60 `#954000` | orange/20 `#FFC8A9` |
| `stroke/default` | grey/90 `#444444` | grey/30 `#CECECE` |
| `stroke/hover` | grey/50 `#9E9E9E` | grey/50 `#9E9E9E` |
| `stroke/open` | grey/50 `#9E9E9E` | grey/50 `#9E9E9E` |

**Links** (each has `default` / `hover` / `disable`):

| Token | Dark (default · hover · disable) | Light (default · hover · disable) |
|---|---|---|
| `link/accent/*` | → `text/accent/*` | → `text/accent/*` |
| `link/primary/grey/*` | grey/30 · orange/30 · grey/70 | grey/100 · orange/55 · grey/40 |
| `link/primary/dark/*` | grey/30 · orange/30 · grey/70 | orange/90 · grey/70 · grey/40 |
| `link/red/*` | red/50 · red/70 · red/90 | red/50 · red/70 · red/90 |

**Third-party brand** (fixed across modes): `trustpilot/green #00B67A`, `/lime #73CF11`, `/yellow #FFCE00`, `/orange #FF8622`, `/red #FF3722`, `/gray #DDDDE7` (Light: `#DCDCE6`).

### 2.3 Domain colors

#### Item wear — `color/wear/*`
| Wear | Hex |
|---|---|
| Factory New | `#78E8FF` |
| Minimal Wear | `#BEFF4F` |
| Field-Tested | `#FFDB54` |
| Well-Worn | `#FF8035` |
| Battle-Scarred | `#FF6060` |
| Not Painted | `#B2B4BB` |

#### Special qualities — `color/other/*`
- `stattrak` `#B67EFF`
- `souvenir` → `color/yellow/50` `#FFDB54`

#### Rarity — `color/rarity/*`
Each rarity has three steps: `/100` (solid), `/50` (50% alpha, used for glows), `/0` (transparent end of gradients).

**CS2 — weapons** (`cs/weaponRarity/*`)
| Rarity | Hex |
|---|---|
| Contraband VII | `#F0762F` |
| Covert VI | `#F05252` |
| Classified V | `#D32CE6` (alias of dota2/legendary) |
| Restricted IV | `#9747FF` |
| Mil-Spec Grade III | `#1A93CD` |
| Industrial Grade II | `#90DBFF` |
| Consumer Grade I | `#FFFFFF` |

**CS2 — agents** (`cs/agentRarity/*`, all aliases): Master → Covert · Superior → Classified · Exceptional → Restricted · Distinguished → Mil-Spec.

**CS2 — stickers & other** (`cs/stickersOtherRarity/*`): Rare Special VIII `#FFC44E` · Contraband `#F0762F` · Extraordinary → Covert · Exotic → Classified · Remarkable → Restricted · High Grade → Mil-Spec · Base Grade → Consumer.

**Dota 2** (`dota2/*`)
| Rarity | Hex |
|---|---|
| Common I | `#B0C3D9` |
| Uncommon II | `#5E98D9` |
| Rare III | `#4B69FF` |
| Mythical IV | `#8847FF` |
| Legendary V | `#D32CE6` |
| Immortal VI | `#B28A33` |
| Arcana VII | `#ADE55C` |
| Ancient VIII | `#EB4B4B` |
| Dota+ | `#FFF34F` |

### 2.4 Gradients & image fills (paint styles)
329 paint styles; almost all are image fills, not colors.
- `Gradients/*` — Red, Orange, Grey, BG (3), Giveaway, Giveaway gray gradient, All unavailable
- Image sets — `Skins/CS2` (97), `Skins/Dota2` (20), `Skins/Rust` (18), `Skin types/*`, `User/1–9` avatars, `Emoji/1–8`, `Bonus imgs/1–9`, `Gems/1–4`, `Prize/$5–$20`, `Referral/*`, `BG/*` (incl. Hero Dota, Hero Rust), `Blogger avatars/*`

---

## 3. Typography

**Family:** IBM Plex Sans (Google Fonts) — the only typeface in the product.
**Weights:** Regular 400 · Medium 500 · Bold 700 (Bold only in H1).
All 28 text styles are bound to `typography` variables (`fontFamily/body`, `fontWeight/*`, `fontSize/*`, `lineHeight/*`, `letterSpacing/*`, `textTransform/*`).

### 3.1 Type scale

| Style | Weight | Size / Line | Case | Tracking |
|---|---|---|---|---|
| `Display/Hero` | Medium | 56 / 68 | UPPER | 0 |
| `Heading/H1/Bold` | Bold | 34 / 44 | UPPER | 0 |
| `Heading/H1/Medium` | Medium | 34 / 44 | UPPER | 0 |
| `Heading/H2` | Medium | 28 / 38 | UPPER | 0 |
| `Heading/H3` | Medium | 24 / 34 | — | 0 |
| `Heading/H4` | Medium | 17 / 24 | — | 0 |
| `Heading/H5` | Medium | 15 / 22 | — | 0 |
| `Subtitle/Subtitle 1` | Medium | 28 / 38 | — | 0 |
| `Subtitle/Subtitle 2` | Medium | 21 / 30 | — | 0 |

### 3.2 Body

Pattern: `Body/<size>/<default|uppercase>/<regular|medium>`. Uppercase variants are 1px smaller (except xxs) with **+0.3px** tracking.

| Size | Default (R/M) | Uppercase (R/M) |
|---|---|---|
| `l` | 17 / 24 | 16 / 22 (Medium only) |
| `m` | 15 / 22 | 14 / 20 · +0.3 |
| `s` | 13 / 18 | 12 / 17 · +0.3 |
| `xs` | 12 / 17 | 11 / 16 · +0.3 |
| `xxs` | 11 / 16 | 11 / 16 · +0.3 |

### 3.3 Raw typography tokens
- `fontSize/*`: 11, 12, 13, 14, 15, 16, 17, 19, 21, 22, 24, 26, 28, 32, 34, 42, 56
- `lineHeight/*`: 16, 17, 18, 20, 22, 24, 28, 30, 34, 38, 42, 44, 58, 68
- `letterSpacing/normal` 0 · `letterSpacing/wide` 0.3
- `textTransform/none` · `textTransform/uppercase`
- Modes **Desktop** / **Mobile** exist but currently hold identical values.

---

## 4. Spacing

`primitivesSizes` → `spacing/*` (px). Base rhythm is **2 / 4px**.

| Group | Values |
|---|---|
| Micro | 0, 1, 2, 4, 6, 8, 10, 12 |
| Component | 16, 18, 20, 22, 24, 28, 30, 32, 36, 38, 40 |
| Section | 44, 48, 50, 56, 68, 72, 80, 100 |
| Layout widths | 342, 360, 420, 566, 640, 1124, 1480 |

Layout widths are fixed containers (e.g. 360 mobile frame, 420/566/640 popup widths, 1124/1480 content max-widths).

---

## 5. Radius

| Token | px |
|---|---|
| `radius/none` | 0 |
| `radius/xxs` | 2 |
| `radius/xs` | 4 |
| `radius/s` | 6 |
| `radius/m` | 8 |
| `radius/l` | 12 |
| `radius/xl` | 16 |
| `radius/2xl` | 20 |
| `radius/3xl` | 24 |
| `radius/round` | 999 |

---

## 6. Elevation & effects

| Effect style | Definition | Use |
|---|---|---|
| `Drop shadow/black` | drop 0 4 / blur 4 | Small elements on dark |
| `Dropshadow/orange` | drop 0 4 / blur 15 | Accent CTA glow |
| `Drop shadow/search cart` | drop 0 50 / blur 50 | Floating search / cart panels |
| `Drop shadow/light theme` | drop 0 4 / blur 6 / spread −4 + drop 0 10 / blur 15 / spread −3 | Cards in Light theme |
| `Header` | background blur 25 | Sticky translucent header |

On dark, elevation comes mostly from surface steps (`grey/120` → `grey/110` → `grey/100`) and `alpha/white` overlays, not shadows.

---

## 7. Layout & breakpoints

| Breakpoint | Min width |
|---|---|
| `md` | 880px |
| `lg` | 1050px |
| `xl` | 1190px |
| `xxl` | 1450px |

Below `md` = mobile (design frame 360px). Max content widths: 1124 / 1480 (`spacing/1124`, `spacing/1480`).

---

## 8. Iconography

### 8.1 Sizes — `icon/*`
`xs 12` · `s 16` · `m 18` · `l 22` · `xl 28` · `2xl 32` · `3xl 40` · `4xl 54` · `5xl 160`
Main UI icon size is **22**; 16 and 12 for dense UI.

### 8.2 Naming
`Icons / <size>/<name>-<style>`, style ∈ `linear` (outline, default), `bold` (filled, active/selected), `duotone` (decorative/illustrative).
Examples: `22/cart-linear`, `22/cart-bold`, `22/chat-duotone`, `16/heart-bold`, `12/lock-bold`.

### 8.3 Inventory (≈79 icons)
Navigation & actions: arrow-left/right, chevron-top/bottom/left/right, close, check, copy, pencil, external-link, filters, sort, sort-ascending/descending, search, menu, update, log-out, eye, clear
Commerce: cart, buy-skins, buy-bulk, sell-skins, inventory, refill, overstock, charm, layers
Status & info: info, attention, error, check-in-circle, progress, clock, lock, safety, question, bell, hot, fast
Product/other: api, blog, browser, desktop, camera, chat, mail, data, day, routing, cursor, referral, steam, steam-in-circle, support, heart

---

## 9. Asset components

| Component set | Variants / properties |
|---|---|
| `Logo Lis-skins` | type: Default, With text, Christmas, Christmas2, Christmas32 · Size: 22–68 · theme: dark/light |
| `State` | Success, Error, Info, Attention, Partial Success, Update · 22 / 32 / 40 |
| `Deal status` | Error, Success, Wait |
| `Spinner` | Small, Large, 16, 22, 32, 40 · White / Orange |
| `Name Tag` | Default / Hover · Show Tooltip |
| `ticket` | 16 / 22 / 32 |
| `Flugs` (flags) | ua, kz, ru, usa · 22 / 28 / 32 |
| `Social Icons` | vk, telegram, youtube, steam, x, whatsapp, instagram, tiktok… · 22/32/40 · Grey / Color |
| `Payment icons` | 81 — crypto & methods (sbp, tether, usdc, bnb, ltc, sol…) · 18/22/28/32 |
| `payment-logo/s`, `Payment logo - M` | 55 methods · show text/description toggles |
| `Banks` | 151 bank logos |
| `Emoji` | 10 reactions |
| `all-pages/icons` | Fast, Profitable, Referral, Safely, Trade, List, Discount, Variety (feature illustrations) |
| `rarity/lines-cs2-cs:go`, `rarity/lines-dota2` | Rarity line accents · 100 / 200 |
| `rarity/backgrounds-cs2-cs:go`, `rarity/backgrounds-dota2` | Rarity glow card backgrounds · 112 / 174 / 495 |
| `bg-dots/cs2`, `bg-dots/dota2` | Dotted rarity patterns |

---

## 10. Content & localization

- All UI copy lives in the `copy` collection with **Ru** and **Eng** modes — switch the mode on a frame to localize it.
- Grouped by product area: `General/*`, `2 Sell skins/*`, `3 Market/*`, `4 Profile/*`, `5 Refill, Withdrawal/*`, `6 Content/*`.
- Product sections (from Navigation): 1 Index/Welcome · 2 Sell skins · 3 Market · 4 Profile · 5 Refill/Withdrawal · 6 Content · 7 Giveaway.

---

## 11. Code reference (CSS custom properties)

```css
:root {
  /* Brand */
  --color-accent: #FF831F;          /* orange/50 */
  --color-accent-strong: #FF5F00;   /* orange/55 */

  /* Status */
  --color-success: #3FDCA1;
  --color-warning: #FFDB54;
  --color-danger:  #F05252;
  --color-info:    #78E8FF;

  /* Radius */
  --radius-xxs: 2px; --radius-xs: 4px; --radius-s: 6px; --radius-m: 8px;
  --radius-l: 12px; --radius-xl: 16px; --radius-2xl: 20px; --radius-3xl: 24px;
  --radius-round: 999px;

  /* Typography */
  --font-body: "IBM Plex Sans", system-ui, sans-serif;
  --tracking-wide: 0.3px;
}

/* Dark — default */
:root, [data-theme="dark"] {
  --bg: #161616;
  --popup-bg: #232323;
  --text-primary: #FFFFFF;
  --text-secondary: #B6B6B6;
  --text-disable: #878787;
  --text-accent: #FF831F;
  --text-accent-hover: #F89E71;
  --text-accent-disable: #954000;
  --stroke-default: #444444;
  --stroke-hover: #9E9E9E;
  --stroke-open: #9E9E9E;
}

[data-theme="light"] {
  --bg: #FFFFFF;
  --popup-bg: #E6E6E6;
  --text-primary: #161616;
  --text-secondary: #2E2E2E;
  --text-disable: #2E2E2E;
  --text-accent: #FF831F;
  --text-accent-hover: #954000;
  --text-accent-disable: #FFC8A9;
  --stroke-default: #CECECE;
  --stroke-hover: #9E9E9E;
  --stroke-open: #9E9E9E;
}

/* Breakpoints */
/* md 880px · lg 1050px · xl 1190px · xxl 1450px */
```

---

## 12. Known gaps & inconsistencies

1. **Thin semantic layer** — no tokens for surfaces (beyond `BG`/`popup`), status (success/warning/error/info), buttons, inputs or overlays. Screens likely bind primitives directly, which weakens Light mode.
2. **Light mode issues** — `text/disable` equals `text/secondary` (`#2E2E2E`); `link/primary/dark/default` resolves to near-black `orange/90`.
3. **Variable scoping** — 281 of 367 non-copy variables use *All scopes*; none have code syntax or descriptions.
4. **Off-scale steps** — `orange/55`, `orange/85`; several hues have only a `/50` step.
5. **Rarity mismatch** — `classified/100` = `#D32CE6` but `classified/50` = `#FD00D5` @ 40% (different hue and alpha than other `/50` steps); `consumerGrade/50` is 30% instead of 50%.
6. **Typography modes** — Desktop and Mobile values are identical; no responsive type scale yet.
7. **Naming** — mixed casing (`BG` vs `text/primary`, `Drop shadow` vs `Dropshadow`), typos (`Flugs`, `Brackpoints`, `Partitial Success`, `Sevice`, `anavailable`), default props (`Property 1` in `ticket`, `Deal status`), mixed icon names (`search_linear`, `Arrow-left-Linear`).
8. **Layout widths in spacing** — 342–1480 belong in a separate `layout/*` or `container/*` group.
