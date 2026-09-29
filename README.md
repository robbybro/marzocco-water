# Espresso Machine Water Profile

Interactive calculator for DIY coffee water, in two tabs:

- **Espresso** — water that stays inside [La Marzocco's water spec](https://lamarzoccousa.com/wp-content/uploads/2023/09/Water-Specifications.pdf), built for a Linea Mini fed from 1-gallon jugs of distilled water.
- **Pourover** — Seattle tap (Cedar or Tolt) brought up to a filter-coffee target with the same two concentrates.

**Live:** https://robbybro.github.io/marzocco-water/

## Espresso tab

- Sliders for **total hardness** (70–100 ppm as CaCO₃), **alkalinity** (40–80 ppm as CaCO₃), and **batch size**
- Recalculates **Epsom salt (MgSO₄·7H₂O)** and **baking soda (NaHCO₃)** doses in grams, plus mL doses of two stock concentrates for better accuracy on a 0.1 g scale
- Live **spec check** against La Marzocco's published limits (hardness, alkalinity, chloride, TDS, pH)
- **Flavor descriptors** — how each profile reads in the cup (brightness, sweetness, body, harshness risk)
- **Shareable profiles** — the sliders are mirrored into the URL, so any dialed-in profile is a link you can send or save as a note

## Espresso share links

The three sliders fully determine the page, so they're the whole payload:

```
?hardness=88&alkalinity=61&batch=2
```

| Param | Range | Step | Default |
| --- | --- | --- | --- |
| `hardness` | 70–100 | 1 | 75 |
| `alkalinity` | 40–80 | 1 | 47 |
| `batch` | 0.5–6 | 0.5 | 1 |

A param matching its default is omitted, so a stock link stays clean and a bare URL means the house profile. Out-of-range values clamp, off-step values snap to the slider grid, and unparseable values fall back to the default — the URL then rewrites itself to the sanitized values. **Copy share link** puts the current URL on the clipboard.

## Why only two salts

Chloride causes pitting corrosion in stainless boilers (LM caps it at 30 ppm; this recipe uses 0), so no table salt or calcium chloride. Chalk won't dissolve in still water without CO₂. Magnesium provides extraction hardness without calcium's carbonate limescale.

## Chemistry

- Hardness as CaCO₃ = Epsom mg/L × 100.09 / 246.47
- Alkalinity as CaCO₃ = NaHCO₃ mg/L × 50.04 / 84.01
- TDS meter estimate ≈ 0.7 × ion sum (conductivity meters under-read MgSO₄/NaHCO₃ against NaCl calibration)

## Pourover tab

Opens with `?tab=pourover`. No boiler to protect, so the spec is taste and the base is tap water.

- **Coffee** picks a target. Roast sets hardness (GH) and alkalinity (KH); process only nudges alkalinity, because nobody publishes process-specific hardness.
- **Water** picks the base (Cedar tap, Tolt tap, distilled) and lets the sliders leave the preset.
- **Recipe** is in mL of the espresso tab's Concentrates A and B. Salts only add, so a target below the tap cuts the tap with distilled first.
- **Where it sits** plots this water against Seattle tap and the published recipes.

| Roast | GH | KH | Evidence |
| --- | --- | --- | --- |
| Light | 70 | 25 | Practitioner recipes (Lotus, Rao) |
| Medium | 70 | 40 | SCA standard |
| Dark | 50 | 40 | Disputed — vendors disagree on direction |

| Process | KH nudge | Evidence |
| --- | --- | --- |
| Washed, honey, blend | +0 | Washed is the published baseline; the rest inferred |
| Natural | +5 | Inferred |
| Anaerobic / carbonic, thermal shock / co-ferment | +10 | Inferred |

| Param | Values | Default |
| --- | --- | --- |
| `roast` | `light` `medium` `dark` | `light` |
| `process` | `washed` `honey` `natural` `anaerobic` `coferment` `blend` | `washed` |
| `base` | `cedar` `tolt` `distilled` | `cedar` |
| `gh` | 20–140 | the preset |
| `kh` | 5–80 | the preset |
| `liters` | 0.5–8, step 0.5 | 1 |

`gh` and `kh` are written only when the sliders are off the preset. Each tab owns the query string while it is showing, so a link carries one profile.

Tap chemistry is the mean of 10 quarterly [Seattle Public Utilities analyses](https://www.seattle.gov/utilities/your-services/water/water-quality/analyses) at in-city distribution points, Feb 2024 – May 2026. Total hardness is calculated as 2.497 × Ca + 4.118 × Mg; SPU's own "Hardness, Grains" row disagrees with its calcium and magnesium in three of those reports.

Single static page, no dependencies. Open `index.html` or serve the repo root.
