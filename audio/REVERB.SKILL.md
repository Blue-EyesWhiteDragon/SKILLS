---
name: Reverb
description: >
    Technical reference for reverberation in music production and generative audio. Covers topology, unit character tags, genre-specific parameter tables, technique decision rules, and pitfall avoidance. Optimised for LLM-driven generation workflows. All parameters expressed in signal-domain terms.
version: 1.0.0
topic: reverberation
keywords: [
    reverberation, audio, reverb, echo, damping, decay, plate, spring, hall, room, church, cathedral
]
author: Blue-EyesWhiteDragon
co-author: Claude Code
last_updated: 2026-05-08
---
# SKILL

### Topic: Reverberation

---

## Topology Reference

> Decision rules only. Tags used throughout: `[UT]` topology, `[GA]` genre application, `[DR]` digital rack, `[PD]` pedal, `[AR]` analogue.

### Plate

- **Mechanism:** Thin metal sheet vibrated by transducer; pickup(s) capture reverberation. Decay controlled by absorptive damping board. [UT]
- **Frequency Behaviour:** High frequencies decay faster than low — produces naturally bright, smooth, dense tail. HF decay shorter than LF decay by approximately 3× at studio settings. [UT]
- **Character Tag:** `bright · smooth · dense · no-room-signature` [UT]
- **Choose when:** Source needs presence and sheen without acoustic-space character. Vocals, snare, strings. [GA]

---

### Spring

- **Mechanism:** Audio drives a tensioned spring; pickup at opposite end captures vibration. Oil-dampened (professional units) or open tank (instrument units). [UT]
- **Frequency Behaviour:** Non-smooth; physical resonances produce characteristic "drip/twang" artifact on transient events. Decay less configurable than plate. [UT]
- **Character Tag:** `warm · characterful · drip · twang · coloured` [UT]
- **Choose when:** Period-correct tone identity is required — surf, blues, country, city pop, vintage rock. Spring is a tonal component, not a spatial effect. [GA]
- **Avoid when:** Acoustic naturalism or neutrality is the goal. Spring is inherently coloured. [GA]

---

### Digital Algorithmic

- **Mechanism:** DSP using all-pass filters, comb filters, and recirculating delay networks. No inherent frequency response bias — all parameters are programmable. [UT]
- **Frequency Behaviour:** Defined entirely by algorithm. Bit depth of converters determines noise floor and grain character — 12-bit (pre-1985) produces audible grain now used aesthetically; 24-bit+ is transparent. [UT]
- **Character Tags by algorithm family:**
    - `Lexicon-480L` → modulated · swimmy · studio-grade · Random-Hall
    - `Lexicon-224` → grainy · 12-bit · 1980s-digital · pop-canonical
    - `AMS-RMX16` → tight · non-linear · gated · drum-canonical
    - `Bricasti-M7` → natural · dense · early-reflection-rich · acoustic
    - `Eventide-Blackhole` → non-physical · vast · non-natural · instrument-grade
    - `Strymon-Cloud` → ambient-pad · blooming · sustain-forward
    - `OBNE-DarkStar` → lo-fi · pitch-shifted · bit-crushed · pad [UT, DR, PD]
- **Choose when:** Precise parameter control, algorithm switching, or a specific tonal signature is required. [GA]

---

### Digital Convolution (IR)

- **Mechanism:** Audio mathematically convolved with an impulse response (IR) of a real acoustic space via FFT. Produces the most acoustically accurate simulation of a specific real space. [UT]
- **Frequency Behaviour:** Exact to the captured space. Static — does not respond dynamically to input level changes. [UT]
- **Character Tag:** `accurate · static · non-modulated · venue-specific` [UT]
- **Choose when:** A specific real acoustic space must be recreated with maximum accuracy. Film scoring, orchestral, post-production. [GA]
- **Avoid when:** Dynamic or modulated reverb character is needed; convolution is computationally fixed. [GA]

---

### Hybrid

- **Mechanism:** Physical spring or plate provides primary reverb; digital processing (delay, modulation, bit-crush, pitch-shift) is applied to the analogue output. [UT]
- **Character Tag:** `physical-spring + digital-texture` [UT]
- **Example:** Dreadbox Hypnosis (three-spring tank + digital chorus/delay). [UT]

---

## Unit Lookup Table

> Compact reference for character-tag assignment. Use the `Character` column to construct generation prompts. `Type`: AR=Analogue, DR=Digital Rack, PD=Pedal.

