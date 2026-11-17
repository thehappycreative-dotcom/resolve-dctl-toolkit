# BHS Pro DCTL Pack — Guide

25 DCTLs for DaVinci Resolve, built on one shared film-style color engine. They sit alongside the lighter tools in `dctl/color`, `dctl/looks`, `dctl/effects` and `dctl/exposure`.

## Install

1. Copy the `dctl/pro` folder into Resolve's LUT folder (Mac: `/Library/Application Support/Blackmagic Design/DaVinci Resolve/LUT/`).
2. Restart Resolve (or right-click in the LUT browser and choose Refresh).
3. On the Color page open **OpenFX → ResolveFX Color → DCTL**, drop it on a node, and pick a `BHS_Pro_…` file from the DCTL list.

Use the DCTL effect rather than applying the file as a LUT: the sliders, animated grain, and the halation and bloom tools only work as an effect.

## The one setting to get right: Working Space

Every tool has **Working Space** at the top. It tells the tool what the node is being fed.

| Your timeline | Set Working Space to |
|---|---|
| Normal Rec.709 timeline, footage already converted (LUT, CST or BHS Camera Input) | **Rec.709 Gamma 2.4** (the default) |
| DaVinci Wide Gamut / Intermediate grade | **DaVinci WG Intermediate** |
| ACES (ACEScct) | **ACEScct** |

With every control at neutral, each tool passes the picture through unchanged.

## Node order

**Rec.709 timeline (simplest)**

1. `U5 Camera Input` → Output: Rec.709 Picture (skip if the footage is already Rec.709)
2. `D6 Exposure and Balance`
3. `D4 Skin Refine` (optional)
4. One look: `A1 Film Lab`, `B1 Looks`, `B2 Inspo Looks` or `B3 Clean Lifestyle`
5. Fine tuning: `C1 Density`, `D1 Vectors HSL`, `D3 Split Tone`
6. Texture: `E2 Halation` → `E3 Bloom and Mist` → `E1 Grain` → `E4 Vignette`

**Wide gamut timeline (most latitude)**

1. `U5 Camera Input` → Output: DaVinci WG Intermediate
2. `U4 Gamut Compress` (only if there are LED or neon colors)
3. Same tools as above, each set to **DaVinci WG Intermediate**
4. `U6 Display Output` as the last node

## The tools

### A — Film

| File | What it does |
|---|---|
| `A1 Film Lab` | Two-stage film emulation: 17 negative stocks (Vision3 50D / 250D / 200T / 500T, Eterna 500T, Portra 160 / 400 / 800, Gold 200, Ektar 100, Fuji Pro 400H, Superia 400, CineStill 800T, Kodachrome 64, Ektachrome E100, Velvia 50, Agfa Vista 200) printed onto 6 print stocks (Kodak 2383, Kodak 2393, Fuji 3513, Bleach Bypass, Aged Print, Black and White). Print Stock = None gives a clean negative scan look. |
| `A2 Mono Film` | Black and white: 5 stocks, 6 lens filters, tone curve, sepia or selenium toning. |

### B — Looks

| File | What it does |
|---|---|
| `B1 Looks` | 20 finished looks: Vintage Contemporary, Mocha Editorial, Quiet Luxury, Teal and Amber, Emerald Noir, Golden Hour, Pastel Dream, Nordic Clean, 90s Editorial, Y2K Flash, Bleach Bypass, Tungsten Night, Super 8 Sunfade, Classic Chrome, Terracotta Earth, Clean Commercial, Creamy Skin Glow, Cool Steel, Two Strip, Warm Mono. |
| `B2 Inspo Looks` | 9 looks inspired by documentary and street-photography frames (see below). |
| `B3 Clean Lifestyle` | Calm, clear, modern lifestyle and beauty work: 7 bases plus plain-language controls (Airy, Clean Whites, Skin Glow, Tame Greens, Soft Blues, Pastel). |

All three share the same trims: **Strength**, **Tone Amount** and **Color Amount** (take only the contrast or only the color of a look), Exposure, Contrast, Saturation, Density, Warmth, Tint, Fade, and **Skin Protect**.

**Inspo Looks**

| Look | Character |
|---|---|
| Danfo Teal, Danfo Teal Soft | Blues and skies pushed to deep teal, dense golden yellows, rich brown skin, cream whites |
| Market Dusk, Market Dusk Lifted | Low-key and dense, rust reds and oranges, olive-black shadows, tan highlights |
| Earth Walk, Rust and Olive | Muted earth tones, cool olive greens, ochre and rust kept rich, soft blacks |
| Backyard Gold, Aqua Sky Vintage | Yellow-green highlights, aqua sky, vivid reds, cream whites |
| Rich Skin | A neutral finishing look that keeps deep skin tones warm and full |

### C — Density and color separation

| File | What it does |
|---|---|
| `C1 Density` | Film density: colorful areas get deeper and richer instead of brighter. Overall amount plus per-color density. |
| `C2 Subtractive Saturation` | Saturation with a Film Depth control (0 = video saturation, 1 = film-style), Vibrance, shadow and highlight saturation, soft ceiling. |
| `C3 Color Separation` | Pulls the palette apart: cleans near-grays, strengthens real color, and gathers hues toward a warm anchor and its opposite. |
| `C4 Crosstalk` | Six dye-layer controls with presets (Dense Print, Warm Dye, Cool Dye, Soft Blend). Grays stay neutral. |

### D — Color tools

