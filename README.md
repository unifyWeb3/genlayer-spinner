# GenLayer Spinner

### Three Perspectives, One Decision

A production-ready animated loading spinner designed for the GenLayer Portal.

![GenLayer Spinner preview](preview/spinner-preview.gif)

**[Open the interactive spinner lab →](https://unifyweb3.github.io/genlayer-spinner/demo/)**

Selected profile: **V2-B / Balanced / 1.00s**

## Why this direction

The spinner derives its geometry from the official three-facet GenLayer mark. The mark remains recognizable in every frame and in monochrome, including at compact interface sizes.

Instead of rotating the logo, the three facets move through restrained, overlapping handoffs. That creates a continuous loading rhythm while keeping the center and outer bounds stable.

The motion takes conceptual inspiration from independent perspectives moving through a coherent shared relationship. It does **not** literally depict validator voting, transaction finality, AI reasoning, or blockchain topology.

## Design principles

| Principle | Implementation |
| --- | --- |
| GenLayer identity | Three-facet official mark geometry |
| Motion | Overlapping facet handoffs |
| Loop | Seamless 1.00s cycle |
| Geometry | Translation + opacity only |
| Rotation | None |
| Scale | None |
| Path morphing | None |
| Color | `currentColor` / host-controlled |
| Accessibility | Reduced-motion static fallback |
| Small sizes | 16 / 20 / 24 / 32 / 48px |

## Technical implementation

The production package contains:

- [`genlayer-spinner.svg`](genlayer-spinner.svg): self-contained animated SVG.
- [`spinner.css`](spinner.css): reusable V2-B animation and layout rules.
- [`GenLayerSpinner.svelte`](GenLayerSpinner.svelte): minimal Svelte 5-compatible wrapper.
- No JavaScript animation loop or animation runtime dependency.

The live lab retains V1, V2-A, and V2-C for comparison. Every V2-B example uses the canonical production keyframes from the root `spinner.css` file.

## Usage

### Standalone SVG

```html
<img src="./genlayer-spinner.svg" alt="Loading" width="24" height="24">
```

The standalone asset animates without external CSS. Because an external SVG cannot inherit the host document's `currentColor`, inline SVG or the Svelte wrapper is preferred for live theme adaptation.

### Inline SVG + CSS

```html
<link rel="stylesheet" href="./spinner.css">

<span class="gl-spinner" style="--gl-spinner-size: 20px" aria-hidden="true">
  <svg class="gl-spinner__svg" viewBox="0 0 100 100" aria-hidden="true">
    <g transform="translate(5 7.7) scale(.92)">
      <g class="gl-spinner__facet gl-spinner__facet--left">
        <polygon points="44.26 32.35 27.72 67.12 43.29 74.9 0 91.93 44.26 0 44.26 32.35" />
      </g>
      <g class="gl-spinner__facet gl-spinner__facet--right">
        <polygon points="53.5 32.35 70.04 67.12 54.47 74.9 97.76 91.93 53.5 0 53.5 32.35" />
      </g>
      <g class="gl-spinner__facet gl-spinner__facet--core">
        <polygon points="48.64 43.78 58.33 62.94 48.64 67.69 39.47 62.92 48.64 43.78" />
      </g>
    </g>
  </svg>
</span>
```

Color is inherited from the parent through `currentColor`.

### Svelte

```svelte
<script>
  import GenLayerSpinner from './GenLayerSpinner.svelte';
</script>

<!-- Decorative: parent or nearby text owns the loading semantics. -->
<GenLayerSpinner size={16} />

<!-- Semantic: one stable status announcement. -->
<GenLayerSpinner size={20} label="Loading contributions" />
```

The component exposes only `size`, `label`, and the standard `class` alias.

## Accessibility

- Use decorative mode when a button, region, or nearby message already communicates loading.
- Pass `label` when the component should provide one stable `role="status"` announcement.
- Put `aria-busy="true"` on the region doing work, not on the spinner by default.
- Keep operation-specific status text in the surrounding interface.
- `prefers-reduced-motion: reduce` disables continuous motion and shows the aligned mark at full opacity.

The spinner is not intended for determinate progress, staged transaction status, errors, or timeouts.

## Validation

### Verified

- `58/58` production checks passed.
- Chromium desktop and mobile rendering.
- 1x and 2x pixel density.
- 16 / 20 / 24 / 32 / 48px sizes.
- Light, dark, monochrome, and accent contexts.
- Reduced motion.
- Standalone SVG and inline implementation.
- 63.8-second continuous browser run.
- SVG XML validation.
- Svelte 5 compilation with zero warnings.

### Not yet runtime-verified

- Firefox.
- Safari/WebKit.
- Live screen-reader behavior.
- Rendering inside the deployed Portal.

See the complete [`VALIDATION.md`](VALIDATION.md) record.

## Project structure

```text
genlayer-spinner/
├── README.md
├── genlayer-spinner.svg
├── spinner.css
├── GenLayerSpinner.svelte
├── VALIDATION.md
├── preview/
│   └── spinner-preview.gif
└── demo/
    ├── index.html
    ├── demo.css
    ├── variants.css
    └── v1.css
```

## Provenance

The facet coordinates match `GenLayer_Mark_Black.svg` from the [GenLayer Foundation design repository](https://github.com/genlayer-foundation/genlayer-design). The loading motion and implementation were created for the community mission. Animated mark usage remains subject to maintainer approval.

## Integration status

**Portal integration status: not yet integrated.** This repository contains the production-ready contribution artifact prepared for maintainer review.

The target Portal repository was identified during contribution research, but no Portal changes or pull request have been made. This repository does not claim official approval or adoption.

**Status: Ready for GenLayer Mission 12 review.**
