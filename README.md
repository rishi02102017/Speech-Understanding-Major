<h1 align="center"> Speech Understanding Major - IIT Jodhpur</h1>

This repository contains the complete submission for the **Speech Understanding Major** course, undertaken as part of the M.Tech program in **Artificial Intelligence** at **Indian Institute of Technology Jodhpur**.

Author: **Jyotishman Das**  
Roll Number: **M24CSA013**  
Instructor: **Dr. Richa Singh**

---

## Overview

This major course project is designed around real-world challenges in multilingual and multimodal **speech understanding systems**. The project comprises **three comprehensive questions**, each addressing a different core area in the speech pipeline: **transcription**, **denoising**, and **future research**. The solutions are implemented using Python, HuggingFace Transformers, Whisper, TTS models, and standard signal processing libraries.

---

## Directory Structure

```
/Speech Understanding Major/
├── Q1/
│   ├── extracted_audio.wav               # Audio extracted from lecture video
│   ├── transcription.txt                 # Raw transcription from Whisper
│   ├── cleaned_transcription.txt         # Transcription with filler words removed
│   ├── bengali_translated_final.txt      # Translated version in Bengali
│   ├── bengali_speech_gTTS.mp3           # Bengali speech generated using gTTS
│   ├── my_voice_sample.wav               # User's voice sample in Assamese
│   ├── your_voice_assamese_output.wav    # Synthesized Assamese speech in user's voice
│   └── Speech_Q1.ipynb                   # Main notebook with full code and workflow
│   └── my_voice_sample_16k               # 16kHz version of user's original voice sample for PESQ/MOS
│   └── your_voice_assamese_output_16k    # 16kHz version of synthesized audio for PESQ/MOS
│   └── Block_Diagram.png    
│   └── README_Q1.md   

├── Q2/
│   ├── Denoising samples/              # From link in the Q
│   │   └── set 2 - only noisy/
│   │       ├── bus.wav
│   │       ├── cafe.wav
│   │       ├── ped.wav
│   │       └── street.wav
│   │
│   ├── Process/
│   │   ├── Audio analysis/             # SNR, PESQ, and spectrum analysis
│   │   │   ├── audio_analysis.ipynb
│   │   │   └── audio_analysis.py
│   │   │
│   │   ├── Denoising/                  # Audio denoising implementation
│   │   │   ├── denoising_audio.ipynb
│   │   │   └── denoising_audio.py
│   │   │
│   │   └── Transcription/             # Speech-to-text script
│   │       ├── transcription.ipynb
│   │       └── transcription.py
│   │
│   ├── Results/
│   │   ├── bus/
│   │   │   ├── Transcript bus.txt
│   │   │   ├── Values bus denoised.png
│   │   │   ├── Values bus noisy.png
│   │   │   └── denoised_audio(BUS).wav
│   │   │
│   │   ├── cafe/
│   │   │   ├── Transcript cafe.txt
│   │   │   ├── Values cafe denoised.png
│   │   │   ├── Values cafe noisy.png
│   │   │   └── denoised_audio (CAFE).wav
│   │   │
│   │   ├── ped/
│   │   │   ├── Transcript ped.txt
│   │   │   ├── Values ped denoised.png
│   │   │   ├── Values ped noisy.png
│   │   │   └── denoised_audio(PED).wav
│   │   │
│   │   └── street/
│   │       ├── Transcript street.txt
│   │       ├── Values street denoised.png
│   │       ├── Values street noisy.png
│   │       └── denoised_audio(STREET).wav
│   │
│   └── Block_diagram                   
│   └── READ_ME.txt                     # Project overview


├── Q3/                        # Novel research challenge in speech
│   └── Block_diagram_Q3.png
│   └── Block_diagram   

├── M24CSA013_major.pdf        # Final technical report in CVPR format

```

---

## Question 1: Code-Switched Transcription and Synthesis

- **Goal**: Transcribe a lecture containing English-Hindi code-switched speech, clean the text, translate it to Bengali (a low-resource language), and synthesize speech from it.
- **Tools Used**:
  - Whisper (ASR)
  - Regex (filler removal)
  - NLLB-200 (Translation)
  - gTTS & YourTTS (TTS)
- **Highlights**:
  - Whisper handled code-switched content with ~8.5% WER.
  - YourTTS was used to clone user's voice in Assamese, even though it’s not natively supported.
  - PESQ: 2.96 | MOS: 3.00

---

## Question 2: Denoising and Transcription of Noisy Audio

- **Goal**: Analyze noisy speech from real environments (bus, cafe, street, pedestrian), design a denoising algorithm, and evaluate transcription accuracy post-denoising.
- **Pipeline**:
  - Noise statistics (RMS, SNR) via `librosa`
  - Classical denoising using **Spectral Subtraction**
  - Whisper for transcription
- **Evaluation**:
  - SNR Improvement: +5 dB to +11 dB
  - PESQ Scores ~1.03
  - WERs between 7.6% and 8.5%
- **Data Visuals**:
  - Spectrograms (Noisy vs Denoised)
  - Block diagram of the pipeline

---

## Question 3: Future Research Challenge in Speech Understanding

- **Title**: *Emotionally-Aware, Context-Retaining Voice Agents for Code-Switched, Multimodal Conversations in Low-Resource Languages*
- **Problem**:
  - Current systems lack long-term memory, emotional adaptation, and code-switch robustness.
- **Proposed Solution**:
  - Integrate WhisperX (ASR), multimodal emotion recognition, memory-augmented dialogue (LLM + RAM), and emotion-aware TTS.
- **Architecture**:
  - AVT (Audio-Visual Transformer), Retrieval-augmented memory, FastSpeech2 with prosody control
- **Datasets**:
  - CMU-MOSEI, SEWA, MUCS, MultiWOZ, EmoV-DB
- **Evaluation Metrics**:
  - WER, CER, Emotion F1, Coherence, BERTScore, MOS

---

## How to Run

Most notebooks can be executed in **Google Colab**. For local runs, ensure the following:

- `Python >= 3.8`
- Install dependencies:
  ```bash
  pip install -r requirements.txt
  ```

- For PESQ/MOS evaluation, install:
  ```bash
  pip install pesq jiwer librosa soundfile
  ```

---

## References

All references to models, datasets, and literature are included in `references.bib`.  
Use `biblatex` with `biber` backend in LaTeX for citation formatting.

---

## Citation

If referencing this repo for academic or demo purposes:

```
@misc{speech_major2024,
  author = {Jyotishman Das},
  title = {Speech Understanding Major - IIT Jodhpur},
  year = {2024},
  howpublished = {\url{https://github.com/rishi02102017/Speech-Understanding-Major}},
}
```

---

## Contact

For any queries, please reach out at:

**Jyotishman Das**  
Email: `m24csa013@iitj.ac.in`
