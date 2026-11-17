# Changelog

## 1.2.0
- Exposure Pro rebuilt as `BHS_Pro_D7_Exposure_Pro` on the shared BHS Pro color core: Working Space (Rec.709 / DaVinci WG / ACEScct), tooltips on every control, neutral passthrough at default settings. Replaces the standalone `dctl/exposure/BHS_Exposure_Pro.dctl`.

## 1.1.1
- Fix: BHS Exposure Pro now loads in DaVinci Resolve. The main transform function had several return statements, and Resolve requires a single `return make_float3(...)`. Also removed `#define`s and brackets in slider labels to match the style of the BHS Pro tools.

## 1.1.0
- Added the BHS Pro pack: 25 film, look, color, texture and utility DCTLs in `dctl/pro`, plus a guide.

## 1.0.0
- Initial release: Exposure Pro, Film Print Look, Split Tone, Skin Vibrance, Vignette.
