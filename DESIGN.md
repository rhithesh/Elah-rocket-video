# elah.dev — "Edit Bay" design system

The homepage reads like footage being cut. The page is the timeline: you scrub it by scrolling,
each section is a clip, and the one saturated colour is the colour of record lights and
playheads. Code lives in `apps/web/components/landing/home/`; tokens in `ui.ts` and
`apps/web/styles/landing.css`.

---

## 1. Principles

1. **The page is a timeline.** Scrolling scrubs it. Sections are clips, with timecode and a playhead.
2. **Neutral stage, one signal colour.** Paper and ink do the work. Cyber red only ever means
   *selected, recording, or now*.
3. **Frames, not shadows.** Structure comes from 1px hairlines and square corners. No radius,
   no drop shadows, no gradients.
4. **Mono is the machine voice.** Anything that is UI (labels, buttons, slates, timecode) is
   mono uppercase. Anything that is a statement is tall condensed display.
5. **Show the engine.** The hero stage and capability tiles are rendered by elah itself, never recorded.

---

## 2. Colour

Neutrals are CSS variables so light and dark swap in one place. Write classes as
`text-[var(--lp-ink)]`, never the raw hex.

| Variable | Light | Dark | Use |
| --- | --- | --- | --- |
| `--lp-paper` | `#F0EFEA` | `#0C0C0E` | Page background |
| `--lp-paper2` | `#E8E6E0` | `#18181B` | Hover fill |
| `--lp-card` | `#F7F6F2` | `#121215` | Cards, panels |
| `--lp-ink` | `#0E0E10` | `#EDECE7` | Text, rules, primary button |
| `--lp-muted` | `#5E5D58` | `#9C9B95` | Secondary text (5.7:1 on light paper) |
| `--lp-line` | `#D9D7D0` | `#2A2A2F` | Hairlines |
| `--lp-stage` | `#0E0E10` | `#141417` | Engine stage, closing CTA |
| `--lp-stage-line` | `#0E0E10` | `#2A2A2F` | Stage outline |

Fixed in both themes:

| Token | Hex | Use |
| --- | --- | --- |
| Cyber red | `#FF003C` | Selection box, playhead, REC dot, primary hover, motion clips |
| Red hover | `#D10030` | Pressed or hovered red fills |
| Mint | `#3DDC97` | Text and audio clips |
| Amber | `#E0A33A` | Secondary clips |
| On-stage text | `#F0EFEA` | Text on the stage and scrub bar |
| On-stage muted | `#9A9993` | Captions on the stage |
| Scrub bar | `#0E0E10` | Transport bar background |

**Rules.** Never set body text in red (3.4:1 on paper). Text on red fills is always literal ink
`#0E0E10`, in both themes. Light and dark are scoped to the homepage via
`.lp[data-theme='dark']`; the rest of the site stays dark-only.

---

## 3. Typography

Three voices.

| Voice | Face | Style | Where |
| --- | --- | --- | --- |
| **Display** | Big Shoulders, 800 | Uppercase, `leading-[0.86–0.92]`, tracking `-0.5px` | Headlines, card titles, stats, wordmark |
| **Label** | Geist Mono, 11px | Uppercase, `tracking-[0.14em]` | Nav, buttons, slates, tags, timecode |
| **Body** | Geist Sans | Sentence case, muted | Leads, card copy, table cells |

| Role | Size |
| --- | --- |
| Hero H1 | `64px` mobile, `112px` sm, `148px` lg |
| Section H2 | `44px`, `64px` sm, `80px` lg |
| CTA H2 | `52px`, `88px` sm, `120px` lg |
| Stat value | `40px`, `52px` sm |
| Card title | `26px`, `leading-none` |
| Lead | `17px / 27px` |
| Card body | `15px / 23px` |
| Label | `11px` |
| Large button | `12px` mono |

Use `!` on the display class so it beats the global `:is(h1,h2,h3,h4)` font rule.

---

## 4. Shape and layout

- **Square everywhere.** `border-radius: 0` on buttons, nav, cards, panels, chips, tiles, marks.
- **Hairline = outline.** `outline: 1px solid var(--lp-line); outline-offset: -0.5px` so frames take no layout space.
- **Container.** `max-w-[1440px]`, gutters `16 / 32 / 72px`.
- **Section rhythm.** `pb-16` and `lg:pb-[104px]`. Each section opens with its slate, then `pt-10` / `lg:pt-14` before the headline.
- **Grids.** Cards sit in hairline-bordered grids (`gap-4`), or share borders as cells (stats, footer).

---

## 5. Signature components

### Selected word — `Sel.tsx`
One word per headline is wrapped like a selected layer: `2px` red outline plus four `7px` square
handles (`paper` fill, red border) at the corners. **One per headline, never more.** Decorative;
the text reads normally.

### Slate — `Section.tsx`
Every section opens with a `1px` ink rule, then a label row:
`SC 03 · BIND` on the left and a short kicker on the right (hidden on mobile).
Props: `n`, `scene`, `kicker`. Slates are what the scrub bar uses as clips.

