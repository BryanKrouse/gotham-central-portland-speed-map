# Gotham Central Web Mapping Cartography Design Schema

**Style label:** Gotham Central Police Procedural / Municipal Observation Cartography  
**Map application:** Portland speed observation web map  
**Purpose:** Create an original, interactive point-based traffic speed map that uses a Gotham Central–inspired procedural visual language while reporting transportation variables without crime or risk terminology.  
**Primary data variables:** `PostedSpeed`, `PctOverPosted`, `PctOverPosted10`  
**Schema version:** 2.1 — revised from v2 with traffic-speed outlier handling, intuitive legend intervals, thinner water treatment, and brighter subtle Portland orientation labels.

---

## Revision Notes (v1 → v2)

The following changes were made from the original schema based on design review:

1. **Water color darkened** — `#2A4351` replaced with `#162530`. Gotham's harbor reads as near-black industrial water, not decorative slate.
2. **Building mass shifted cold** — `#2A2F34` (Concrete Gray) replaced with `#252B31`. Secondary panels and block texture now carry a blue-gray bias instead of warm neutral.
3. **Road framework shifted cold** — Asphalt major roads `#3E464F` replaced with `#3A434D`; Side Street minor roads `#2F353B` replaced with `#2B3239`. The urban grid should feel cold and institutional, not warm-gray.
4. **Title typography reordered** — `Libre Baskerville` promoted to primary title font. `Cinzel` demoted to alternate. Libre Baskerville reads as worn municipal authority; Cinzel reads as elevated classical, which is slightly too decorative for a precinct document.
5. **Texture implementation specified** — Section 7 now includes a concrete canvas noise implementation pattern with pixel-level instructions. A vague opacity note at 3–6% is insufficient to achieve the worn, institutional register that distinguishes this map from a clean dark dashboard.
6. **CSS token naming noted** — Token names (`--crime`, `--police`, `--investigation`) are flavor identifiers for the palette only and must not appear in any visible UI text, legend labels, or popup content.


## Revision Notes (v2 → v2.1)

The following changes were made after dashboard review and user feedback:

1. **Traffic-speed outliers removed from analytical calculations** — exclude implausible `PostedSpeed` values of `2`, `3`, `230`, and `10316` mph before classification, legend generation, summary statistics, and charting. These values should not influence breaks, map colors, histograms, or dashboard totals.
2. **PostedSpeed legend breaks made intuitive** — use rounded transportation-friendly bins rather than raw quantile or outlier-driven class limits. Preferred default bins are `≤20`, `21–25`, `26–30`, `31–35`, and `≥36` mph after outlier removal.
3. **Water treatment narrowed** — the Willamette River and other water cues should be thin contextual features. Dark-blue water must not be so wide or visually dominant that traffic observations appear to sit in a river.
4. **Subtle Portland orientation labels added** — include restrained neighborhood, district, and major-street labels so readers can understand where they are in Portland without turning the map into a standard street map.
5. **Basemap label brightness increased** — labels should use File White at approximately `rgba(236,232,223,0.68)` with a subtle dark halo. Labels remain secondary to traffic observations but must be readable enough for orientation.

---

## 1. Design Intent

This style is designed for a dark, procedural, internal-agency mapping product. It should feel like a municipal operations plate, case-file exhibit, or observation ledger rather than a commercial GIS dashboard.

The final map should communicate:

- institutional discipline
- investigative clarity
- restrained urban atmosphere
- analytical transportation reporting
- dense point observations
- evidence-board organization
- official internal documentation

The design should be serious and grounded. It should not use superhero imagery, comic-book styling, neon effects, or theatrical crime-scene clichés.

---

## 2. Core Identity

The map should resemble a printed internal briefing document translated into an interactive web map.

It should feel:

- matte
- structured
- documentary
- worn but legible
- technical
- procedural
- compact
- data-first

The visual tone comes from cold blue-gray neutrals, low contrast, hard-edged panels, disciplined typography, and evidence-style tabular information. The dominant impression should be of a city that is cold, functional, and institutional — not warm, clean, or modern.

---

## 3. Color System

### Core Palette

