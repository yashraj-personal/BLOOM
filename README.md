# BLOOM°

> *An emotional interactive digital garden.*
> *Plant something small and watch an entire botanical world bloom.*

BLOOM is an interactive single-page web experience blending Apple-level simplicity, high-fashion editorial typography, and botanical art installation aesthetics.

---

## 🌸 Key Features

- **Intro Experience**: Near-black night tone with an interactive glowing seed.
- **Instant Click, Hold & Auto-Bloom Interaction**:
  - One-tap / single-click "Click to Bloom" button for immediate, satisfying garden sprouting.
  - Optional hold-to-bloom with circular golden progress indicator, glowing dust particles, and haptic feedback.
  - Automatic gentle countdown (starts blooming on its own if left idle for 6s).
- **Cinematic Growth Sequence (8–14s)**:
  - Seed reacts and cracks open with radiant light.
  - Stems emerge upward with organic Bézier curvature.
  - Leaves unfold at stem nodes with spring physics.
  - Buds swell and peel open sepals.
  - Multi-layered flower petals unfurl across staggered intervals.
- **Procedural Botany Engine** (no two petals are ever identical):
  - Every petal outline is *generated*, not hard-coded: a width profile with a
    ruffled edge, a bent centreline and a choice of tip (round, cleft, toothed,
    pointed), smoothed through a closed Catmull-Rom spline.
  - A seeded xorshift RNG per plant drives petal count, length, width, curl and
    asymmetry, so the same garden is reproducible but never uniform.
  - Gradients are built on demand into `<defs>`: each whorl gets its own velvet
    ramp, deepened toward the throat and lit toward the tip, plus a shared
    shading overlay and a hairline edge that keeps overlapping petals legible.
  - Each bloom picks a colourway and shifts its hue a few degrees, so no two
    flowers of the same species look cloned.
- **Semi-Photorealistic Botanical Flora**:
  - **Roses**: five whorls on the golden angle, every petal curling the same way,
    closing over a dark rolled heart — the spiral, not the rosette.
  - **Sunflowers**: two rows of toothed lanceolate rays over a Fibonacci disc.
  - **Peonies**: crowded ruffles crumpling toward a golden stamen crown.
  - **Tulips**: six satin tepals closing into a veined goblet.
  - **Daisies**: slim three-toothed rays around a golden dome.
  - **Poppies**: papery crinkled cups, veined, with a charcoal basal blotch.
  - **Wildflowers**: cornflower stars with a luminous eye.
  - **Gypsophila**: airy sprays of five-petalled florets on fine branching arms.
- **Render Budget**: full geometry in the two sharp depth planes, simplified
  silhouettes behind the depth-of-field blur, and a light-render path for phones,
  low-core machines and `prefers-reduced-motion`.
- **Dynamic Lighting Transition**:
  - Deep Night → Blue Hour → Sunrise Coral/Amber → Warm Natural Morning Light.
  - The garden itself warms with the sky: brightness and saturation ride the
    same transition, so the blooms wake up rather than just sitting in a lit set.
- **Living Environmental Ambience**:
  - Continuous gentle wind sway and leaf movement.
  - 60fps Canvas particle engine for floating pollen, dust, and drifting petals.
  - Subtle pointer parallax and tilt.
- **Editable Dedication** (no link required):
  - The closing screen is never finished text — the name it is planted for and
    the words themselves are rewritten in place, in English by default.
  - Edits persist locally and are folded back into the URL, so what is on screen
    is exactly what gets shared, and the keepsake card follows along.
- **Personalized Bloom & Gifting Experience**:
  - Shareable URL parameters (`?to=Emma&from=Alex&message=You%20are%20loved&type=love`).
  - Sender remains a surprise until the garden completes its bloom.
  - Intention selector: Love, Friendship, New Beginning, Thinking of You, Birthday, Miss You, Keep Going.
- **Interactive Botanical Meaning & Easter Eggs**:
  - Hover / tap flowers to discover their poetic meanings.
  - Click flowers to release drifting falling petals.
  - Double-click/double-tap anywhere to sprout a new miniature wildflower on the spot.
  - Long-press a flower to reveal: *"Everything blooms differently."*
- **Botanical Keepsake Card Engine**:
  - High-resolution `1080x1350` digital keepsake card generated dynamically via offscreen HTML5 Canvas.
  - French luxury editorial aesthetic with gold hairline border, botanical illustration, wax seal emblem, and personalized dedication.
  - The card's centrepiece rose is drawn with the same cupped-petal geometry and
    shadowed spiral heart as the garden, tinted to the chosen intention.
  - One-tap PNG download, direct WhatsApp sharing with pre-formatted message, and native Web Share API integration.
- **4-Layer Depth & Volumetric Lighting**:
  - 4 depth planes (`layerBackground`, `layerMidBack`, `layerMidground`, `layerForeground`) with realistic depth-of-field optical blurs.
  - Crepuscular light rays (god rays) shining through morning mist.
  - Dewdrops on rose petals with specular highlights.
- **Procedural Web Audio Engine**:
  - Optional sound toggle (muted by default).
  - 100% self-contained synthesized wind ambience, opening bloom chimes, and sunrise harmonic swell via the Web Audio API (zero external `.mp3` dependencies).

---

## ⚡ Render Budget

The garden is roughly 3,900 SVG nodes. A few decisions keep that affordable:

- **Adaptive tessellation** — a petal is sampled in proportion to its size, so a
  17px heart petal doesn't get the curve segments a 92px guard petal needs.
- **Shading lives in the fill** — a radial gradient over a tall bounding box
  already *is* an axial ramp, so there is no second path per petal duplicating
  its geometry just to darken the throat.
- **No filter on the SVG root** — a root filter forces the whole tree to
  re-rasterise whenever anything sways. The light response rides on the four
  depth layers instead, so the static backdrop stays cached.
- **The blurred backdrop doesn't animate** — under 4.6px of blur nobody sees the
  motion, but everyone pays for the repaint.
- **A light-render path** for phones, ≤4-core machines and
  `prefers-reduced-motion`: same silhouettes, fewer petals.

## 🚀 How to Run

1. Open [`index.html`](file:///Users/alessiosabatino/bloom/index.html) directly in any modern browser (Safari, Chrome, Firefox, Edge).
2. Or run a local HTTP server:
   ```bash
   cd /Users/alessiosabatino/bloom
   python3 -m http.server 8765
   ```
   and navigate to `http://localhost:8765/`.

3. Try a personalized gift link:
   ```
   http://localhost:8765/?to=Emma&from=Alex&message=You%20are%20loved&type=love
   ```

---

## 📄 License

MIT — see [LICENSE](LICENSE).