| Unit                           | Type      | Character                                         | Primary Genre Tags                |
|--------------------------------|-----------|---------------------------------------------------|-----------------------------------|
| EMT 140                        | AR-Plate  | bright · smooth · dense · studio-canonical        | Pop · Rock · Orchestral · Film    |
| EMT 240                        | AR-Plate  | bright · airy · lighter-than-140                  | Acoustic · Strings · Mastering    |
| CVPA PlateMic                  | AR-Plate  | bright · smooth · dense                           | Studio · Acoustic                 |
| AKG BX-20                      | AR-Spring | warm · dark · controlled-drip                     | Pop · Soul · Vocal                |
| AKG BX-10                      | AR-Spring | warm · lighter-than-BX20                          | Vocal · Guitar                    |
| Grampian 636                   | AR-Spring | forward · nasal · British-60s                     | British-Invasion · Guitar         |
| Orban 111B                     | AR-Spring | smooth · broadcast-grade                          | Broadcast · Voiceover             |
| Hammond Type 4                 | AR-Spring | loose · splash · surf-defining                    | Surf · Vintage-Rock               |
| Steinway Spring                | AR-Spring | warm · instrument-integrated                      | Boutique · Instrument             |
| Dreadbox Hypnosis              | Hybrid    | spring-warm + digital-texture                     | Synth · Electronic · 80s          |
| Lexicon 480L                   | DR        | modulated · swimmy · studio-gold · Random-Hall    | Vocal · Film · Orchestral         |
| Lexicon 224                    | DR        | grainy · 12-bit · 1980s-canonical · ECM-aesthetic | Pop · Jazz · Synth                |
| Lexicon 960L                   | DR        | clean · multi-channel · precise                   | Film · Post-Production            |
| Lexicon PCM70                  | DR        | smooth · dense · budget-480L                      | Studio · Vocal · 80s              |
| Lexicon PCM91                  | DR        | smooth · 32-bit · professional                    | Studio · Live                     |
| Lexicon PCM92                  | DR        | smooth + filter-shaping                           | Studio · Professional             |
| Lexicon MPX500/200/MX400       | DR        | smooth · reduced-depth · semi-pro                 | Home-Studio                       |
| AMS Neve RMX16                 | DR        | tight · non-linear · drum-canonical · gated       | Drums · Pop · 80s                 |
| Eventide SP2016                | DR        | early-digital · dense-room                        | Drums · Studio                    |
| Eventide Reverb 2016           | DR        | early-digital · dense-room · modern-I/O           | Drums · Studio                    |
| Eventide H8000FW/H9000         | DR        | vast · algorithm-rich · Blackhole-source          | Film · Sound-Design               |
| Eventide Eclipse/Orville/H3000 | DR        | algorithm-rich · professional                     | Studio · Live                     |
| TC M3000/M4000/M6000           | DR        | neutral · precise · dual-engine                   | Drums · Broadcast                 |
| TC System 6000                 | DR        | neutral · surround · broadcast                    | Film · Broadcast                  |
| Yamaha SPX90                   | DR        | grainy · 1985-digital · Symphonic-patch           | 80s · Bass · Lo-Fi                |
| Yamaha SPX1000/REV500/REV7     | DR        | improved-SPX90 · functional                       | Studio · Broadcast                |
| Roland SRV-2000/R-880/SDE-1000 | DR        | warm · round · Japanese-digital                   | Electronic · 80s                  |
| Bricasti M7                    | DR        | natural · acoustic · early-reflection-rich        | Studio · Vocal · Orchestral       |
| Bricasti M10                   | DR        | M7-remote                                         | Studio                            |
| Bricasti M7CL                  | DR        | M7-live-variant                                   | Live-Sound                        |
| Sony DRE-S777                  | DR        | convolution · venue-accurate · static             | Film · Orchestral                 |
| Quantec QRS                    | DR        | scientific · neutral · precise                    | Classical · Broadcast             |
| Ursa Major SST-282             | DR        | grainy · early-digital · Eno-associated           | Ambient · Lo-Fi                   |
| Klark Teknik DN-780            | DR        | warm · British · professional                     | Studio · Live                     |
| AMS CX20                       | DR        | early-AMS · British                               | Studio                            |
| Publison DHM89                 | DR        | French-digital · granular-pioneer                 | Experimental                      |
| EMT 251                        | DR        | early-digital · West-Coast                        | Studio · Film                     |
| Ensoniq DP/4                   | DR        | functional · parallel-effects                     | Studio-Utility                    |
| Alesis MidiVerb II             | DR        | grainy · lo-fi · budget                           | Lo-Fi · Bedroom                   |
| Alesis QuadraVerb              | DR        | multi-effect · budget                             | Home-Studio                       |
| Alesis MidiVerb 4/NanoVerb     | DR        | grainy · lo-fi · minimal                          | Lo-Fi                             |
| Zoom RFX-1000/2200             | DR        | functional · budget                               | Project-Studio                    |
| Behringer DSP8000              | DR        | budget · functional                               | Entry-Level                       |
| Strymon BigSky MX              | PD        | 12-algorithm · versatile · studio-grade           | All-Genres                        |
| Strymon Flint                  | PD        | vintage-Fender · spring+tremolo                   | Blues · Country · Rock            |
| Strymon Cloudburst             | PD        | ensemble-pad · ambient · blooming                 | Ambient · Post-Rock · House       |
| Strymon BlueSky MkII           | PD        | shimmer · plate · spring · hall                   | Ambient · Shoegaze                |
| Eventide Space                 | PD        | 12-algorithm · Blackhole · professional           | All-Genres · Sound-Design         |
| Eventide H9                    | PD        | all-Eventide-algorithms · MIDI                    | All-Genres                        |
| Eventide Black Hole            | PD        | non-physical · vast · non-natural                 | Ambient · Drone · Film            |
| Boss RV-6                      | PD        | reliable · multi-algorithm · mid-level            | General                           |
| Boss RV-200                    | PD        | 12-type · tweakable · mid-level                   | General                           |
| Boss RV-500                    | PD        | 21-type · three-block · professional              | Studio · Live                     |
| TC HOF 2                       | PD        | MASH · TonePrint · versatile                      | General · Gigging                 |
| TC Nova Reverb NR-1            | PD        | desktop · TC-quality                              | Synth · Keyboard                  |
| Source Audio True Spring       | PD        | spring-emulation-reference · tank-sizable         | Surf · Blues · Country            |
| Source Audio Collider          | PD        | delay+reverb · dual · routing-flexible            | Ambient · Studio                  |
| Source Audio Ventris           | PD        | dual-engine · algorithm-library                   | Professional · Synth              |
| Walrus Audio Fathom            | PD        | hall+plate+lo-fi+sonar · Sustain                  | Ambient · Experimental            |
| Walrus Audio Slö               | PD        | dark+rise+dream · pad-latching                    | Ambient · Worship · Post-Rock     |
| Walrus Audio Fundamental       | PD        | hall+spring+plate · entry                         | General                           |
| EQD Afterneath V3              | PD        | delay-swarm · cascading · alien                   | Shoegaze · Ambient · Experimental |
| EQD Transmisser                | PD        | cosmic · self-oscillating · cave                  | Noise · Doom · Experimental       |
| EQD Levitation                 | PD        | modulated-hall · lush · live-usable               | Ambient · Guitar                  |
| Catalinbread Talisman          | PD        | EMT-140-plate-emulation · single-purpose          | Guitar · Synth                    |
| Catalinbread Soft Focus        | PD        | chorused-plate · octave-up · Slowdive             | Shoegaze · Dream-Pop              |
| DigiTech Polara                | PD        | Lexicon-MPX1 · Halo · versatile                   | General                           |
| MXR M300                       | PD        | warm · six-type · compact                         | Blues · Rock · Country            |
| EHX Cathedral                  | PD        | nine-type · Infinite · stereo                     | General · Ambient                 |
| EHX Holy Grail Plus            | PD        | spring+hall+room · simple · affordable            | Entry                             |
| EHX Oceans 11                  | PD        | eleven-type · Tides · Shimmer                     | General                           |
| EHX Oceans 12                  | PD        | dual-engine · stereo · twelve-type                | General · Stereo                  |
| Death By Audio Reverb Machine  | PD        | boutique · bright/dark · cave                     | Experimental · Noise              |
| Keeley Realverb Pro            | PD        | professional · transparent-dry                    | General · Studio                  |
| Neunaber Immerse MkII          | PD        | shimmer-focused · multi-mode                      | Ambient · Shimmer                 |
| Chase Bliss CXM 1978           | PD        | Lexicon-224-inspired · motorised · line-level     | Synth · Studio                    |
| Meris Mercury7                 | PD        | Blade-Runner · Lexicon-adjacent · hidden-params   | Ambient · Film                    |
| Spaceman Effects Orion         | PD        | true-analogue-spring · reference                  | Surf · Vintage                    |
| Danelectro Spring King         | PD        | true-analogue-spring · compact                    | Surf · Blues                      |
| Hotone NC-200 Verbera          | PD        | convolution+algorithmic · IR-loading              | Studio · Guitar                   |
| UAFX Golden Reverberator       | PD        | Lexicon-224-character · crusty · accurate         | Vocal · Studio · Guitar           |
| UAFX Starlight Echo Station    | PD        | tape-echo+reverb · RE-201 · Echoplex              | Vintage · Rock · Surf             |
| UAFX Astra                     | PD        | modulation-primary · reverb-secondary             | Modulation                        |
| Empress Reverb                 | PD        | 32-algorithm · studio-grade · line-level-tolerant | All-Genres · Synth                |
| Hologram Chroma Console        | PD        | granular+reverb · unpredictable · textural        | Electronic · Experimental         |
| OBNE Procession                | PD        | dark-pad · Flange/Filter/Tremolo · Hold           | Shoegaze · Doom · Film            |
| OBNE Dark Star                 | PD        | pad · Pitch/Delay/Crush · lo-fi                   | Ambient · Drone · Shoegaze        |
| OBNE Dark Star V3 Stereo       | PD        | pad · simultaneous-processing · stereo · MIDI     | Ambient · Film · Electronic       |
| OBNE Sunlight                  | PD        | dynamic-hold · note-by-note-sustain               | Ambient · Worship · Post-Rock     |
| OBNE Sunlight Stereo           | PD        | dynamic-hold · LFO · stereo                       | Ambient · Electronic              |
| OBNE Screen Violence           | PD        | modulated-reverb+drive · CHVRCHES-character       | Shoegaze · Indie · Synth-Pop      |
| OBNE Minim                     | PD        | reverb+delay+reverse · compact                    | Ambient · Experimental            |
| OBNE Rever                     | PD        | modulated-reverb+reverse+delay · order-switch     | Ambient · Bass-VI                 |
| OBNE BL-37                     | PD        | variable-clock · lo-fi · single-voice             | Lo-Fi · Ambient                   |
| OBNE Parting                   | PD        | granular-glitch+reverb · randomised               | Experimental · Harp · Noise       |
| OBNE Bathing                   | PD        | delay+reverb-hybrid · liminal · textural          | Experimental · Drone              |
| OBNE Dark Light                | PD        | DarkStar+Sunlight · dual                          | Ambient                           |

