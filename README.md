# Frequency Response to Target Curve

Convert a REW measurement into a Dirac target curve, with optional curve shaping built in.

**[Open the tool](https://csocso-fl.github.io/Frequency-Response-to-Target-Curve/)**

## How to use

1. Export your measurement from REW as TXT using **1/6-octave or Psychoacoustic smoothing**. Choose **SPL**, **Space** delimiter and **REW export format**. Exclude comments, headers and phase.
2. Upload the TXT file or paste its contents. The measurement must include **500–2,000 Hz**; the tool sets that band's average to **0 dB**.
3. Choose the output frequency range and breakpoints per octave. The defaults are **15–20,000 Hz** and **18 breakpoints per octave**.
4. Use **Optional Curve Shaping** if desired. I use it mainly for more treble roll-off. Try **High transition: −0.5 dB** and **Treble / end: −3 dB**. Also try **Curved** treble transition. Leave the bass adjustments at 0 dB for now.
5. Click **Generate target curve**, review the graph, and download the `.targetcurve` file.
6. Import it into Dirac Live and check it against your measured response before exporting the filters.

The graph stays visible while you edit. Click **Generate** to apply changes or **Reset shaping to neutral** to remove them.

Uploaded filenames are preserved in downloads. Everything runs locally in your browser. No biquad conversion or separate curve-combining tool is needed for this workflow.
