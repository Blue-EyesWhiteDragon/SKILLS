---
name: Mastering
description: >
    Technical reference for the final stereo delivery chain. Covers process topologies, 
    toolkit-specific unit tags (FabFilter, SSL, UAD), genre-specific parameter targets, 
    and Harman-target alignment rules. Optimized for high-precision generative audio 
    mastering workflows.
version: 1.0.0
topic: mastering
keywords: [
    mastering, LUFS, Harman target, clipping, limiting, linear-phase, mid-side, true-peak, 32-bit, crest-factor
]
author: Blue-EyesWhiteDragon
co-author: Claude Code
last_updated: 2026-05-09
---

# SKILL

### Topic: Mastering (Final Stereo Delivery)

---

## Topology Reference

> Decision rules only. Tags used throughout: [UT] Unit Topology / Mechanism, [GA] Genre Application.

### Surgical EQ (Subtractive)
- **Mechanism:** Linear Phase EQ (FabFilter Pro-Q 3). [UT]
- **Decision Rule:** Use only for narrow-Q notch filtering of resonances. Linear phase avoids the phase-smearing of transients common in minimum-phase filters during steep subtraction. [GA]
- **Character Tag:** `transparent · surgical · phase-accurate` [UT]

### Tonal EQ (Additive)
- **Mechanism:** Minimum Phase / Analog Emulated EQ (SSL Native/Waves, UAD). [UT]
- **Decision Rule:** Use broad-Q shelves or bells for tonal shaping. The resulting phase-shift from analog-style filters provides psychoacoustic "depth" and "warmth." [GA]
- **Character Tag:** `musical · weighted · depth-forward` [UT]

### Dynamic Correction (Multiband)
- **Mechanism:** Multiband Compression (FabFilter Pro-MB). [UT]
- **Decision Rule:** Engage only when the crest factor in a specific frequency band exceeds genre thresholds. Prevents the master from "breaking up" under localized energy build-up. [GA]
- **Character Tag:** `controlled · spectral-stability` [UT]

### Mid-Side (M/S) Processing
- **Mechanism:** Independent processing of Mid (Sum) and Side (Difference) channels. [UT]
- **Decision Rule:** Use M/S EQ to manage width. A High-pass filter on the Side channel (Mono-Bass) ensures all sub-frequency energy is phase-aligned in the center. [GA]
- **Character Tag:** `wide · focused · phase-aligned` [UT]

### Harmonic Saturation (Tape/Transformer)
- **Mechanism:** Transformer or Tape Emulation (UAD Ampex ATR-102, SSL X-Saturator). [UT]
- **Decision Rule:** Apply for "Analog Glue." Tape emulation adds non-linear density and low-mid cohesion, mimicking the response of high-end magnetic mastering decks. [GA]
- **Character Tag:** `warm · dense · glued · analog-weight` [UT]

### Soft Clipping (Transient Shaving)
- **Mechanism:** Hard/Soft Clipping (UAD or digital-domain clipping). [UT]
- **Decision Rule:** **Clipper-First Logic.** Shave the top 1.5–3dB of peak transients before the limiter. This creates "loudness headroom" and prevents the final limiter from pumping. [GA]
- **Character Tag:** `aggressive · loud · transient-transparent` [UT]

---

## Unit Lookup Table

| Unit                           | Brand      | Type      | Character                                         |
|--------------------------------|------------|-----------|---------------------------------------------------|
| Pro-Q 3                        | FabFilter  | EQ        | surgical · linear-phase · clean                   |
| Pro-L 2                        | FabFilter  | Limiter   | versatile · modern · transparent                  |
| Pro-MB                         | FabFilter  | Multiband | precise · correction-focused                      |
| SSL G-Master Bus Comp          | SSL/Waves  | Comp      | classic-glue · rhythmic · punchy                  |
| SSL Native X-EQ 2              | SSL        | EQ        | clean-analog · versatile                          |
| SSL Native X-Saturator         | SSL        | Saturator | grit · weight · harmonic-density                  |
| Ampex ATR-102                  | UAD        | Tape      | ultimate-glue · weight · 30ips-clarity            |
| Manley Massive Passive         | UAD        | EQ        | tube-weight · broad-tonal-shaping                 |
| Precision Maximizer            | UAD        | Dynamics  | loudness-enhancer · harmonic-shaping              |