| File | What it does |
|---|---|
| `D1 Vectors HSL` | Hue, saturation and luminance for eight colors: red, orange (skin), yellow, green, cyan, blue, purple, magenta. |
| `D2 Tetra` | Six-vector tetrahedral control, with R, G and B targets per color. |
| `D3 Split Tone` | Shadow, midtone and highlight tints with balance and softness. Hues follow the normal color wheel. |
| `D4 Skin Refine` | Finds skin by hue, then evens and enriches it. **Shadow Richness** keeps deep skin tones from going gray. **Show Skin Mask** shows what is being treated. |
| `D5 Film Curve` | Contrast with a soft toe and shoulder. Film RGB enriches color; Luma Only leaves saturation alone. |
| `D6 Exposure and Balance` | Exposure in stops, temperature, tint and printer lights (12 points = 1 stop). |

### E — Texture

| File | What it does |
|---|---|
| `E1 Grain` | Film grain in log, scaled to the frame so 1080p and 4K match. Types: 35mm Fine, 35mm Fast, 16mm, Super 8. |
| `E2 Halation` | Red-orange glow around bright lights and edges. |
| `E3 Bloom and Mist` | Highlight bloom plus a soft mist-filter veil. |
| `E4 Vignette` | Lens-style vignette in stops, with edge warmth and saturation. |

Halation and Bloom are the heavy ones. They default to **Fast**; switch Quality to **High** for the final render. Expect them to slow playback on older GPUs, especially at 4K — turn them off while you grade and on to render.

### U — Utility and evaluation

| File | What it does |
|---|---|
| `U1 False Color` | Exposure map. See the legend below. |
| `U2 Scope Views` | Ten views: Luminance, Saturation Map, Hue Only, Skin Check, Clipping, Gamut Warning, Red / Green / Blue channel, Warm Cool Map. |
| `U3 Test Chart` | Generates an exposure ramp, hue sweep, color patches, skin tones or saturation ramps so you can see what a grade does. Put it on the first node. |
| `U4 Gamut Compress` | Brings LED and neon colors back inside Rec.709 smoothly. |
| `U5 Camera Input` | Log to Rec.709 or to DaVinci WG for 14 camera formats: Sony S-Log3 (S-Gamut3.Cine and S-Gamut3), ARRI LogC3 and LogC4, Canon Log 2 and Log 3, Panasonic V-Log, Fujifilm F-Log and F-Log2, Nikon N-Log, Blackmagic Film Gen 5, RED Log3G10, DJI D-Log, Apple Log. |
| `U6 Display Output` | Final DaVinci WG → Rec.709 conversion with a filmic rolloff. |

**False Color legend** (left to right on the strip at the bottom of the frame)

| Color | Stops from mid gray | IRE on a Rec.709 picture |
|---|---|---|
| Purple | below −6 | under 2 |
| Blue | −6 to −4 | 2–10 |
| Teal | −4 to −2.5 | 10–20 |
| Green | −0.5 to +0.5 (mid gray) | 38–46 |
| Pink | +1 to +1.7 (bright skin) | 52–62 |
| Yellow | +2.5 to +3.5 | 78–90 |
| Orange | +3.5 to +4.5 | 90–97 |
| Red | above +4.5 | over 97 |

Everything in between shows as gray.

## Starting points

**Fashion film:** Camera Input → Exposure and Balance → Skin Refine (Glow 0.2, Shadow Richness 0.3) → Film Lab (Vision3 250D + Kodak 2383) → Density 0.3 → Halation 0.4 → Grain (35mm Fast, 0.3).

**Documentary look:** Camera Input → Exposure and Balance → Inspo Looks (Danfo Teal or Market Dusk, Strength 0.8) → Skin Refine if skin needs it → Grain (35mm Fine).

**Calm lifestyle:** Camera Input → Exposure and Balance → Clean Lifestyle (Bright Airy or Clean Natural) → Bloom and Mist (Bloom 0.2, Mist 0.15). No grain, or 35mm Fine at 0.15.

## Notes

- **Camera Input vs Resolve's own conversion.** Use one or the other on a clip, not both. Camera Input does not cover DJI D-Log M, Sony S-Log2 or HLG; use a Color Space Transform for those.
- **Looks are a starting point.** On footage that is already contrasty, bring Tone Amount down first.
- **Animated grain** needs the DCTL applied as an effect on Resolve 19.1 or later.
- **What was tested.** The first version of this pack failed to load with "main DCTL function's return value must be float3". Resolve reads the `return` line of each tool's main function as text and requires it to say `make_float3(...)`; most files returned through a helper instead. All 25 are fixed. Each file is now checked against the rules in Resolve 20's own DCTL checker, compiled with the Metal compiler using Resolve's own macro definitions, and run on both GPUs in this Mac (Radeon Pro 560X and Intel UHD 630), where the output matches the reference to within 0.0005. They are also run across every menu entry and both ends of every slider in all three working spaces, checked to return an unchanged picture at neutral settings, and all 15 Camera Input entries are checked against their published mid-gray values. Loading them inside Resolve itself is the one step only you can do. If Resolve shows a "DCTL Build Error" for any file, send me the message and I will fix it.
- **If a node still shows the old error.** Resolve keeps the failed build until told to rebuild: press the reset button beside the DCTL list on that node, or pick the DCTL again.
- **About the film stocks.** They are built from each stock's published and widely documented character, tuned by eye on test images. They are not measured from film scans, so treat the names as a guide to the flavor rather than a lab-accurate match.
