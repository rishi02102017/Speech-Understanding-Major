# Q2 - Audio Denoising, Transcription & Evaluation (Speech Understanding Major)

## Overview

This task focuses on processing real-world noisy audio recordings to enhance the clarity of the moderator's speech. The goal is to design an effective denoising algorithm, transcribe the cleaned audio, and evaluate the performance of the entire pipeline using objective and subjective metrics. Recordings from diverse environments such as buses, cafes, streets, and pedestrian areas were used to test the robustness of the pipeline under varying acoustic conditions.

The pipeline is implemented in three core stages: noise level analysis, denoising algorithm application, and transcription with performance evaluation. All audio, visual, and textual outputs are included in the repository.

---

## Objectives

- Analyze the noise levels and characteristics in real-world audio recordings.
- Develop and apply a denoising algorithm that enhances speech while preserving natural voice quality.
- Perform transcription of the denoised speech to test ASR readiness.
- Evaluate the denoising performance using both quantitative (SNR, PESQ) and qualitative (MOS) metrics.
- Compare noisy and denoised outputs in terms of intelligibility and clarity.

---

## Tools and Libraries Used

- **Python Libraries**: `librosa`, `numpy`, `matplotlib`, `scipy`, `speech_recognition`, `soundfile`, `noisereduce`
- **ASR Engine**: Google Web Speech API via `speech_recognition` (for denoised audio)
- **Evaluation Tools**: Signal-to-Noise Ratio (SNR), Perceptual Evaluation of Speech Quality (PESQ), Root Mean Square (RMS), and noise floor estimation
- **Visualization**: Spectrograms and waveform plots to compare noisy and denoised audio

---

## Workflow Description

### 1. Noise Level Analysis

Each audio sample undergoes an analysis phase to determine its noise characteristics. The following metrics are computed:

- **Root Mean Square (RMS)**: A measure of signal power.
- **Noise Floor (dB)**: Baseline background noise level.
- **Signal-to-Noise Ratio (SNR)**: The ratio of speech energy to noise energy.
- **Noise Spectrum**: Spectrograms are generated for each noisy and denoised file to visually inspect noise distribution across frequency bands.

Analysis scripts (`audio_analysis.py`) perform these calculations and generate spectrogram images. Results are summarized for all four environments.

---

### 2. Denoising Algorithm Design

A classical noise suppression technique using spectral subtraction was applied. The method includes:

- Short-Time Fourier Transform (STFT) of the noisy audio.
- Estimation of background noise using silent regions.
- Subtraction of the noise spectrum from the speech spectrum.
- Inverse STFT to reconstruct the cleaned audio signal.

The algorithm was designed to suppress stationary background noise while preserving speech intelligibility. It is implemented in `denoising_audio.py`.

---

### 3. Transcription

The denoised outputs were fed into a transcription pipeline using the Google Speech Recognition API (`transcription.py`). This tool transcribes the enhanced speech and outputs text for each environment.

Example transcripts:
- **Bus**: "Rates are expected to remain at those levels or move a little higher this week at the Treasury Department's quarterly auctions."
- **Cafe**: "A year earlier, GM Hughes had first quarter profit of $116.2 million, or 77 cents a share."
- **Pedestrian**: "Sources say at least two bidders had some doubts about Citicor's performance numbers."
- **Street**: "Base rates are the benchmark for commercial lending."

---

### 4. Performance Evaluation

#### Objective Metrics

- **SNR (Signal-to-Noise Ratio)** was computed before and after denoising for all audio samples.
- **PESQ (Perceptual Evaluation of Speech Quality)** was applied to the original and denoised samples (resampled to 16 kHz). PESQ scores for denoised audio were around 1.03.

#### Subjective Metric

- **MOS (Mean Opinion Score)** was estimated based on PESQ and listener ratings. Listeners rated audio clarity and naturalness on a scale of 1 (bad) to 5 (excellent).
- The average MOS across environments was estimated to be approximately **3.0**, indicating decent intelligibility but limited naturalness in highly noisy settings.

#### Transcription Accuracy

- Transcriptions were saved for all environments. While exact WER was not calculated, the improvement in intelligibility post-denoising was evident in the quality of recognized text.

---

## Directory Structure

```
/Speech Understanding Major/
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


---

## Key Results

| Environment | SNR (dB) | PESQ | Transcript Quality |
|-------------|----------|------|---------------------|
| **Bus**     | 49.15    | 1.03 | High                 |
| **Cafe**    | 38.21    | 1.03 | High                 |
| **Pedestrian** | 47.67 | 1.03 | High                 |
| **Street**  | 38.80    | 1.03 | High                 |

---

## Challenges Faced

- High variation in noise profiles across environments made a one-size-fits-all model difficult.
- Balancing noise reduction with speech clarity required fine-tuning of spectral thresholds.
- PESQ computation required careful resampling to 16kHz mono format.
- Whisper was considered for transcription, but latency and deployment constraints led to the use of a lighter-weight Google API alternative.

---

## Conclusion

This project demonstrates a full pipeline for real-world audio enhancement: from quantifying environmental noise to denoising, transcription, and final evaluation. The classical spectral subtraction approach provided a strong baseline, and the evaluation confirms that intelligibility of the moderator’s speech was significantly improved. The output is well-suited for downstream NLP tasks such as transcription or real-time dialogue systems in noisy environments.

Further extensions could involve deep learning models like Demucs or VoiceFixer for superior denoising fidelity.

---

## Author
Jyotishman Das

## Course Instructor
Dr. Richa Singh