| Token | Hex | Use |
|---|---:|---|
| Evidence Black | `#101214` | Page background and deepest shadows |
| Precinct Charcoal | `#181B1F` | Main map land field |
| Concrete Gray | `#252B31` | Building mass, block texture, secondary panels — cold blue-gray bias |
| Asphalt | `#3A434D` | Major road framework — cooler than neutral gray |
| Side Street | `#2B3239` | Minor roads and subdued grid lines — cold bias |
| River Dark | `#162530` | Water bodies and river corridors — near-black industrial harbor |
| File White | `#ECE8DF` | Primary text |
| Report Gray | `#B6BDC3` | Secondary text and muted annotation |
| Patrol Blue | `#536C82` | Selection, overlays, active focus |
| Evidence Amber | `#B98A34` | Highlights, headers, selected bars |
| Incident Red | `#8A2A2A` | Highest class only |
| Case Yellow | `#C8A44B` | Upper-middle value class and chart emphasis |
| Park Olive | `#4D604E` | Low value class and open-space tone |
| Border Steel | `#48505A` | Panel and popup borders |
| Ink Black | `#050607` | Symbol outlines |

### Cold Register Note

The palette should read as cold throughout. Warm gray tones will undermine the Gotham institutional atmosphere. When in doubt between a warm-neutral and a cold-neutral at any hex value, choose the cold option.

---

## 4. Variable Color Ramps

The map uses Gotham Central palette colors for the traffic variables. These colors represent **reported value classes**, not risk categories.

### PostedSpeed Ramp

Use for posted speed limits in miles per hour.

| Class | Meaning | Color |
|---|---|---:|
| 1 | Lowest posted speeds | `#4D604E` |
| 2 | Low-to-moderate speeds | `#536C82` |
| 3 | Moderate speeds | `#B98A34` |
| 4 | Higher posted speeds | `#C8A44B` |
| 5 | Highest posted speeds | `#8A2A2A` |

### PctOverPosted Ramp

Use for the percentage of recorded vehicles traveling faster than the posted speed.

| Class | Meaning | Color |
|---|---|---:|
| 1 | Lowest percentages | `#4D604E` |
| 2 | Below-middle percentages | `#536C82` |
| 3 | Middle percentages | `#B98A34` |
| 4 | High percentages | `#C8A44B` |
| 5 | Highest percentages | `#8A2A2A` |

### PctOverPosted10 Ramp

Use for the percentage of recorded vehicles traveling at least 10 mph above the posted speed.

| Class | Meaning | Color |
|---|---|---:|
| 1 | Lowest percentages | `#4D604E` |
| 2 | Below-middle percentages | `#536C82` |
| 3 | Middle percentages | `#B98A34` |
| 4 | High percentages | `#C8A44B` |
| 5 | Highest percentages | `#8A2A2A` |

### Color Behavior Rules

- Do not call classes "risk."
- Do not use traffic-light red/yellow/green language.
- Do not use rainbow ramps.
- Red is reserved for the highest observed class only.
- Amber and case yellow should feel like evidence emphasis, not decoration.
- Low values should be muted, not cheerful.
- All point symbols require a dark outline.

---

## 5. Typography

### Title Typography

Use one of:

- `Libre Baskerville` — **primary choice**; reads as worn municipal authority, institutional weight
- `Cormorant Garamond` — secondary; more refined, use if Libre Baskerville unavailable
- `Cinzel` — tertiary alternate only; avoid as first choice — too elevated and classical for a precinct document
- Georgia — fallback

Rules:

- uppercase or small caps
- 1–2 px letter spacing
- bold or semi-bold
- 30–42 px desktop
- 24–30 px mobile

### Interface Typography

Use one of:

- `IBM Plex Sans Condensed`
- `Roboto Condensed`
- `Arial Narrow`

Rules:

- uppercase section headings
- 600–700 weight
- compact line height
- restrained tracking

### Body Typography

Use one of:

- `IBM Plex Sans`
- `Source Sans 3`
- `Inter`

Rules:

- 13–15 px
- 1.45–1.55 line height
- high readability
- no rounded, friendly SaaS fonts

### Data Typography

Use:

- `IBM Plex Mono`
- `Roboto Mono`
- monospace fallback

Use for:

- summary values
- observation counts
- metadata
- variable names
- histogram ranges

---

## 6. Layout Structure

The layout should be a full-page web map composed as an internal agency plate.

Recommended structure:

```text
+------------------------------------------------------------+
| ATLAS / OBSERVATION HEADER                                 |
+--------------------------+---------------------------------+
|                          |                                 |
| LEFT CASE PANEL          |                                 |
|                          |                                 |
| Title / subtitle         |                                 |
| Variable selector        |             MAP FIELD           |
| Persistent definitions   |                                 |
| Summary table            |                                 |
| Legend                   |                                 |
| Histogram                |                                 |
| Histogram readout        |                                 |
| Metadata / sources       |                                 |
+--------------------------+---------------------------------+
```