---

## Parameter Reference

### Decay (RT60)

- **Definition:** Time in seconds for reverb tail to attenuate by 60dB. [UT]
- **Decision rule:** Decay should not exceed one beat period in rhythmically active arrangements. At 120 BPM (beat period = 500ms), decay above 500ms blurs rhythmic definition. [GA]
- **Exception:** Ambient, drone, and pad applications intentionally violate this rule — infinite or very long decay is the design goal. [GA]

---

### Pre-delay

- **Definition:** Gap in milliseconds between direct signal onset and reverb onset. [UT]
- **Decision rule:** Increase pre-delay to improve source clarity without reducing reverb level. 20ms–50ms is effective for vocals and melodic leads in dense arrangements. 0ms–10ms for drums, percussive synthesis, and ambient wash where immediate onset is the goal. [GA]

---

### Diffusion

- **Definition:** Rate at which echo density builds up. High = immediate smooth wash; low = audible individual early reflections before dense tail. [UT]
- **Decision rule:** Low diffusion (20–45%) for drums and percussive material to preserve spatial placement. High diffusion (70–100%) for pads, vocals, and orchestral material for enveloping character. [GA]

---

### Damping

- **Definition:** Rate at which high frequencies decay relative to low frequencies within the tail. [UT]
- **Decision rule:** Increase damping (HF rolloff at 3kHz–5kHz) when the reverb tail competes with high-frequency arrangement content (cymbals, bright synths, distorted guitar). Low damping appropriate for classical, jazz, and contexts where natural hall brightness is required. [GA]

