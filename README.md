# Text-to-Timbre Drum Transfer
**Controllable Drum Audio Synthesis via Beatboxing and Text Prompts**

This project builds a **two-stage generative audio pipeline** that asks:
1) **Beatbox** a rhythm (rhythmic control)  
2) **Type** a text prompt for the drum style (timbral control)  
…and get a synthesized **drum performance** that follows your rhythm while matching the requested style. :contentReference[oaicite:2]{index=2}

> Core idea: generate a **timbre reference** from text (AudioLDM), then use **TRIA** to transfer the beatbox rhythm onto that timbre. :contentReference[oaicite:3]{index=3}

---

## What this does
- **Input**:
  - Beatbox WAV (typically 5–10 seconds)
  - Text prompt describing drum style (e.g., “lo-fi hip-hop drums”, “heavy metal kit”) :contentReference[oaicite:4]{index=4}
- **Output**:
  - A generated drum WAV that preserves the rhythm and reflects the prompt’s style. :contentReference[oaicite:5]{index=5}

---

## How it works (Pipeline)
### Stage 1 — Text → Drum timbre reference (AudioLDM)
We generate a short **drum loop / timbre reference** conditioned on the user’s text prompt.  
This reference acts like the “drum kit sound palette” for the next stage. :contentReference[oaicite:6]{index=6}

### Stage 2 — Beatbox rhythm transfer (TRIA)
TRIA takes:
- **Rhythm input**: your beatbox
- **Timbre reference**: the generated “drums.wav”  
…and outputs a realistic drum track that matches the beatbox rhythm using the timbre from the reference. :contentReference[oaicite:7]{index=7}

---

## Repository structure
```

Text-to-Timbre-Drum-Transfer/
├─ dataset/
│  └─ beatbox_*.wav                 # Example beatbox recordings
│
├─ models/
│  ├─ audioLDM/                     # Text → drum timbre generation
│  └─ TRIA/                         # Rhythm transfer model code / setup
│
├─ Full_Pipeline/
│  └─ Text_and_Beatbox_into_Drum_Generation.ipynb   # End-to-end notebook
│
└─ README.md

````

---

## Steps
1. Open the notebook in **Google Colab** (GPU runtime needed).
2. Run cells in order.
3. When prompted:
   - Enter a **TEXT_PROMPT** (e.g., `tight jazz brushes`)
   - Upload a **beatbox WAV**
4. The notebook will:
   - Generate `drums.wav` from the text prompt (AudioLDM)
   - Run TRIA to produce final drum output(s)
   - Generate a few drums solo records according to beatbox rythm and text style

> Tip: For cleaner timbre references, keep prompts drum-specific (avoid “melody”, “vocals”, “bass”, etc.).

---

### 2) Install Python dependencies (typical)

Your notebook installs packages like:

* `diffusers`, `transformers`, `accelerate`, `scipy`
* `descript-audiotools`, `librosa`, `soundfile`, `pyloudnorm`, `primePy`
* `huggingface_hub`

> Exact versions may matter. If you hit issues, start by matching the notebook installs.

### 3) Download TRIA weights

The notebook downloads pretrained artifacts from Hugging Face into:

* `pretrained/tria/.../model.pt`
* `pretrained/tokenizer/...`

Make sure paths match what your TRIA loading code expects.

---

## Usage tips

* **Beatbox recording**

  * Keep it dry (minimal room noise, no background music)
  * Clear transients help rhythm extraction
* **Prompting**

  * Good: `clean 90s hip hop drums`, `tight jazz kit`, `metal double kick`
  * Avoid: prompts that encourage non-percussive instruments
* **Duration**

  * Timbre reference: short (4–8s is usually enough)
  * Output: start small (to debug) then increase

---

## Success criteria (Project goals)

We aim to:

* Produce drum outputs that are **rhythm-faithful** to beatboxing and **style-aligned** to the prompt.
* Demonstrate at least **3+ genres** (e.g., rock, hip-hop, metal). 

---

## Known challenges / concerns

* Prompt consistency and avoiding non-drum artifacts
* Tempo alignment between generated timbre reference and beatbox rhythm
* Diffusion latency for longer clips 

---

## References

* **TRIA: The Rhythm In Anything** (O’Reilly et al., 2025) 
* **Stable Audio Open** (Stability AI, 2024) 
* **AudioLDM** (Liu et al., 2023) 
* **AudioLDM 2** (Liu et al., 2023) 
* **Tango / Tango 2** (Chen et al., 2023–2024) 

---

## Authors

* Alon Canfi
* Amit Zachi
* Omri Triff
* Yuval Ratzabi
* Gilead Lashesko 