### Scrub bar — `ScrubBar.tsx`
A `44px` transport bar fixed to the bottom, always ink with paper text.
- **Left:** red square plus the timecode `00:MM:SS:FF`. The whole page maps to one minute at 30 fps.
- **Middle (md+):** every `[data-scene]` element is a clip, positioned and sized by its share of
  page height. A diamond marks the clip start. The active clip fills red with ink text. Click to
  jump (smooth scroll).
- **Playhead:** a `2px` red line with a triangle cap, sitting at 40% down the viewport.
- **Mobile:** collapses to a thin progress line.
- **Right (lg+):** `30 FPS`.
- **Contract:** a new section needs `data-scene="Name"` to appear on the bar.

### Viewfinder hero — `HomeHero.tsx`
Crop marks (`CropMarks`, `18px` L-brackets) frame the headline, with a faint centre cross. Above it
a row reads `● REC 00:00:04:16` on the left and the licence on the right. The timecode runs from
page load and freezes under `prefers-reduced-motion`. Below the headline: lead, primary CTA, the
install-copy button, then a full-width changelog strip.

### Program monitor
The engine stage sits in an ink frame with a header strip (`Program · hero.json`, `30 fps · 8.0 s
loop`) and a caption strip below. Text on the stage is `#F0EFEA` / `#9A9993`.

### Closing CTA — `HomeCta.tsx`
An ink stage block with inset crop marks (`#5E5D58`), a `FINAL CUT` label, a very large headline
with a selected word, a lead, and two buttons (red primary, outlined secondary).

### Footer — `HomeFooter.tsx`
Four hairline columns (brand and star button, then link groups), a `End of reel` credit strip,
then the wordmark `E L A H` set at `24–34vw`, letters spread edge to edge. The footer is
`data-scene="Credits"`.

### Nav — `HomeNav.tsx`
Sticky, `52px`, a strip of hairline cells: logo and wordmark, mono links, then (right) theme
toggle, GitHub with star count, and a solid ink `GET STARTED` cell that turns red on hover. The
background is `paper` at 88% with backdrop blur.

---

## 6. Buttons

All square, mono uppercase, `tracking-[0.12em]`.

| Variant | Style | Hover |
| --- | --- | --- |
| **Primary** | Ink fill, paper text | Red fill, ink text |
| **Secondary** | Transparent, `1px` ink border, ink text | Ink fill, paper text |
| **On stage, primary** | Red fill, ink text | Paper fill |
| **On stage, secondary** | `1px` paper border, paper text | Paper fill, ink text |

Sizes: large `h-[52px] px-6 text-[12px]`; small `h-[36px] px-4 text-[11px]`.

---

## 7. Cards, chips and tables

- **Card:** `--lp-card` fill, hairline outline, `p-6`, `gap-5`. The title is display; the body is muted.
- **Chip / tag:** `11px` mono uppercase, hairline outline, `px-[10px] py-[6px]`.
- **Code strip:** paper fill, hairline, `12px` mono.
- **Table:** hairline frame, `px-4 py-4` cells, the `elah` column header in red, first column semibold.
- **FAQ:** native `<details>`, a red `+` that rotates 45° when open.
- **Mini timelines (`MiniLanes`):** solid clips (red = motion, mint = text/audio, amber = secondary),
  ink labels, `7px` rotated-square keyframes, and a `2px` ink playhead with a triangle cap.

---

## 8. Theme

`ThemeToggle.tsx` is a moon/sun cell in the nav.
- Stores the choice in `localStorage` under `elah-lp-theme`.
- Until chosen, follows `prefers-color-scheme` and updates live.
- An inline script (`lpThemeInitScript`) is the first child of the `.lp` wrapper and sets
  `data-theme` before first paint, so there is no flash.
- Colours animate over `300ms`, disabled under reduced motion.

---

## 9. Motion

- Page-level motion is the scrub bar and the REC timecode. Everything else is still.
- The engine stage and capability tiles loop on their own.
- Transitions are `transition-colors` only. Under `prefers-reduced-motion`: the timecode freezes
  and the theme transition is off.

---

## 10. Accessibility

- Body text meets 4.5:1 in both themes (muted on paper is 5.7:1 light).
- Red is never used as a text colour for body copy. Text on red is ink.
- The scrub bar is a labelled `<nav aria-label="Page sections">`, its clips are real buttons, and
  the timecode has an `aria-label`.
- The theme toggle labels its next state ("Switch to dark mode").
- Decorative marks (`Sel` handles, crop marks, diamonds, red dots) are `aria-hidden`.
- The comparison table and the code panes are keyboard-scrollable regions.

---

## 11. Do and don't

| Do | Don't |
| --- | --- |
| One red selected word per headline | Colour whole headlines red |
| Square corners and hairlines | Radius, shadows, gradients |
| Mono uppercase for UI text | Mix sentence-case labels into strips |
| Read colours from `--lp-*` variables | Hard-code paper or ink hex in components |
| Add `data-scene` to new sections | Add a section the scrub bar can't see |
| Show real engine output | Use screen recordings or stock footage |