---

### Mix (Wet/Dry)

- **Definition:** Amplitude ratio of processed reverb signal to unprocessed direct signal. [UT]
- **Decision rule:** Set mix in full-arrangement context, never in isolation. Reverb at -20dB return send is often too loud when heard in context of a full mix. [GA]
- **Reverb-as-instrument:** 80–100% wet when reverb is a generative sound design element, not a spatial effect. [GA]

---

### Modulation

- **Definition:** Slow periodic variation applied to delay times within the reverb network. Prevents comb-filter resonance ("ringing") and adds organic quality. [UT]
- **Decision rule:** Enable low modulation (Spin/Wander at minimum) on any algorithmic reverb with decay above 2.5s to prevent metallic resonance. Increase modulation depth for pad and shimmer applications. Keep modulation off or subliminal for classical, jazz, and naturalistic contexts. [GA]

---

### Early Reflections

- **Definition:** Initial discrete echoes within the first 5–80ms following the direct sound. Encode acoustic geometry — size, shape, surface material of the simulated space. [UT]
- **Decision rule:** For natural-space simulation, early reflections must be consistent with the late tail. Mismatched early reflections (e.g., small-room pattern with large-hall tail) produce an unconvincing acoustic. Bricasti M7 architecture separates early reflection engine from tail engine to avoid this. [DR, GA]

---

### Freeze / Hold

- **Definition:** Routes delay network output to its own input at unity gain, sustaining the tail indefinitely. [UT]
- **Decision rule:** Freeze generates a static pad from whatever reverb tail was active at trigger time. Character of the frozen pad is determined by the algorithm — plate freeze = bright dense pad; Blackhole freeze = vast non-physical pad; OBNE DarkStar freeze = lo-fi pitch-shifted pad. [GA]

---

## Genre × Application Matrix

> Each entry: `Algorithm · Decay · Pre-delay · Diffusion · Damping · Mix · Mod · Note`. Tags: [GA] genre application, [DR] digital rack, [PD] pedal, [AR] analogue.

---

### Vocal

