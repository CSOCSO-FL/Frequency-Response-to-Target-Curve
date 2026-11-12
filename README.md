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
- Adjust the output frequency range. You can also change the dB decimal precision, although the default setting should work fine.
- Compare the normalized measurement with the generated curve.
- Download a `.targetcurve` file or frequency/dB TXT.

**Recommended REW export settings:** Set **1/6-octave or Psychoacoustic smoothing**, select **SPL** export units, **Space** delimiter, and **REW export format**. Check **Do not include any comments or headers in the export** and **Do not include phase in the export**.

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

## Next step: Combine your measured response with a house curve

Once you've created a target curve from your REW measurement, you can add a **bass boost or high-frequency roll-off** without losing the measured peaks and dips.

### Step 1: Create your preferred house curve

Open the [EQ Target Curve Generator](https://databender1729.github.io/eq-target-curves/).

1. Change **End Hz** from **24,000** to **20,000 Hz**.
2. Adjust **High Cutoff dB** and **End dB** to taste. For example, try **−1 dB** for High Cutoff and **−5 dB** for End.
3. **Important: Keep Start dB at 0 dB (recommended).** Your measurement-based target curve already contains the measured bass response. Any additional bass boost from the house curve is **added on top of it**, potentially raising the final bass target much more than intended. In this workflow, use the house curve primarily to shape the **high-frequency roll-off**. Only increase Start dB if you deliberately want *extra* bass boost beyond what is already present in your normalized measurement.
4. Click **Generate**, then copy the generated target curve.

### Step 2: Convert your house curve to biquads

Open [Target Curve to Biquads](https://csocso-fl.github.io/Frequency-Response-to-Target-Curve/target-curve-to-biquads.html), paste your house curve, and click **Generate biquads**. Use **96 kHz** for the sample rate, check the fitted-response graph and error, and copy the generated biquad coefficients.

### Step 3: Create your measurement-based target curve

In **REW**, export your frequency-response measurement as a TXT file using **1/6-octave or Psychoacoustic smoothing**, without phase or header information. Open [Frequency Response to Target Curve](https://csocso-fl.github.io/Frequency-Response-to-Target-Curve/), import the TXT file, and generate your normalized measurement curve. Copy the generated `.targetcurve` text.

### Step 4: Combine both curves

Open [Target Curve PEQ](https://databender1729.github.io/eq-target-curves/target_curve_peq.html).

1. Paste your **measurement-based target curve** into the **first box**.
2. Paste the **house curve biquad coefficients** into the **second box**.
3. Click **Generate new target curve**.
4. Review the graph, then download the combined target curve.

**Result:** Your original measured peaks and dips are retained, while the bass boost or high-frequency roll-off from your house curve is added to the response. The result follows the *fitted biquad approximation* of your house curve, so check the final graph before importing it into Dirac Live.

**Tip:** The two curves are additive. For example, if your measured curve is +2 dB at a frequency and your house-curve biquads add +3 dB there, the combined target will be approximately +5 dB.
