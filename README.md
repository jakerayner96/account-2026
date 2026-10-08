# Account 2026 — All Brands

Configurator prototype for the **new 2026 account designs** on all 16 fascias with 2026 account frames (no live-format toggle — Jake, 06 Oct), built on the DS (`../../assets/ds/tokens.css` + `components.css`, linked, not copied). It uses the same shell as Core PDP 2026 and PLP UI updates: **window** controls on top, **page** controls down the left.

- **Live:** https://jakerayner96.github.io/account-2026/ · **Repo:** github.com/jakerayner96/account-2026
- **Configurator:** `index.html` · **Page:** `account.html` (reads `?s=<base64 state>`, `?brand=`, or `window.ACCT_PRESET`)
- DS: tokens, components, icons, brand art and the USP banners load from the live DS site (`jakerayner96.github.io/debenhamsgroup.design/assets/…`), so publishing a DS change updates this prototype. Serve locally with `python3 -m http.server` from the repo root.
- Listed on the DS site under Projects as **Account 2026**.

## Figma sources

| File | Node | Used for |
|---|---|---|
| SEEL Enhancements 2026 `CQIe2e2c0iagD1T9WjdYsx` | 3336-188708 (Latest UI 16.09.26) | The five Unlimited states (Regular · Unlimited · Unlimited+ · Expiring · Unlimited+ Expiring): dot #D6D6D6 / #70C474 / #D33F3F, 12px caps, ∞ icon (now DS `unlimited-infinity`; Unlimited+ uses DS `unlimited-plus`) |
| Account 2026 `2KLlzqIWlDcri8YIHwEd63` | 1009:1836 — Debenhams / PLT / boohoo Account sections (1296:69081, 1292:68264, 1304:17136) | Balance card, Account Balance page, No balance activity, desktop card + tile grid |
| | 1009:1836 — per-fascia frames 1357:12796–12806 | Balance card fill / button / label colour for Burton, Coast, DP, Misspap, Nasty Gal, Oasis, Principles, Wallis, Warehouse, DSGN, Brand Room; which rows each fascia carries |

## Figma companion (08 Oct 2026)

**Account 2026 `2KLlzqIWlDcri8YIHwEd63` · page "Account Icons - 08.10.26" (1900:8625).** It holds 34 frames rendered from this prototype (Jake, 08 Oct: landing only), one Figma section per fascia: Mobile 390 + Desktop 1440, with Debenhams in both Unlimited and Unlimited+. Frames are named `<Fascia> / <Mobile|Desktop> / <State>`. Text is live with the brand fonts, and the icons and logos are vectors or images. They're plain layers, not DS components.

To regenerate after a change, serve the repo on :3031 and run the snapshot builder (scratch script `snap.mjs`: Playwright renders each state, freezes the CSS for the width, inlines the fonts and images, writes ≤18 screens per HTML file). Then send each file to `html_to_figma` with `cssSelector=section.screen` and re-lay-out with `use_figma`. The script checked every frame's copyright line and state text before renaming.

## Live check (06 Oct 2026)

Every fascia's `/account` redirects to `/login` when you're signed out, so a logged-out scraper can't capture the account dashboard. The live header and USP strings for the core seven were captured and are used in the page.

## Controls

- **Top:** fascia (7 chips + More fascias) · Desktop / Mobile · width preset + drag handle · Full page / Fold (iOS Safari frame) · Export (zip: 390 + 1440 full-page PNGs, `config.json`, README with a reopen link).
- **Left (only two controls, Jake 06 Oct):** Account balance on/off (the balance card and the Account Balance row together) · Membership Unlimited / Unlimited+ (Debenhams only; other fascias show their own programme as active). Everything else is the design as is.
- State persists in localStorage and in the URL (`?s=`), so any view is shareable.

## Decisions / notes

- The 2026 balance card colours come from Figma, set as page overrides (`--ac-*`). DS `--card-bg` for the 16 non-core fascias is still the placeholder teal gradient, so these values should land in `tokens.css` when this brief merges. boohooMAN and Karen Millen have no 2026 frame and keep their DS tokens.
- Membership icon (Jake, 06 Oct): Debenhams `unlimited-infinity` / `unlimited-plus` (∞ is Debenhams only) · PLT `plt-royalty` (the Royalty emblem, ROY-EMBLEM-11) · boohoo `delivery-fast` · boohooMAN `boohooman-premier` (the P) · every other fascia the live diamond `unlimited`.
- Misspap's DS mode has `--surface-page:#000`, so the header is black. The page draws the logo in red #C22527 (masked) with inverted icons, as in the Figma frame.
- USP (08 Oct pm): the banked DS banners. `usp-live.js` and `usp.js` are mounted into `<div data-usp-banners>` under the header and nav, plus an `above` slot over the logo row; the prototype doesn't build its own bars. They're linked from this repo's `assets/ds/`, which are the same files the site serves (tag `usp-banners-2026-10-08`). A check against a bare DS-only page matched at 390 and 1440 for all seven banked fascias (Debenhams, boohoo, boohooMAN, PLT, Karen Millen, Warehouse, The Brand Room). The nine fascias not banked yet keep the prototype's strip until they're added to `usp-live.js`.
- Deliver+ banner = DS `.dplus` with the per-fascia lockups and the account copy from the Figma fascia banners ("Protect your order from £2.99…"). It's off by default.