| Genre                 | Algorithm                     | Decay    | Pre-delay | Diffusion | Damping            | Mix Return     | Mod        | Note                                                         |
|-----------------------|-------------------------------|----------|-----------|-----------|--------------------|----------------|------------|--------------------------------------------------------------|
| Pop                   | Plate                         | 1.5–2.5s | 25–50ms   | 60–80%    | 5kHz rolloff       | −20 to −14dBFS | Low        | HF damping prevents tail competing with vocal presence range |
| Hyperpop              | Plate short + Room very short | 0.5–1.5s | 0–8ms     | 100%      | None (bright)      | −6 to −3dBFS   | Fast+deep  | Reverb is harmonic layer, not space; high mix is intentional |
| Folk                  | Room or Plate warm            | 0.8–1.8s | 10–25ms   | 30–55%    | Heavy 3kHz rolloff | −22 to −18dBFS | Off        | Intimate; reverb sounds like the room, not processing        |
| Traditional/Classical | Large Hall                    | 2.0–4.0s | 20–60ms   | 75–95%    | Minimal            | −16 to −10dBFS | Subliminal | Must not truncate before ensemble's own natural decay        |
| Choral                | Hall or Chamber               | 2.5–4.5s | 30–60ms   | 80–100%   | Low                | −14 to −10dBFS | Off        | Modulation conflicts with choral intonation purity           |
| K-pop                 | Plate                         | 1.2–2.0s | 20–40ms   | 70–85%    | Moderate 5kHz      | −18 to −14dBFS | Low        | High HF retention matches arrangement brightness             |
| J-pop                 | Plate or Room warm            | 1.5–2.5s | 20–35ms   | 60–75%    | 4kHz rolloff       | −18 to −15dBFS | Low        | Slightly darker than K-pop; more mid-forward                 |
| City Pop              | Plate warm or Spring          | 1.5–2.5s | 15–30ms   | 50–70%    | Moderate           | −18 to −14dBFS | Low/slow   | AMS RMX16 Plate A1 or EMT 140 are historically accurate      |
| Metal                 | Plate (vocal)                 | 1.5–2.5s | 25–40ms   | 65–80%    | Moderate           | −16 to −12dBFS | Low        | Plate for presence in high-SPL arrangement                   |
| Rock                  | Plate or Hall                 | 1.5–2.5s | 25–40ms   | 50–70%    | 5kHz rolloff       | −16 to −12dBFS | Low        |                                                              |
| Blues                 | Spring or Room                | 1.0–2.0s | 5–20ms    | 30–55%    | Heavy              | −16 to −12dBFS | Off        | Spring is tonal identity, not spatial effect                 |
| Jazz                  | Hall or Chamber               | 1.2–3.0s | 20–50ms   | 70–90%    | Minimal            | −18 to −12dBFS | Off        | Reverb should sound like the venue, not processing           |
| House                 | Plate                         | 1.2–2.0s | 15–30ms   | 75–90%    | Moderate           | −16 to −12dBFS | Low        | Separate reverb from kick-sidechain pumping on same bus      |

---

### Drums

| Genre                 | Snare Algorithm                                                                         | Snare Decay           | Kit Room Decay | Pre-delay                   | Diffusion Room | Sidechain / Routing                                      | Note                                                                                          |
|-----------------------|-----------------------------------------------------------------------------------------|-----------------------|----------------|-----------------------------|----------------|----------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Pop                   | Plate A1 (AMS) · Room A1 (AMS) · Ambience (overheads)                                   | 1.0–1.8s              | 0.4–1.0s       | 10–20ms snare               | 40–60%         | HPF at 100–150Hz on reverb send — mandatory              | Three-send approach: Ambience on overheads, Room on bus, Plate on snare                       |
| Hyperpop              | Plate 100% wet · Room short                                                             | 0.5–1.2s              | 0.1–0.3s       | 0–5ms                       | 100%           | None                                                     | Reverb adds density, not space; high mix intentional                                          |
| Folk                  | Room natural                                                                            | 0.8–1.5s              | 0.6–1.2s       | 10–20ms                     | 35–55%         | None                                                     | Preserves dynamic feel; minimal compression on reverb return                                  |
| Classical/Traditional | Hall · Plate accent                                                                     | 2.0–3.5s              | 1.0–2.0s       | 20–50ms                     | 80–95%         | None                                                     | Reverb must not truncate before natural percussion decay                                      |
| Metal                 | Nonlin/Gated snare (AMS Nonlin2) · Room close (very short) · Hall room crush (100% wet) | Cut at 150–300ms      | 0.2–0.6s       | 10–20ms snare · 0–5ms close | 15–30%         | HPF at 100Hz                                             | Three-layer: (1) tight room, (2) gated snare, (3) crushed hall via FET compressor at 100% wet |
| Rock                  | Plate snare · Room                                                                      | 1.0–1.8s              | 0.5–1.2s       | 10–20ms                     | 50–70%         | HPF at 100Hz                                             | FET compression on room return for weight                                                     |
| Blues                 | Spring or Room                                                                          | 0.8–1.5s              | 0.5–1.0s       | 5–15ms                      | 30–55%         | None                                                     | Natural decay priority                                                                        |
| Jazz                  | Room minimal or none                                                                    | 0.5–1.2s              | 0.4–0.8s       | 5–15ms                      | 50–70%         | None                                                     | Overhead natural room dominant; reverb supplements only                                       |
| K-pop                 | Plate snare · Room bus                                                                  | 1.0–1.6s              | 0.3–0.8s       | 8–18ms                      | 65–80%         | HPF at 80Hz                                              | High RMS drum bus; transient preserved in attack window                                       |
| J-pop                 | Plate snare · Room                                                                      | 1.0–1.8s              | 0.4–1.0s       | 10–20ms                     | 60–75%         | HPF at 80Hz                                              | Slightly more dynamic range than K-pop                                                        |
| House                 | Room tight · Hall 100% wet (pad layer)                                                  | 0.2–0.8s room · ∞ pad | —              | 0–5ms room                  | 50–65%         | Kick sidechain on room/overhead sends; HPF at 60Hz on SC | Room tight for presence; infinite pad as independent harmonic layer                           |
| City Pop              | Room or Spring tight                                                                    | 0.5–1.2s              | 0.4–0.8s       | 5–15ms                      | 50–65%         | HPF at 100Hz                                             | Controlled; period-correct SPX90 or AMS RMX16 Room character                                  |