### Layout Rules

- Use square panels only.
- No rounded cards.
- No glassmorphism.
- No large drop shadows.
- Map field should occupy most of the screen.
- Sidebar should feel like a case-file column.
- All important interpretation must be visible without hover.
- Popup interaction may add detail but must not be the only explanation.

---

## 7. Basemap Design

The map uses a custom canvas-style basemap rather than relying on an external tile service. This prevents external basemap load failures and keeps the map self-contained.

### Basemap Characteristics

- cold matte land field with blue-gray bias
- near-black industrial water
- cold road and grid framework
- faint block texture in cold concrete
- worn paper grain and subtle blueprint-style grid
- no bright commercial labels
- no external basemap dependency required
- city extent derived from the data bounds

### Land

Use `#181B1F` as the dominant land field.

### Water

Use `#162530`. Water must read as cold, industrial, and dark — close to black. It should not appear decorative or coastal-vacation blue. Gotham's harbor and river are functional infrastructure, not scenic elements.

Water features must be visually restrained. In the Portland dashboard, the Willamette River and any other water corridors should be drawn as thinner contextual ribbons rather than broad filled shapes. The water should orient the reader but never dominate the data layer or create the impression that traffic observations are located in the river. Recommended canvas stroke or simplified-water width: about `4–8 px` at the default citywide extent, tapering or scaling down at smaller screens.

### Roads and Grid

Major framework lines: `#3A434D`  
Minor grid lines: `#2B3239`  
Opacity should remain low. Grid should support orientation without pretending to be exact road data.

### Subtle Orientation Labels

The basemap should include a small number of subtle Portland identifiers to help readers understand location context:

- major streets and corridors
- river orientation labels only if they do not compete with data
- neighborhood or district names
- civic anchors where helpful

Label color should be File White at approximately `rgba(236,232,223,0.68)`, slightly brighter than the original subdued treatment. Use a subtle dark halo or shadow, such as `rgba(5,6,7,0.75)` at `1–2 px`, so labels remain legible over roads and water. Labels must remain secondary to point observations: small size, low density, no bright glow, no heavy outlines, and no standard commercial street-map styling.

---

## 7a. Texture Implementation

This section replaces the vague "3–6% opacity paper grain" note from v1 with a concrete canvas implementation pattern. Without pixel-level specification, the texture will render imperceptibly and the map will read as a clean modern dark dashboard rather than a worn municipal plate.

### Required Texture Layers

Apply in order, composited over the basemap before data points are drawn.

#### Layer 1 — Base Noise Grain

```javascript
function applyFilmGrain(ctx, width, height) {
  const imageData = ctx.getImageData(0, 0, width, height);
  const data = imageData.data;
  for (let i = 0; i < data.length; i += 4) {
    const noise = (Math.random() - 0.5) * 18; // grain amplitude: 14–22 recommended
    data[i]     = Math.min(255, Math.max(0, data[i]     + noise));
    data[i + 1] = Math.min(255, Math.max(0, data[i + 1] + noise));
    data[i + 2] = Math.min(255, Math.max(0, data[i + 2] + noise));
    // alpha unchanged
  }
  ctx.putImageData(imageData, 0, 0);
}
```

Apply after the land fill and before roads. This adds per-pixel randomness that prevents the map from reading as flat digital fill.

#### Layer 2 — Blueprint Grid Overlay

```javascript
function applyBlueprintGrid(ctx, width, height) {
  ctx.save();
  // Major grid lines
  ctx.strokeStyle = 'rgba(83, 108, 130, 0.06)'; // Patrol Blue at very low alpha
  ctx.lineWidth = 1;
  const majorSpacing = 80;
  for (let x = 0; x < width; x += majorSpacing) {
    ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, height); ctx.stroke();
  }
  for (let y = 0; y < height; y += majorSpacing) {
    ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(width, y); ctx.stroke();
  }
  // Minor grid lines
  ctx.strokeStyle = 'rgba(83, 108, 130, 0.03)';
  const minorSpacing = 20;
  for (let x = 0; x < width; x += minorSpacing) {
    ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, height); ctx.stroke();
  }
  for (let y = 0; y < height; y += minorSpacing) {
    ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(width, y); ctx.stroke();
  }
  ctx.restore();
}
```

#### Layer 3 — Vignette Edge Darkening

