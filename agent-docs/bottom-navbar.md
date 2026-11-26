# Bottom navbar

> The tab bar at the bottom of the app for moving between its main sections. Mutual Fund and F&O have their own sub-navs with a Home item back to the main bar.

- Group: Navigation
- Lifecycle: wip
- Status: Figma synced
- Version: 1.2.0
- Figma: https://www.figma.com/design/lxQ6QIXGOv5mmx0khh5sJn/?node-id=4543-61961
- Source: `src/components/BottomNavbar`
- Also called: Bottom navigation, tab bar, nav bar, bottom tabs, dock

## Import

```tsx
import { BottomNavbar, NavIcon, navIconNames } from './components/BottomNavbar' // path relative to src/
```

## Overview

### Main nav and sub-navs

The main bar has Stocks, Market, Portfolio, Mutual Fund and F&O. Mutual Fund and F&O each have their own bar, which starts with a Home item and a separator to get back. Tap Mutual Fund in the demo above to try it.

The main bar has Stocks, Market, Portfolio, Mutual Fund and F&O. Mutual Fund and F&O each have their own bar. Pass `home` to add the Home item and the separator after it. Tap Mutual Fund in the demo above to try it.

### Moving between navs

When the options change, the bar animates. The option you tapped glides into its new slot, and the rest slide in one after another from the direction you're going: from the right into a sub-nav, from the left back Home. The animation uses the motion tokens, and it's turned off when the device is set to reduce motion.

### Floating

A floating version, after the Minted app: the bar becomes a pill 16 in from the sides and 14 up from the bottom, with a soft green glow behind the current option. The page scrolls on under it and fades into the screen's colour near the bottom. It's being tried out in code and isn't in Figma yet.

Pass `variant="floating"`. It takes no height: the page runs on under the pill, so its scrolling content must end 70 (14 + the 56 pill) above its usual end. The frame is marked `data-bottom-navbar="floating"` for that. Not in Figma yet.

### Nav icons

The nav icons are custom artwork. Unselected icons are one color and follow the theme; selected icons are two-tone brand artwork with fixed colors, so they look the same in every theme. Any other icon is a Material Symbol in content-tertiary, or success green when selected.

`NavIcon` is Figma's nav icon set. Unselected icons are one color, with the tertiary and secondary parts built into the artwork, and follow the theme. Selected icons are two-tone brand artwork with fixed colors, so they look the same in every theme. For any other icon, pass a Material Symbol with `<Icon>`: it's shown in content-tertiary, or success green when selected.

### Accessibility

Every option always shows its label, and the current one is marked for screen readers. The bar stays at the bottom of the screen and leaves room for the phone's home indicator.

The bar is a `<nav>` landmark. Give it a name with `aria-label`. Each option is a button, or a link when you pass `href`. The current option is marked with `aria-current="page"`, and the label is always shown. With `fixed`, the bar sticks to the bottom of the screen and adds space for the home indicator.

## Do / Don't

### Only top-level sections

- ✅ **Do:** Three to five main sections, always with labels.
- ❌ **Don't:** Put actions (like Buy) or more than five items in the bar.

## Options (tree)

Bottom navbar — App sections, 3–5 items

- **Item set** — Which part of the app
  - `main` — Top-level sections, always labelled.
  - `sub-nav + home` — MF / F&O sections with a way back home.
- **Rules**
  - `no actions` — Never Buy or other actions in the bar; never more than five items.
  - `aria-current` — The current section is marked for screen readers.

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `items` | `BottomNavbarItem[]` |  | { value, label, icon, selectedIcon?, href? }. Icons are 24px. |
| `value` | `string` |  | The current section (Figma Tab / isActive). |
| `onChange` | `(value) => void` |  | Called when an option is tapped. |
| `home` | `{ label?, onClick?, href? }` |  | Figma MF / F&O sub-navs: a Home item (back-home icon) and a separator. The label defaults to 'Home'. |
| `aria-label` | `string` | `'Main'` | Name of the nav landmark. |
| `fixed` | `boolean` | `false` | Fix the bar to the bottom of the viewport and add the safe-area inset. |
| `variant` | `'docked' \| 'floating'` | `'docked'` | docked: the Figma bar. floating: a pill over a fade (code only, not in Figma yet). It takes no height, so the page under it must end 70 higher (14 + 56). |
| `NavIcon` | `{ name: NavIconName; selected? }` |  | Figma .L3: base navicons: stocks, market, portfolio, mutualFund, fno, mfFunds, mfDashboard, mfSips, fnoOptionChain, fnoPositions, fnoScalper, backHome. |

## Tokens used

- `surface/primary`
- `border/light`
- `content/tertiary (unselected)`
- `content/accent/success-default (selected)`
- `content/primary (nav icon mask)`
- `Label/10`
- `size/64`
- `spacing/04 · 10`
- `icon-size/24`
- `shadow/elevation-medium`
- `state-layer/dark/*`

## Recent changes

- **1.2.0** (2026-11-20) Floating version: A floating version, after the Minted app: a pill 16 in and 14 up, a soft green glow behind the current option, and the page fading into the screen colour under it. Code only, not in Figma yet. variant="floating" (default 'docked'). It takes no height: the page under it must end 70 (14 + 56) higher; the frame is [data-bottom-navbar="floating"].
- **1.1.0** (2026-10-05) New type weights: Text uses the three typography roles: titles Heading (750), labels Label (650).
- **1.0.1** (2026-10-04) Typography tokens renamed: Text tokens renamed to the Figma roles (e.g. --l3-text-label-12). No visual change.