---

### Instrument / Synth

| Context                   | Algorithm                                 | Decay    | Pre-delay | Diffusion | Damping                     | Mix            | Note                                                                |
|---------------------------|-------------------------------------------|----------|-----------|-----------|-----------------------------|----------------|---------------------------------------------------------------------|
| Guitar — Spring           | Spring (AKG BX20 or True Spring)          | 0.8–2.0s | 5–20ms    | 30–55%    | Heavy                       | −16 to −12dBFS | Spring is tonal identity; drip artifact is intentional              |
| Guitar — Ambient/Shoegaze | Hall large · Cloud · Blackhole · DarkStar | 4.0s–∞   | 0–15ms    | 80–100%   | Minimal                     | 80–100% wet    | Reverb IS the sound; freeze/hold used performatively                |
| Guitar — Pop/Rock         | Plate or Room                             | 0.5–1.5s | 10–20ms   | 50–70%    | Moderate                    | −22 to −16dBFS | Short room for placement; plate for cohesion                        |
| Bass Guitar               | Plate or Room very subtle                 | 0.3–0.8s | 0–10ms    | 40–60%    | Heavy LF cut on reverb send | −24 to −20dBFS | HPF at 200–300Hz on reverb send — prevents low-end mud accumulation |
| Synthesiser — Pads        | Hall or Cloud or Ensemble                 | 3.0s–∞   | 0–20ms    | 80–100%   | Minimal                     | 40–100% wet    | Line-level input required — use CXM 1978, Empress, or rack unit     |
| Synthesiser — Percussive  | Plate or Room short                       | 0.3–1.0s | 5–15ms    | 50–70%    | Moderate                    | −20 to −14dBFS | Short decay preserves attack transient definition                   |
| Acoustic Piano            | Room medium or Hall                       | 1.5–2.5s | 15–35ms   | 60–80%    | 4kHz rolloff                | −18 to −14dBFS | Must model natural acoustic of a room around the instrument         |
| Electric Piano            | Room or Spring subtle                     | 0.5–1.2s | 5–20ms    | 45–65%    | Moderate                    | −20 to −16dBFS | Spring adds vintage character in city pop and jazz contexts         |
| Strings (orchestral)      | Hall or Chamber                           | 2.0–4.0s | 20–50ms   | 75–95%    | Low                         | −16 to −10dBFS | Long pre-delay models distance in large hall                        |
| Broadcast / VO            | Room short or subtle Plate                | 0.4–0.9s | 5–15ms    | 50–70%    | Heavy                       | −24 to −20dBFS | Minimal; clarity of speech is primary constraint                    |

---

## Technique Decision Rules

### Pre-delay for Clarity Without Mix Reduction

- **When:** Vocal or lead instrument is losing intelligibility in a dense mix despite moderate reverb level. [GA]
- **Action:** Increase pre-delay to 25–50ms before reducing mix. Pre-delay preserves source onset while maintaining spatial depth. [UT, GA]

---

### Non-linear / Gated Reverb

- **When:** Rhythmic clarity is required alongside aggressive reverb density — drums in 1980s pop, rock, metal. [GA]
- **Action:** AMS RMX16 Nonlin2 or equivalent gated algorithm. Set gate cutoff at 150–300ms. Reverb is audible at full density immediately post-transient; no sustaining tail into subsequent hits. [DR, GA]
- **Character:** `aggressive · present · rhythmically-clean · 80s-canonical`

