# Linea Mini Water Lab

Interactive calculator for DIY espresso water that stays inside [La Marzocco's water spec](https://lamarzoccousa.com/wp-content/uploads/2023/09/Water-Specifications.pdf), built for a Linea Mini fed from 1-gallon jugs of distilled water.

**Live:** https://robbybro.github.io/marzocco-water/

## What it does

- Sliders for **total hardness** (70–100 ppm as CaCO₃), **alkalinity** (40–80 ppm as CaCO₃), and **batch size**
- Recalculates **Epsom salt (MgSO₄·7H₂O)** and **baking soda (NaHCO₃)** doses in grams, plus mL doses of two stock concentrates for better accuracy on a 0.1 g scale
- Live **spec check** against La Marzocco's published limits (hardness, alkalinity, chloride, TDS, pH)
- **Flavor descriptors** — how each profile reads in the cup (brightness, sweetness, body, harshness risk)

## Why only two salts

Chloride causes pitting corrosion in stainless boilers (LM caps it at 30 ppm; this recipe uses 0), so no table salt or calcium chloride. Chalk won't dissolve in still water without CO₂. Magnesium provides extraction hardness without calcium's carbonate limescale.

## Chemistry

- Hardness as CaCO₃ = Epsom mg/L × 100.09 / 246.47
- Alkalinity as CaCO₃ = NaHCO₃ mg/L × 50.04 / 84.01
- TDS meter estimate ≈ 0.7 × ion sum (conductivity meters under-read MgSO₄/NaHCO₃ against NaCl calibration)

Single static page, no dependencies. Open `index.html` or serve the repo root.