---

## Genre × Parameter Matrix

| Genre    | Target Integrated LUFS | True Peak Ceiling | Clipper Drive | Mono-Bass | Harman Delta | Note                                    |
|----------|------------------------|-------------------|---------------|-----------|--------------|-----------------------------------------|
| Pop      | -8.0                   | -1.0 dBTP         | 2.0 dB        | 90 Hz     | 0.0 dB       | Neutral Harman alignment. [GA]          |
| Hyperpop | -6.0                   | -1.0 dBTP         | 4.5 dB        | 120 Hz    | +1.5 dB      | Extreme clipping; bright slope. [GA]    |
| House    | -6.0                   | -1.0 dBTP         | 3.0 dB        | 120 Hz    | +1.0 dB      | Club-ready mono-alignment. [GA]         |
| Rock     | -9.0                   | -1.0 dBTP         | 2.0 dB        | 60 Hz     | -0.5 dB      | Mid-forward; Ampex 15ips weight. [GA]   |
| Jazz     | -12.0                  | -1.0 dBTP         | 0.0 dB        | 0 Hz      | -1.0 dB      | Dynamic preservation; no clipping. [GA] |

---

## Pitfalls — Avoidance Rules

### Phase Smearing via Subtractive EQ
- **Trigger:** Using Minimum Phase EQ for steep narrow-Q cuts. [UT]
- **Fix:** Mandate **Linear Phase** for all surgical subtraction (Pro-Q 3). [GA]

### Limiter Over-Working (Pumping)
- **Trigger:** Relying on the Limiter for >4dB of gain reduction. [UT]
- **Fix:** Implement **Clipper-First** logic; shave peaks *before* the limiter. [GA]

### Quantization Distortion
- **Trigger:** Rendering to 24-bit without dither. [UT]
- **Fix:** Use **32-bit Float** internally. If final output is 24-bit, use **TPDF dither**. [GA]

---

## Glossary

| Term              | Definition                                                                                 |
|-------------------|--------------------------------------------------------------------------------------------|
| 32-bit Float      | Resolution providing virtually infinite headroom and eliminating internal clipping. [UT]   |
| dBTP (True Peak)  | Signal peaks measured after D/A reconstruction; prevents inter-sample clipping. [UT]       |
| Delta from Harman | Spectral deviation from the Harman Reference Curve (Sean Olive research). [UT]             |
| Harman Target     | A listener-preferred frequency response featuring a sub-shelf and smooth HF roll-off. [UT] |

---

## References

### Unit Topology [UT]
1. FabFilter. *Equalization: Linear Phase EQ Explained*. [https://www.fabfilter.com/learn/equalization/linear-phase-eq]
2. Universal Audio. *Ampex ATR-102 Mastering Tape Recorder Manual*. [https://help.uaudio.com/hc/en-us/articles/32491139365140-Ampex-ATR-102-Mastering-Tape-Recorder-Manual]
3. Katz, B. (2014). *Mastering Audio: The Art and the Science*. Focal Press. (Standard for K-System and Clipping).
4. Solid State Logic. *SSL Plug-ins - Native & Waves Collections*. [https://solidstatelogic.com/products/ssl-plug-ins]
5. AES. *AESTD1008: Recommendations for Loudness of Internet Audio Streaming*. [https://aes.org/community/technical-document-aestd1008/]

### Genre Application [GA]
1. Olive, S. (2022). *The Harman Reference Curve: Why Immersive Audio is the Future*. Headliner Magazine. [https://headlinerhub.com/harman-dr-sean-olive-harman-reference-curve-immersive-audio-is-the-future.html]
2. Sound On Sound. *The End of the Loudness War?* [https://www.soundonsound.com/techniques/end-loudness-war]
3. iZotope. *Mastering for Streaming Platforms: Targets and Standards*. [https://www.izotope.com/en/learn/mastering-for-streaming-platforms]
4. Mix with the Masters. *Mastering Masterclasses*. [https://mixwiththemasters.com/]