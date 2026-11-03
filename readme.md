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

> **What this pack delivers.** The full palette and fonts everywhere, plus the
> flat/sharp language (0px radius, hard 1px borders, terminal grain) on the six
> surfaces a theme pack is allowed to reach: the topbar, sidebar, chat
> container, message bubbles, composer, and code blocks. Kiro Crew enforces a
> **runtime selector allowlist** — an `overrides.css` rule aimed at anything
> else (a utility class, `*`, `:root`) is silently dropped — so a pack cannot
> zero the dashboard's global radius tokens or restyle arbitrary components. To
> flatten the remaining rounded chrome (cards, chips, pills, tab strips), use
> the companion **userstyle** below, which runs browser-side and is not bound by
> the allowlist. Pack = color + fonts + sanctioned-surface shape; userstyle =
> the rest of the shape.

## Install

Settings → Display → Install theme, then paste either:

- this repo URL (`https://github.com/revagomes/kirocrew-term-theme`), or
- the local folder path if you have it checked out.

Re-installing overwrites the previous copy — that is the update path.

## What it themes

- Palette of 37 variables per polarity (only the three required vars are
  mandatory; the rest are tuned so surfaces, borders, JSON syntax, and terminal
  hues read like the v3 TUI). Diff colors are left to the dashboard to
  auto-derive from each polarity.
- Sans face → Sans option; Mono face → Mono option **and** all code surfaces.
- `styles/overrides.css` applies the flat/sharp language on the six surfaces the
  runtime allows a pack to target: 0px radius + hard borders on `.topbar`,
  `.sidebar`, `.chat-container`, `.message-bubble`, `.input-area` and
  `.code-block`, an accent underline on the topbar, a left accent caret-rail on
  the composer (`.input-area:focus-within`), message-wrapper padding
  (`.message-bubble.msg-content`), a flat `button.primary`, and a faint terminal
  grain on `body`. The dashboard drops any rule outside its allowlist (no `*`,
  no `:root`, no utility classes), so these are the only surfaces a pack can
  reach — the userstyle below covers the rest.

## Flat/sharp shape — companion userstyle (for the rest of the dashboard)

The pack flattens the six surfaces it is allowed to target, but the dashboard's
other rounded chrome (cards, chips, status pills, tab strips) lives on
framework utility classes a theme pack **cannot** reach — Kiro Crew's runtime
drops any `overrides.css` rule outside its selector allowlist, including the
`:root` radius-token zeroing that would otherwise square everything. To flatten
that remaining chrome, install the companion **userstyle**, which runs
browser-side and is not bound by the allowlist:

1. Install a userstyle manager — [Stylus](https://add0n.com/stylus.html)
   (Chrome/Firefox) is recommended.
2. Open `.github/userstyle/kirocrew-term.user.css` from this repo and install it
   (Stylus detects the `==UserStyle==` header), **or** paste its contents into a
   new Stylus style scoped to your dashboard origin.
3. Adjust the `url-prefix(...)` lines at the top if your dashboard runs on a
   host/port other than `localhost:5476`.

How it works: the dashboard's rounded corners resolve through its own
`--radius-*` CSS variables. A theme pack cannot touch those (the runtime drops
`:root` rules), but a browser-side userstyle can — it zeroes `--radius-lg`,
`--radius-xl`, etc. and squares every surface the pack couldn't reach, in one
move. It changes **shape only**; the palette, fonts, and the six sanctioned
surfaces still come from the pack, so the two layers compose.

### Desktop app (Electron)

The desktop app has no custom-CSS setting and can't load a Stylus userstyle, so
to flatten the chrome the pack can't reach, use its **DevTools** (DevTools must
be enabled):

1. Open DevTools in the desktop app.
2. Paste the contents of `.github/userstyle/console-inject.js` into the **Console** and
   press Enter — the app goes flat/sharp immediately.
3. Not persistent across restarts. To avoid re-pasting, save it once as a
   **DevTools Snippet** (Sources → Snippets) and run it after each launch.

The snippet injects the same radius-zeroing CSS as the userstyle, flattening the
chrome the pack cannot. For a fully set-and-forget experience, run the dashboard
in a browser with Stylus — the desktop app has no supported auto-load hook, and
patching its bundled assets is unsupported and breaks on update.

## Notes

- The System font option always stays the OS font; a theme pack cannot change
  it, by design.
- Fonts are declared only through the role system in `theme.json`; none are set
  in CSS (the runtime rejects that).

## License

Theme sources: MIT. Bundled fonts: SIL OFL 1.1. See `LICENSE.txt`.
