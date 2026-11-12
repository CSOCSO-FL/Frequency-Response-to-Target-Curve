# Audio Calibration Tools

Free browser-based tools for working with **REW frequency responses**, **Dirac Live target curves**, and **biquad EQ filters**.

Both tools run locally in your browser. No installation or account is needed to use them.

## Open the tools

### 1. Frequency Response to Target Curve

**[Open Frequency Response to Target Curve](https://csocso-fl.github.io/Frequency-Response-to-Target-Curve/)**

Turn a Room EQ Wizard (REW) frequency response into a Dirac-compatible target curve.

- Calculates the average SPL between **500 and 2,000 Hz** and offsets that average to **0 dB**.
- Preserves the measurement's peaks and dips, rather than inverting them.
- Choose **6, 18, or 36 breakpoints per octave**; default is **18**.
- Adjust output frequency range and dB decimal precision.
- Compare the normalized measurement with the generated curve.
- Download a `.targetcurve` file or frequency/dB TXT.

**Recommended REW export settings:** Set **1/6-octave smoothing**, select **SPL** export units, **Space** delimiter, and **REW export format**. Check **Do not include any comments or headers in the export** and **Do not include phase in the export**.

**Important:** This exports a normalized measurement curve, not an inverse EQ correction curve.

### 2. Target Curve to Biquads

**[Open Target Curve to Biquads](https://csocso-fl.github.io/Frequency-Response-to-Target-Curve/target-curve-to-biquads.html)**

Fit a target curve with PEQ and shelving filters, then export biquad coefficients.

- Paste Hz/dB pairs or upload `.targetcurve` and TXT files.
- Choose **4, 6, 8, 10, 12, or 16 biquad filters**.
- Select **96 kHz** (recommended) or **48 kHz** sample rate.
- Choose Fast, Balanced, or High accuracy optimization.
- Compare original and fitted curves, inspect individual filter responses, and review the filter summary.
- Check RMS and maximum fitting errors.
- Copy or download REW/miniDSP-style biquad TXT coefficients.

**Important:** Biquads approximate the original curve; they are not guaranteed to reproduce every sharp peak or dip perfectly. Check the plotted fit and use the same sample rate as the receiving PEQ tool.

## How to use these tools together

1. Export a frequency response from REW.
2. Open **Frequency Response to Target Curve**, generate the normalized target curve, and download it.
3. If you want a biquad representation of that curve, open **Target Curve to Biquads**, load the generated file, and fit it.
4. Check the resulting graphs and fitting errors before using any exported filters.

## Source files

- [Frequency Response to Target Curve (index.html)](index.html)
- [Target Curve to Biquads (target-curve-to-biquads.html)](target-curve-to-biquads.html)

These are standalone HTML tools; their processing runs in the browser.
