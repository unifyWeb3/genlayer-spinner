# Production Validation

Validation date: 2026-08-17

This record covers the frozen **V2-B / Balanced / 1.00s** production candidate. It does not claim Portal integration.

## Automated

- V1 regression validator: `37/37` checks passed.
- V2 design validator: `50/50` checks passed.
- Production package validator: `58/58` checks passed.
- `xmllint --noout` accepted the standalone SVG file.
- Svelte 5 compilation completed with zero compiler warnings.
- A temporary production build passed with Svelte `5.56.3`, Vite `8.0.16`, and `@sveltejs/vite-plugin-svelte` `7.1.2`, matching the verified Portal frontend versions.

The checks cover fixed bounds, exact official facet coordinates, three named facets, `currentColor`, the 1.00s Balanced profile, transform/opacity-only motion, absence of rotation/scale/path morphing/filters/JavaScript timers, reduced motion, component semantics, file-size budgets, package completeness, and nonempty preview artifacts.

## Rendering

Verified with **Google Chrome for Testing 151.0.7922.34**:

| Case | Result |
| --- | --- |
| Desktop 1440 x 1000 at 1x | Passed |
| Desktop 1440 x 1000 at 2x | Passed |
| Mobile 390 x 844 at 1x | Passed |
| Sizes 16, 20, 24, 32, 48px | Exact CSS bounds at each size |
| Inline Svelte wrapper | 16/16 instances rendered at nonzero bounds |
| Normal motion | 48/48 facet animations running; sampled frames changed |
| Reduced motion | 0 facet animations; all facets aligned at opacity 1 |
| Standalone SVG | 3 polygons and 3 running animations |
| Standalone reduced motion | 0 animations; aligned transforms and opacity 1 |
| Responsive layout | Document width matched desktop and mobile viewport width |
| Browser errors | None in the clean verification run |

The rendered matrix covered black on white, white on black, accent purple, pale lavender, dark violet, dark teal, and a translucent surface. Chromium-generated review media is in `preview/`.

## Accessibility

- Fourteen semantic instances exposed one stable `role="status"` label each.
- Two decorative instances exposed `aria-hidden="true"` on the host.
- Two loading regions owned `aria-busy="true"`; the spinner did not assign it.
- The nested SVG remained decorative and unfocusable in the Svelte wrapper.
- Animation frames did not change accessible text.
- Reduced motion produced a static aligned mark while labels retained loading semantics.

This is code-level and accessibility-tree inspection in Chromium. It is not a live screen-reader runtime test.

## Manual

- The clean browser run remained active for `63.833s`; all 48 inline facet animations were still running afterward.
- A previous design-lab run observed the same motion for `69.803s`; no restart, completion pause, or animation stoppage was detected.
- The light, dark, and size preview captures were visually inspected.
- A four-frame contact sheet from the GIF confirmed that translation and opacity hand off across the unchanged three-facet silhouette.
- At 16px the full silhouette remains identifiable without detached pieces; 20-24px preserve the clearest phase relationship.

## Asset Sizes

| Asset | Size |
| --- | ---: |
| `genlayer-spinner.svg` | 2,939 bytes |
| `spinner.css` | 3,617 bytes |
| `GenLayerSpinner.svelte` | 1,211 bytes |
| `spinner-preview.gif` | approximately 17 KiB |

No production runtime dependency is introduced by the asset, CSS, or component.

## Not Verified

- Firefox runtime rendering
- Safari/WebKit runtime rendering
- Live screen-reader announcement behavior
- Rendering inside the deployed Portal
- The exact deployed `genlayer-foundation/points` commit
- Maintainer-approved component filename, token imports, and loader migration scope
- Maintainer approval for animated use of the official mark geometry

These are explicit integration or platform gaps, not implicit passes.