```javascript
function applyVignette(ctx, width, height) {
  const gradient = ctx.createRadialGradient(
    width / 2, height / 2, height * 0.3,
    width / 2, height / 2, height * 0.85
  );
  gradient.addColorStop(0, 'rgba(0,0,0,0)');
  gradient.addColorStop(1, 'rgba(0,0,0,0.28)');
  ctx.fillStyle = gradient;
  ctx.fillRect(0, 0, width, height);
}
```

Apply last, after data points are drawn. The vignette reinforces the plate/document framing and darkens the map edges so the eye remains on the data field.

### Texture Calibration Notes

- Grain amplitude of 14–22 is correct for this map scale. Below 12 is invisible at typical monitor brightness. Above 26 obscures point patterns.
- Blueprint grid at 6% alpha for major lines, 3% for minor lines. These values are intentionally subtle — they suggest municipal structure without competing with data symbols.
- Do not apply CSS `filter: noise()` or `backdrop-filter` as a substitute. Canvas pixel-level noise renders at screen resolution and behaves correctly on high-DPI displays; CSS filter results vary by browser.
- Regenerate grain on each full redraw, not each frame. Static grain is correct for a printed-document aesthetic.

---

## 8. Traffic Count Symbols

### Geometry

Use circles.

### Size

Default radius:

- 4–7 px for dense full-extent view
- larger only on selection or hover

### Stroke

Use:

- stroke color: `#050607`
- stroke width: 1.25–2 px
- matte fill
- no glow

### Opacity

Use:

- fill opacity: 0.78–0.88
- stroke opacity: 0.9–1.0

### Selection State

Selected point:

- larger radius
- amber or patrol-blue outline
- slightly stronger stroke
- no pulsing animation

---

## 9. Variable Definitions

Always display the three definitions persistently in the sidebar.

### PostedSpeed

Posted speed limit at the traffic count location, in miles per hour.

### PctOverPosted

Percentage of recorded vehicles traveling faster than the posted speed.

### PctOverPosted10

Percentage of recorded vehicles traveling at least 10 mph above the posted speed.

---

## 10. Summary Table

The summary table reports descriptive statistics for the active variable.

Recommended rows:

| Label | Meaning |
|---|---|
| Observations | Number of mapped records with valid geometry and valid active-variable value |
| Average | Arithmetic mean of the active variable |
| Median | Middle value of the active variable |
| Highest observed value | Largest observed value in the dataset for the active variable |

Do not label the final row only as "Max." Use **Highest observed value** so the statistic is self-explanatory.

---

## 11. Legend Design

The legend should describe the active variable only.

### Required Elements

- active variable name
- 5 color classes
- value ranges
- statement that colors represent reported values
- no risk wording

### Default Break Strategy

Legend breaks should be intuitive and stable after outlier removal. Do not let implausible records control the legend.

For `PostedSpeed`, use rounded speed-limit classes:

| Class | Range |
|---|---:|
| 1 | `≤20 mph` |
| 2 | `21–25 mph` |
| 3 | `26–30 mph` |
| 4 | `31–35 mph` |
| 5 | `≥36 mph` |

For percentage variables (`PctOverPosted`, `PctOverPosted10`), use clean rounded intervals that reflect the valid distribution. Recommended default:

| Class | Range |
|---|---:|
| 1 | `0–10%` |
| 2 | `10–25%` |
| 3 | `25–50%` |
| 4 | `50–75%` |
| 5 | `75–100%` |

If the valid data range is narrower than these bins, compress gracefully to rounded, reader-friendly intervals. Avoid raw quantile labels with long decimals.

### Legend Style

- hard-edged frame
- dark panel background
- small circular swatches
- compact data text
- muted gray supporting note
- amber rule line or heading accent

---

## 12. Histogram Design

The histogram supports interpretation of the active variable distribution.

### Visual Style

- dark chart background
- amber/case-yellow bars
- steel-gray gridlines
- monospace axis labels
- square frame
- no rounded bars
- no rainbow colors

### Interaction

Histogram bars must be clickable.

When a bar is clicked, display a readout containing:

- selected range
- count of observations in the bin
- percentage of active-variable records
- active variable name

Optional behavior:

- temporarily emphasize mapped points that fall in the selected bin
- keep the readout persistent until another bar is clicked

### Required Readout Language

Use neutral reporting language such as:

> Selected bin: 25–30  
> Records in range: 1,245  
> Share of valid observations: 6.4%

Avoid:

- danger
- risk
- critical
- alert
- violent
- crime

unless the underlying dataset is actually crime data.

---

## 13. Popup Design

Popups should resemble compact observation notes.

### Style