## Open

- Nasty Gal has no logo in `assets/brands/`, so it falls back to a text wordmark.
- The Nasty Gal DS mode still uses Debenhams teal for primary actions (newsletter Subscribe).
- The app variants (App / Account / Landing with the tab bar) aren't built.
- The Beauty Club "new" rewards card (£6.18 Rewards balance) is hidden in the SEEL file. Its styling (black card, #FFD0B1 label) is inferred from the layer colours.

## Live membership audit (06 Oct 2026)

Source: the live platform code, the same build (`account/index-ZU3OXHYI`) on all 17 platform sites. It comes from each site's `__remixManifest` plus the shared fascia config chunk (`unlimitedOverrides`, `hidePremier`), with membership pages checked on every domain. Live account pages need a login, so this reads the code that draws them.

**Icon in live today (checked signed in, 08 Oct 2026; this corrects the code-only reading above):** the diamond on every fascia, except boohooMAN (the Premier P) and PLT (the old Royalty crown). The landing tiles and the mobile rows use the same mark. The label is `unlimitedOverrides.name`, otherwise "Unlimited". The row is hidden where `hidePremier` is true.

**Live account menus (signed in, 08 Oct 2026), in the order the prototype now follows:**
- Debenhams: Order History · Subscribe & Save · My Details · Addresses · Unlimited · Contact Preferences · Debenhams Mastercard
- boohoo: Order History · Subscribe & Save · My Details · Addresses · Premier · Contact Preferences
- boohooMAN / Karen Millen: Order History · My Details · Addresses · Premier · Contact Preferences
- PLT: balance card · Order History · Account Balance · My Details · Addresses · Royalty · Contact Preferences
- Coast, Oasis, Wallis: Order History · Subscribe & Save · My Details · Addresses · Unlimited · Contact Preferences
- Principles: rewards card · Order History · Subscribe & Save · Debenhams Rewards · My Details · Addresses · Unlimited · Contact Preferences
- Warehouse, Burton, DP, Misspap: Order History · My Details · Addresses · Unlimited · Contact Preferences
- The Brand Room, DSGN Studio, Training Dept: Order History · My Details · Addresses · Contact Preferences
- Debenhams Outlet: Order History · My Details · Addresses · Contact Preferences · Debenhams Mastercard (no membership)

On the non-Debenhams family sites, "Debenhams Mastercard" is a footer link, not a menu row. Account Balance appears with the balance card (the 2026 store-credit design). Live only has it where the customer has store credit (PLT today).

**Membership page `/account/unlimited` (live):** mobile has a back header plus a box: logo band, then for a non-member "Enjoy unlimited delivery for an entire year for just £14.99" (£9.99 on boohoo, boohooMAN and PLT) with ADD and FIND OUT MORE, and for a member ACTIVE, Your Membership, Expiry Date and the no-auto-renew note. Desktop shows the greeting and side menu (current page grey with a brand-colour bar) next to the box. The prototype shows the member view; the membership row clicks into it.

**Membership state (08 Oct 2026):** the shell toggles Active / Not active / Expires in 3 days on every fascia with a membership (SEEL 3525:157792 · 157039 · 157904); the tier toggle Unlimited / Unlimited+ is Debenhams only. On the row: green Active, grey Not active, red Expires in 3 days. The membership page shows the join box (price, Add, Find out more) when not active, the member view when active, and the member view with a red "Expires in 3 days", an expiry of 11/10/2026 and a Renew button when expiring. That last one is my assumption: the SEEL frames only define the row. Debenhams Unlimited+ uses its own wordmark, `assets/brands/memberships/unlimited-plus-logo.svg`.

**App tab bar (08 Oct 2026):** the DS `.app-tabbar` (catalogue `app-tabbar`, icons in `assets/ds/icons/app/`). The account page is a sub-page of Home (Best App Ever 135:8351): it has the DS nav-bar back chevron (`assets/ds/icons/app/nav-back.svg`, DS 3864:611) and Home is the active tab on every fascia. The standard bar is Account 2026 2136:198 / DS 3824:9530, with the bookmark on boohooMAN and Karen Millen (DS 9893:28665). PLT uses its labelled Best App Ever bar (HoBuVNEhf1qpL61XFipy0f 1128:225860) on a cream page. The app is always shown cropped at the fold.

**App:** the shell's Web / App toggle is phone-only. It's built from Figma `1296:69086` (status bar, centred greeting, card, divided list with chevrons plus FAQs, Help and Support and Settings, grey Sign Out, tab bar) and keeps each fascia's live menu.

| Fascia | Domain | Name in live | Info page |
|---|---|---|---|
| Debenhams | debenhams.com | Unlimited | /pages/informational/unlimited-delivery |
| Debenhams Outlet | debenhamsoutlet.com | Unlimited (Debenhams config) | unlimited-delivery |
| boohoo | boohoo.com | Premier (marketed as "Premier Club") | premier-delivery |
| boohooMAN | boohooman.com | Premier | premier-delivery |
| PLT | prettylittlething.com | Royalty | royalty |
| Karen Millen | karenmillen.com | Premier | premier-delivery |
| Burton | burton.co.uk | Unlimited | unlimited-delivery |
| Coast | coastfashion.com | Unlimited | unlimited-delivery |
| Dorothy Perkins | dorothyperkins.com | Unlimited | unlimited-delivery |
| Misspap | misspap.com | Unlimited | unlimited-delivery |
| Oasis | oasisfashion.com | Unlimited | unlimited-delivery |
| Principles | principlesfashion.com | Unlimited | unlimited-delivery |
| Wallis | wallis.co.uk | Unlimited | unlimited-delivery |
| Warehouse | warehousefashion.com | Unlimited | unlimited-delivery |
| DSGN Studio | dsgnstudio.com | **None** (`hidePremier`) | none |
| Training Dept | trainingdept.com | **None** (`hidePremier`) | none |
| The Brand Room | thebrandroom.com | **None** (`hidePremier`; a generic unlimited-delivery info page still resolves) | — |
| Nasty Gal | nastygal.co.uk | Not live ("Coming Soon"); config would show Unlimited | — |
| Maine, Gorgeous, Forever Unique | — | No live site (brand configs only, no domain) | — |

Abroad, `hidePremier` hides the row on most non-UK locales (Debenhams US/IE, boohoo outside UK and IE, PLT outside UK, FR and IE, KM outside UK and IE, every boohooMAN locale outside the UK, Nasty Gal US).

## Screens (08 Oct 2026)
Top bar **Account · PDP · Checkout**.
- **Checkout** — active member only. Live checkout layout (boohooMAN web, Debenhams app sheet) with all four delivery options kept; the new pieces from Checkout 2026 (`WChEtDPH0LcErdYFS9SESn` 3996:173990 Unlimited · 3996:174293 Unlimited+, current 3996:171295) are the membership pill on *Delivery Method* (grey Unlimited / Premier / Royalty; black→teal gradient Unlimited+) and the Deliver+ box (upsell + *Get Unlimited+* strip with Unlimited, *Included* with Unlimited+). Tier toggle stays for Debenhams; no pill for Brand Room / DSGN Studio.
- **PDP** — the core-pdp-2026 pages copied into `pdp/` (boohooMAN = new-format `pdp.html`, other fascias = live recreations `live.html` + `live-pdp.js` + `brands-live.js`; assets load from core-pdp-2026 Pages). Only change: the Debenhams membership box uses the new Unlimited wordmark (DS `assets/brands/memberships/unlimited-logo.svg`). Web only.

### 08 Oct 2026 (later)
- **New checkout** screen: Checkout 2026 3996:173492 landing (bag + express pay, Arrives/Change summary, Pennies donation, payment grid, order summary). **Change** opens the delivery-method modal (3996:173990 / 174293); all four options kept. No USP bar (as Figma).
- **Current checkout:** the membership pill sits on the right edge of the Delivery Method heading.
- **App checkout** (both): App Checkout `zGhu3eHyChNPZCHsFOmuie` 5441:420 (PLT) layout for every fascia, in that fascia's font.
- **Deliver+** in checkout for non-Debenhams fascias = the new DS checkout banner `.dplus-co` (SEEL Enhancements 2026 "Small New", own lockup / font / colour). Debenhams keeps the Unlimited / Unlimited+ member boxes from Checkout 2026.
