# Resolve DCTL Toolkit

Free, open-source DCTLs for DaVinci Resolve by **Behappystudiox** (BHS), made for video editors and colorists. MIT licensed: use them in client work, modify them, share them.

## Tools

| Tool | Folder | What it does |
|---|---|---|
| **BHS Exposure Pro** | `dctl/exposure` | Exposure (stops), contrast + pivot, whites, highlights, midtones, shadows, blacks, highlight roll-off, saturation. Built-in False Color, Clipping Warning and Zone Mask views. |
| **BHS Film Print Look** | `dctl/looks` | Film-style tone curve, dye crosstalk, tinted shadows/highlights, highlight desaturation. |
| **BHS Split Tone** | `dctl/color` | Tint shadows and highlights with two hues while keeping brightness. |
| **BHS Skin Vibrance** | `dctl/color` | Boosts dull colors, leaves skin tones alone. |
| **BHS Vignette** | `dctl/effects` | Darken or lighten edges, with highlight protection. |

## Install

1. In Resolve: **DaVinci Resolve > Open LUT Folder** (Mac) or the equivalent option in the Color page LUT menu.
2. Copy the `.dctl` files into that folder (a subfolder is fine).
3. **Color page > right-click a node > LUT > Refresh List**, then apply the DCTL from the LUT list.

> DCTL support requires DaVinci Resolve Studio.

## Exposure Pro quick start

1. Put it on its own node before your look.
2. Set **Input Space** to match the footage (Linear, Gamma24, or DaVinciInt).
3. Set **View Mode** to *FalseColor* and adjust Exposure until skin and mid-grey sit where you want them; use *ClipWarning* to protect highlights and blacks.
4. Set View Mode back to **Off**.

## Contributing

Issues and pull requests are welcome. Bug reports with the Resolve version and the footage's color space help most.

## License

[MIT](LICENSE)