- square charcoal panel
- 1px steel border
- amber header strip
- file-white text
- muted gray labels
- compact table structure

### Required Fields

- Location or description, if available
- PostedSpeed
- PctOverPosted
- PctOverPosted10

### Fields to Exclude

Do not show:

- latitude
- longitude
- raw projected coordinates
- internal geometry fields
- unnecessary technical fields

### Popup Tone

Use:

- "Observation Record"
- "Traffic count location"
- "Reported value"

Avoid:

- incident
- crime
- suspect
- homicide
- emergency

unless the data actually supports those terms.

---

## 14. Interaction Model

Interaction should feel investigative but not playful.

### Required Interactions

- variable selector changes symbol color classes
- summary table updates with selected variable
- legend updates with selected variable
- histogram updates with selected variable
- histogram bars are clickable
- map points are clickable
- selected popup displays traffic values

### Optional Interactions

- search by location description
- filter by histogram bin
- reset selection
- show top observed values table
- export selected observations

### Avoid

- playful bouncing markers
- glowing animations
- spinning loaders
- confetti effects
- cartoon hover states
- unnecessary transition effects

---

## 15. Removed Elements

Do **not** include:

- scale bar
- north arrow

These were intentionally removed because the user requested a cleaner procedural dashboard.

---

## 16. CSS Design Tokens

Token names ending in `--crime`, `--police`, and `--investigation` are palette flavor identifiers only. They must not appear in any visible UI text, legend labels, popup content, or ARIA labels. They are internal naming conventions for the color system.

```css
:root {
  /* Background and surface */
  --bg:               #101214;
  --land:             #181B1F;
  --building:         #252B31;   /* v2: cooler blue-gray, was #2A2F34 */
  --road-major:       #3A434D;   /* v2: cold bias, was #3E464F */
  --road-minor:       #2B3239;   /* v2: cold bias, was #2F353B */
  --water:            #162530;   /* v2: near-black industrial harbor, was #2A4351 */

  /* Text */
  --text:             #ECE8DF;
  --text-secondary:   #B6BDC3;

  /* UI states */
  --police:           #536C82;   /* palette token only — not for visible labels */
  --border-color:     #48505A;
  --ink:              #050607;

  /* Data emphasis */
  --amber:            #B98A34;
  --crime:            #8A2A2A;   /* palette token only — not for visible labels */
  --investigation:    #C8A44B;   /* palette token only — not for visible labels */
  --park:             #4D604E;

  /* Typography */
  --font-title:  "Libre Baskerville", "Cormorant Garamond", Georgia, serif; /* v2: LB primary */
  --font-ui:     "IBM Plex Sans Condensed", "Arial Narrow", sans-serif;
  --font-body:   "IBM Plex Sans", Inter, sans-serif;
  --font-mono:   "IBM Plex Mono", "Roboto Mono", monospace;

  /* Structure */
  --radius:          0px;
  --border:          1px solid #48505A;
  --panel-padding:   12px 14px;
  --texture-opacity: 0.05;
}
```

---

## 17. HTML Component Requirements

A reproducible implementation should include:

```text
<header class="atlas-header">
  plate label
  map title
  subtitle
</header>

<aside class="case-panel">
  variable selector
  definitions
  summary table
  legend
  histogram
  histogram readout
  source block
</aside>

<main class="map-stage">
  canvas basemap
  canvas texture (grain + grid + vignette — see Section 7a)
  canvas data layer
  popup layer
</main>
```

### Required Metadata

Include metadata in the HTML:

```html
<meta name="description" content="Interactive Portland traffic speed observation map using Gotham Central procedural cartography.">
<meta name="keywords" content="traffic speed, Portland, canvas map, procedural cartography, transportation observations">
<meta name="orig_prompt" content="Using the Gotham Central web mapping cartography design schema v2, create an HTML interactive map using the Portland data and the three variables.">
```

---

## 18. JavaScript Behavior Requirements

### Data Handling

The implementation should:

- embed the CSV or preprocessed JSON in the HTML for single-file operation
- parse `PostedSpeed`, `PctOverPosted`, and `PctOverPosted10` as numbers
- exclude records with invalid coordinates from rendering
- remove implausible `PostedSpeed` outliers before analysis and rendering
- preserve original values for popups only for records that pass validation
- compute statistics dynamically from valid active-variable values

For the Portland traffic speed dataset, exclude records where `PostedSpeed` equals `2`, `3`, `230`, or `10316` mph. These values are considered data-quality outliers and must not influence:

- map rendering
- active-variable classification
- legend breaks
- summary statistics
- histograms
- dashboard totals
- popup availability

### Coordinate Handling

If input coordinates are projected Web Mercator meters:

- convert x/y to longitude/latitude
- project geographic coordinates into screen space based on data bounds
- maintain aspect ratio
- pad extent so symbols are not clipped

### Rendering

Use canvas when point counts exceed several thousand records.

Canvas layer should render in this order:

1. Procedural basemap (land, water, roads)
2. Texture layers (grain, blueprint grid) — see Section 7a
3. Point observations
4. Selection highlight
5. Vignette — see Section 7a

This draw order ensures texture sits between basemap and data, and vignette frames the completed map field.

---

## 19. Accessibility

The map should remain usable without relying only on color.

Recommended support:

- value ranges in legend
- numeric popup values
- histogram count labels or readout
- high-contrast text
- no hover-only meaning
- keyboard-accessible controls where possible

---

## 20. Agent Prompt

Create a single-file interactive HTML web map using Portland traffic speed count data and the variables `PostedSpeed`, `PctOverPosted`, and `PctOverPosted10`. Remove implausible `PostedSpeed` outliers of `2`, `3`, `230`, and `10316` mph before map rendering, classifications, summaries, legends, histograms, and popups. Use intuitive rounded legend breaks, especially for `PostedSpeed`. Use an original Gotham Central police-procedural cartographic style with a cold blue-gray palette, thin near-black industrial water, subtle brighter Portland orientation labels, and a worn institutional atmosphere. Report the data as transportation observations rather than crime or risk. Use a dark matte self-contained basemap with canvas-rendered pixel-level grain noise, a blueprint grid overlay at low opacity, and a vignette edge-darkening layer. Use muted institutional colors with cold bias throughout, square information panels, compact typography with Libre Baskerville as the title font, and heavy outlined circular symbols. The map must include persistent definitions, active-variable legend, dynamic summary table, clickable histogram bars with a readout, and compact popups that show the three traffic variables but not latitude or longitude. Do not include a scale bar or north arrow. Avoid superhero imagery, neon cyberpunk, comic-book effects, rounded cards, consumer dashboard styling, warm neutral grays, and decorative water colors.

---

## 21. Hard Rules

1. Use Gotham Central palette colors for symbols.
2. Do not use the word "risk" for the Portland traffic variable legend.
3. Do not show latitude or longitude in popups.
4. Rename "Max" as "Highest observed value."
5. Make histogram bars clickable and provide range/count details.
6. Keep the map self-contained if external basemaps are unreliable.
7. Use canvas rendering for large point datasets.
8. Use square panels only.
9. Keep animations minimal.
10. Preserve analytical clarity over atmosphere.
11. Do not include scale bar or north arrow.
12. Avoid superhero branding or protected imagery.
13. Water must render as near-black industrial harbor, not decorative blue.
14. All gray tones must carry a cold blue bias, not warm neutral.
15. Apply canvas pixel-level grain noise per Section 7a — CSS filter substitutes are not acceptable.
16. CSS palette token names (`--crime`, `--police`, `--investigation`) must never appear in visible UI text.

---

## 22. Quality Checks

A successful map should satisfy the following:

- The dashboard opens by double-clicking the HTML file.
- The data renders without requiring a local server.
- The basemap and data are visible even without external tile services.
- Symbol colors match the Gotham Central color palette.
- The active variable is clear.
- The legend matches the selected variable.
- Histogram bars respond to clicks.
- The popup reports only relevant traffic attributes.
- The interface feels like an internal municipal observation ledger.
- The map does not appear to be a generic dark GIS dashboard.
- The water reads as cold and near-black, not decorative.
- The basemap reads as worn, not flat and digital.
- All gray surfaces carry a cold bias — no warm taupe or brown-gray tones.

---

## 23. Negative Prompt

Avoid neon colors, cyberpunk lighting, superhero logos, bat symbols, comic-book panels, glassmorphism, rounded cards, glossy gradients, fantasy architecture, Halloween themes, consumer dashboard aesthetics, traffic-light color schemes, rainbow ramps, excessive glow, decorative crime-scene tape, emoji markers, hover-only interpretation, warm neutral grays, decorative coastal water colors, and any basemap so dark that the point pattern becomes unreadable.

---

## 24. License

Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0).

This specification is an original cartographic design guide inspired by broad procedural, municipal, noir, and internal-agency mapping traditions. It does not authorize copying protected artwork, logos, character imagery, production designs, or trade dress.