---

### Reverb-as-Instrument (Freeze / Pad)

- **When:** A harmonically rich pad is required without a synthesiser part; ambient composition; generative texture. [GA]
- **Action:** Set reverb to 80–100% wet. Engage freeze/hold on the reverb tail. Continue playing over the frozen pad. Algorithm choice determines character — see Unit Lookup Table character column. [PD, GA]
- **Key units:** OBNE Dark Star, Eventide Blackhole, Strymon Cloudburst Ensemble, OBNE Sunlight (dynamic hold — no footswitch needed). [PD]

---

### Three-Send Drum Reverb Architecture (Pop/Rock)

- **When:** Dense arrangement where drums need spatial presence without reverb tail accumulation in kick frequency range. [GA]
- **Architecture:** Send 1 (Ambience, −18dBFS) on overhead bus → AMS RMX16 Ambience. Send 2 (Room, −15dBFS) on drum bus → AMS RMX16 Room A1 with HPF at 100–150Hz. Send 3 (Plate, −12dBFS) on snare channel → AMS RMX16 Plate A1. [DR, GA]
- **Rationale:** Each send targets different frequency content and dynamic event type. HPF on drum bus send prevents kick low-end from accumulating in room reverb. [GA]

---

### Parallel Reverb

- **When:** Source needs increased density and size without the source signal losing level. [UT]
- **Action:** Route reverb on aux send/return, not as insert. Dry signal preserved at unity gain; reverb return added separately. Enables higher reverb levels without reducing source presence. [UT, GA]

---

### Reverse Reverb

- **When:** A swell or "inhale" leading into a phrase is needed; ambient transitions; psychedelic production. [GA]
- **Mechanism:** Reverb tail is reversed in time — amplitude builds toward the source onset rather than decaying away from it. Implemented via DAW (record tail, reverse in region) or dedicated algorithm (AMS RMX16 Reverse, Eventide Space Reverse, OBNE Rever/Minim). [DR, PD, GA]

---

## Pitfalls — Avoidance Rules

### Transient Smear (Diffusion Too High on Percussive Material)

- **Trigger:** Diffusion above 60% on kick drum, snare, plucked strings, staccato vocal. [UT]
- **Effect:** Smooth reverb onset blends with transient peak; source loses spatial placement and attack definition; mix sounds "blurred." [UT]
- **Fix:** Reduce diffusion to 20–45% on percussive material. [GA]

---

### Low-Mid Mud Accumulation

- **Trigger:** Reverb applied to bass-range instruments (bass guitar, cello, lower-register piano, kick) without HPF on reverb send. [UT]
- **Effect:** Low-frequency energy recirculates through reverb network and accumulates in 100–300Hz range, producing "washy" mix with reduced kick clarity. [UT]
- **Fix:** HPF on reverb send at 150–300Hz for bass instruments; HPF at 80–150Hz on drum bus reverb send. [GA]

---

### Pre-delay Too Short — Source/Reverb Blend Conflict

- **Trigger:** Pre-delay below 5ms on complex harmonic sources (dense chords, full mixes, choral sections). [UT]
- **Effect:** Reverb onset phase-interferes with direct signal at shared frequencies; source sounds "washed out" at moderate mix levels. [UT]
- **Fix:** Apply 20–40ms pre-delay on complex harmonic material. [GA]

---

### Metallic Resonance at Long Decay

- **Trigger:** Decay above 8–10s on algorithmic reverb without modulation. [DR]
- **Effect:** Fixed delay networks resonate at specific frequencies; a tonal "ringing" or metallic artifact appears in the tail. [UT]
- **Fix:** Enable modulation (Spin/Wander or equivalent). Apply HF damping. [DR, GA]

---

### Reverb Tail Truncating Ensemble Decay

- **Trigger:** Compressor release time shorter than RT60 of the recording space applied to room mics or stereo bus. [UT]
- **Effect:** Gain reduction engages before previous reverb tail has decayed; ensemble ambiance "breathes" or "ducks" after each event. Destroys naturalism of classical, choral, jazz recordings. [UT]
- **Fix:** Release time ≥ RT60 of the space. Program-dependent release preferred for room mic compression. [GA]

---

### Spring Vibration Artifact

- **Trigger:** Physical spring reverb unit (hardware or pedal) mounted on vibration-transmitting surface, or in proximity to high-SPL monitoring. [AR]
- **Effect:** Spring resonates from external physical force; audible "boing" artifact in output. [AR]
- **Fix:** Use digital spring emulation (Source Audio True Spring) in high-SPL or vibration-prone environments. Isolate hardware units on floating mounting. [PD, GA]

---

### Line-Level Synthesiser into Instrument-Level Pedal

