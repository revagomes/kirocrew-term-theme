# Kiro Crew Term (v3) 👻

A Kiro Crew dashboard theme that mirrors the look of **kiro-cli v3** (the
refreshed `--tui` terminal experience): a near-black terminal canvas, the Kiro
violet accent (`#c6a0ff`), ANSI-styled status and diff colors, and a
mono-forward type system.

- **Level:** 1 (colors + fonts + scoped structural CSS)
- **Fonts:** [Inter](https://github.com/rsms/inter) (sans) and
  [JetBrains Mono](https://github.com/JetBrains/JetBrainsMono) (mono + code),
  both SIL Open Font License 1.1.
- **Palettes:** `dark` (the v3 dark terminal) and `light` (the v3 light/safe
  variant).

## Design direction

The image below is the **target aesthetic** for the theme across the main
dashboard screens — flat fills, 0px radius, hard 1px borders, ANSI accents, a
`❯` prompt and block caret.

![Kiro Crew Term (v3) — design direction across the dashboard screens](.github/preview/preview.png)

> **What this pack delivers.** Palette, fonts, **and the flat/sharp shape** —
> all from the pack itself, installed once via Settings → Display. The
> structural CSS in `styles/overrides.css` zeroes the dashboard's own
> `--radius-*` tokens (which its utility classes resolve through), so every
> rounded surface squares in one move, with hard 1px borders and a faint
> terminal grain on top. No per-browser userstyle or DevTools paste is needed
> for the shape anymore; the companion userstyle below remains only as an
> optional belt-and-braces layer.

## Install

Settings → Display → Install theme, then paste either:

- this repo URL (`https://github.com/revagomes/kirocrew-term`), or
- the local folder path if you have it checked out.

Re-installing overwrites the previous copy — that is the update path.

## What it themes

- Palette of 37 variables per polarity (only the three required vars are
  mandatory; the rest are tuned so surfaces, borders, JSON syntax, and terminal
  hues read like the v3 TUI). Diff colors are left to the dashboard to
  auto-derive from each polarity.
- Sans face → Sans option; Mono face → Mono option **and** all code surfaces.
- `styles/overrides.css` applies the flat/sharp language across the whole
  dashboard by zeroing its `--radius-*` token scale (`--radius-sm` … `--radius-3xl`)
  on `:root` plus a `*` radius sweep, so every rounded surface squares at once.
  It then drops soft shadows for crisp seams, outlines the primary action
  (`.btn-sweep`) with a hard accent border, squares the composer, sets the
  message-wrapper padding (`.message-bubble.msg-content`), and lays a faint
  terminal grain over `body`. These target the dashboard's real DOM (its utility
  classes and radius tokens), not placeholder class names — so the shape
  actually lands on install.

## Flat/sharp shape — companion userstyle (optional, legacy)

The pack now ships the flat/sharp shape itself (see above), so this userstyle is
**no longer required** — it predates in-pack structural CSS and is kept as an
optional per-browser layer (e.g. if you run the dashboard under an origin the
pack's radius-zeroing somehow doesn't reach). To use it:

1. Install a userstyle manager — [Stylus](https://add0n.com/stylus.html)
   (Chrome/Firefox) is recommended.
2. Open `.github/userstyle/kirocrew-term.user.css` from this repo and install it
   (Stylus detects the `==UserStyle==` header), **or** paste its contents into a
   new Stylus style scoped to your dashboard origin.
3. Adjust the `url-prefix(...)` lines at the top if your dashboard runs on a
   host/port other than `localhost:5476`.

How it works: it applies the same radius-zeroing as the pack's
`styles/overrides.css` (zero the `--radius-*` vars the dashboard rounds
through). Since the pack already does this on install, the userstyle is
redundant on a current Kiro Crew — it is retained for older builds or
non-standard origins.

### Desktop app (Electron)

The pack's in-pack shape installs natively in the desktop app too, so the
DevTools route below is now a **legacy fallback** — only needed on an older Kiro
Crew that predates Level 1 structural CSS. If you want it anyway (DevTools must
be enabled):

1. Open DevTools in the desktop app.
2. Paste the contents of `.github/userstyle/console-inject.js` into the **Console** and
   press Enter — the app goes flat/sharp immediately.
3. Not persistent across restarts. To avoid re-pasting, save it once as a
   **DevTools Snippet** (Sources → Snippets) and run it after each launch.

The snippet injects the same radius-zeroing CSS as the userstyle. For a
fully set-and-forget experience, run the dashboard in a browser with Stylus —
the desktop app has no supported auto-load hook, and patching its bundled
assets is unsupported and breaks on update.

## Notes

- The System font option always stays the OS font; a theme pack cannot change
  it, by design.
- Fonts are declared only through the role system in `theme.json`; none are set
  in CSS (the runtime rejects that).

## License

Theme sources: MIT. Bundled fonts: SIL OFL 1.1. See `LICENSE.txt`.
