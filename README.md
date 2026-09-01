# @tnotesjs/ui

Shared Vue UI for TNotes built-in blocks. Consumed by:

- `@tnotesjs/core` VitePress theme (`tn:dev`)
- TNotes Desk (Electron visual editor)

## Package rules

- No direct `vitepress` imports in components
- Styles use `--tn-*` tokens (`src/styles/tokens.css`)
- Built-ins use short semantic names in markdown (`BilibiliVideo`, `WordList`); third-party components must use a vendor prefix
- Short one-letter tags (`B` / `E` / `N` / `F`) are **not** supported

## Install

```bash
pnpm add @tnotesjs/ui
```

Requires `vue` `^3.5` (peer).

## Local development

Sibling checkouts under `tnotesjs/` (optional `file:` while iterating):

```text
tnotesjs/ui
tnotesjs/core   # production: "@tnotesjs/ui": "^0.1.0"
tnotesjs/desk   # production: "@tnotesjs/ui": "^0.1.0"
```

```bash
cd ui && pnpm install
cd ../core && pnpm install
cd ../desk && pnpm install
```

Published packages should depend on the npm version of `@tnotesjs/ui`, not `file:../ui`.

## Components

### `BilibiliVideo` — `<BilibiliVideo id="BVxxxx" />`

| Prop | Default | Notes |
|------|---------|--------|
| `id` | required | BV id |
| `autoplay` | `false` | Embed URL sends `autoplay=0` unless enabled |
| `muted` | `false` | Embed URL sends `muted=0\|1` |

```md
<BilibiliVideo id="BV1QR4y1y7GG" :autoplay="true" :muted="true" />
```

### `WordList` — `<WordList :words="[…]" />`

| Prop | Default | Notes |
|------|---------|--------|
| `words` | `[]` | Word strings |
| `needSort` | `false` | Sort A→Z by first letter |
| `wordsBaseUrl` | en-words blob URL | Optional host override |
| `wordsRawBaseUrl` | en-words raw URL | Optional host override |
| `features` | `WORD_LIST_FEATURES_FULL` | Capability flags (see below) |

```md
<WordList :words="['cancel', 'salary']" :needSort="true" />
```

**Features presets** (no consumer/`host` field — capability-based):

| Preset | Cards | Fetch word data | Menu Pin | Menu Auto Show Card |
|--------|-------|-----------------|----------|---------------------|
| `WORD_LIST_FEATURES_FULL` (default) | ✓ | ✓ | ✓ | ✓ |
| `WORD_LIST_FEATURES_STATIC` | — | — | — | — |

### `Mermaid`

Shared diagram preview for core (`tn:dev`) and Desk. Markdown fence language: `mermaid`.

| Prop | Default | Notes |
|------|---------|--------|
| `source` | `''` | Plain Mermaid text (Desk) |
| `graph` | `''` | URI-encoded source (VitePress fence) |
| `id` | auto | Mermaid render id |
| `center` | `false` | From fence keyword `center`; omit → not centered |
| `isDark` | auto | Or pass explicitly |
| `securityLevel` | `'loose'` | Desk preview uses `'strict'` |
| `enableCopy` | `true` | Hover copy action |
| `enableFullscreen` | `true` | Hover fullscreen action |
| `enableCenterToggle` | `true` | Hover center toggle (left of fullscreen) |

Fence:

- `` ```mermaid `` → not centered  
- `` ```mermaid center `` → centered  

Icons for the toggle live in `src/components/Mermaid/icons/` (`icon__center_on.svg` / `icon__center_off.svg`).