- **Trigger:** Synthesiser output (−10dBV to +4dBu) fed directly into pedal reverb designed for instrument level (~−20dBu). [GA]
- **Effect:** Input clipping in pedal's front-end; distortion on reverb tail; loss of dynamic range in the reverb processing. [GA]
- **Fix:** Use line-level-tolerant reverb (Chase Bliss CXM 1978 line-level mode, Empress Reverb, rack digital unit). [PD, DR, GA]

---

### Convolution Reverb on Dynamic Material

- **Trigger:** Convolution (IR) reverb applied to source with very wide dynamic range where the acoustic response should vary with level. [UT]
- **Effect:** Convolution is a linear process — the same IR is applied regardless of input level. At high SPL, the tail is unrealistically consistent. [UT]
- **Fix:** Use algorithmic reverb when dynamic non-linearity of the simulated space is perceptually important. Reserve convolution for fixed-level acoustic accuracy requirements. [UT, GA]

---

## Glossary

| Term                       | Definition                                                                                                                                                                                                              |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Algorithm                  | Mathematical model of acoustic space using all-pass filters, comb filters, and recirculating delay networks.                                                                                                            |
| All-pass Filter            | Phase-only filter (no amplitude change). Used in reverb diffusion to spread phase relationships across spectrum, smoothing discrete reflections into a dense tail.                                                      |
| Comb Filter                | Destructive/constructive interference between a signal and a time-delayed copy. Produces frequency-response notches and peaks. Used in reverb late-reverberation engines; audible as metallic resonance if unmodulated. |
| Convolution                | Mathematical multiplication of audio with an impulse response (IR) of a real acoustic space via FFT. Produces accurate but static, non-dynamic reverb.                                                                  |
| Decay / RT60               | Time in seconds for reverb tail to attenuate by 60dB. Primary measure of space size and surface absorption.                                                                                                             |
| Diffusion                  | Rate of echo density build-up after onset. High = immediate smooth wash; low = sparse audible early reflections before dense tail.                                                                                      |
| Dynamic Hold               | Freeze mechanism triggered by cessation of input signal rather than a footswitch. Reverb tail sustains when playing stops; resumes when playing restarts. Pioneered by OBNE Sunlight.                                   |
| Early Reflections          | First discrete echoes arriving 5–80ms after direct sound. Encode acoustic geometry (size, shape, surface material of space).                                                                                            |
| Ensemble (Strymon)         | Reverb mode in the Cloudburst generating harmonically rich pad texture following playing dynamics. Not a spatial simulation — a generative pad voice.                                                                   |
| Freeze / Hold              | Sustains reverb tail indefinitely by routing delay network output to its own input at unity gain.                                                                                                                       |
| Gated Reverb               | Reverb tail truncated abruptly at a set point; tail is present at full density immediately post-transient but does not sustain into subsequent hits.                                                                    |
| HPF (on reverb send)       | High-pass filter applied to the reverb send signal before it enters the reverb unit. Prevents low-frequency energy from accumulating in the reverb tail.                                                                |
| Impulse Response (IR)      | Digital audio file recording a real acoustic space's response to a test impulse. Used in convolution reverb.                                                                                                            |
| Late Reverberation         | Dense, diffuse tail following early reflections. Produced by thousands of overlapping reflections; statistically random; decays at RT60 rate.                                                                           |
| Modulation                 | Slow periodic variation of delay times within reverb network. Prevents comb-filter metallic resonance; adds organic character to tail.                                                                                  |
| Nonlin / Gated (AMS RMX16) | Non-linear reverb program producing a rising envelope that is cut off abruptly rather than decaying naturally. Defines 1980s drum production aesthetic.                                                                 |
| Pre-delay                  | Gap in milliseconds between direct signal onset and reverb onset. Preserves source clarity without reducing reverb level.                                                                                               |
| Random Hall (Lexicon 480L) | Lexicon 480L's signature algorithm. Spin and Wander parameters modulate delay lines pseudo-randomly, producing a "swimmy" tail without metallic resonance.                                                              |
| RT60                       | See Decay.                                                                                                                                                                                                              |
| Shimmer                    | Reverb effect in which a pitch-shifted copy of the tail (typically ±1 octave) is fed back into the reverb input, creating a continuously harmonically enriched pad.                                                     |
| Spin / Wander              | Lexicon parameters governing modulation of delay network. Spin = modulation rate; Wander = randomisation of modulation depth. Prevents metallic resonance.                                                              |
| Spring Drip                | Characteristic transient resonance artifact of a spring reverb on sharp attack transients. Audible as "boing" or "splash." Desirable in surf, blues, vintage contexts; managed elsewhere.                               |
| Tail                       | The sustained, decaying portion of the reverb signal following early reflections. Primary determinant of perceived space size.                                                                                          |
| Wet/Dry Mix                | Amplitude ratio of processed reverb to unprocessed dry signal. 0% = dry only; 100% = reverb only (used for reverb-as-instrument applications).                                                                          |