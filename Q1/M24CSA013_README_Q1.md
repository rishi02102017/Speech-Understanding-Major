
# Q1 - Code-Switched Speech Transcription, Translation & Synthesis (Speech Understanding Major)

## Overview

This project is part of the **Speech Understanding Major** and addresses the challenges of processing code-switched speech data (i.e., audio with mixed languages such as English and Hindi). The primary goal of this task is to develop a full pipeline for:

1. **Transcribing** lecture audio containing code-switched speech.
2. **Removing filler words** from the transcription to enhance clarity.
3. **Translating** the cleaned transcription into a **low-resource language** (in our case, Bengali).
4. **Generating synthetic speech** in that low-resource language using a **Text-to-Speech (TTS)** model.
5. **Personal voice cloning** by synthesizing the translated content in the user’s **own voice** and **native language** (Assamese).
6. **Evaluating** the pipeline using objective metrics.

The notebook `Speech_Q1.ipynb` demonstrates all of these stages programmatically using modern tools in speech and NLP.

---

## Objectives

- Work with multilingual and code-switched audio data.
- Apply speech-to-text transcription with filler removal.
- Translate to a low-resource language.
- Synthesize speech using standard TTS and voice cloning.
- Evaluate transcription and audio generation accuracy.

---

## Tools and Libraries Used

- **OpenAI Whisper** for automatic speech recognition (ASR).
- **Regular Expressions (Regex)** for filler word removal.
- **Facebook NLLB-200** for multilingual translation (English to Bengali).
- **gTTS (Google Text-to-Speech)** for generating Bengali audio.
- **YourTTS** from Coqui for multilingual, multi-speaker TTS with voice cloning.
- **FFmpeg** for audio extraction and conversion.
- **JiWER** for calculating Word Error Rate (WER) and Character Error Rate (CER).

---

## Workflow Description

### 1. Transcription

- Extracted audio from the original video lecture using FFmpeg.
- Used **Whisper large model** to transcribe the lecture.
- The transcription captured both English and Hindi parts accurately, thanks to Whisper’s multilingual capabilities.

### 2. Filler Word Removal

- Applied a regex-based function to remove common filler words such as “um”, “uh”, “you know”, etc.
- The cleaned transcript is more concise and suitable for translation or synthesis.

### 3. Translation

- The cleaned transcription was translated from **English to Bengali** using **facebook/nllb-200-distilled-600M**, a state-of-the-art translation model for low-resource languages.
- The output was saved as `bengali_translated_final.txt`.

### 4. Bengali TTS Generation

- The translated Bengali text was passed through **gTTS** (Google Text-to-Speech) to generate natural-sounding Bengali audio.
- This generated file (`bengali_speech_gTTS.mp3`) captures the complete lecture in Bengali in synthetic voice.

### 5. Voice Cloning using Assamese

- As a bonus attempt, the user recorded their **own voice in Assamese**.
- The sample was used as a **voice reference** for **YourTTS**, which supports voice cloning with multilingual synthesis.
- The cleaned and translated text (now in Assamese) was synthesized in the user's **own voice**, resulting in `your_voice_assamese_output.wav`.

> Note: While YourTTS doesn't support Assamese natively, it was tested to evaluate how well it handles phonetic alignment from another Indian script. Character-level vocabulary mismatches were observed, pointing to further research needed in Assamese voice synthesis.

### 6. Evaluation

- **Transcription Accuracy** (from Whisper ASR):
  - **Word Error Rate (WER)**: Measures the percentage of incorrect words in the hypothesis compared to the reference.
    - **WER Score**: 0.0851
  - **Character Error Rate (CER)**: Measures the number of character-level edits (insertions, deletions, substitutions) required.
    - **CER Score**: 0.0639
  - These scores indicate that the transcription quality from Whisper is highly accurate and well-suited for further processing like translation or synthesis.

- **Audio Quality Evaluation** (Optional):
  - **PESQ (Perceptual Evaluation of Speech Quality)** was used to compare the synthesized Assamese speech (`your_voice_assamese_output_16k.wav`) with the user's original voice sample (`my_voice_sample_16k.wav`). PESQ is a widely-used metric for evaluating perceived speech quality.
  - **MOS (Mean Opinion Score)** was estimated based on PESQ results, approximating subjective human ratings.
  - **Scores Obtained**:
    - **PESQ Score**: *2.96*
    - **Estimated MOS**: *3.00*
  - This indicates moderate intelligibility and speaker similarity despite Assamese not being natively supported by the TTS model used.

---

## Project Directory Structure

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

---

## Key Insights & Learnings

- **Multilingual models** like Whisper and NLLB-200 are highly effective for code-switched data.
- **Filler word removal** enhances the quality of both translation and synthesized audio.
- Bengali, though low-resource, is reasonably supported across translation and TTS pipelines.
- Attempting **voice cloning in Assamese** provided insights into limitations of current multilingual TTS models when faced with unsupported scripts.
- **YourTTS** requires further adaptation for non-Latin scripts like Assamese to work seamlessly.

---

## Challenges Faced

- **Language vocabulary mismatches** while cloning Assamese voice using a model not trained on that script.
- Ensuring accurate segmentation of speech during transcription and translation.
- Finding TTS models that support both voice cloning and low-resource languages.
- Managing audio conversion parameters (sample rate, mono channel) for compatibility with models.

---

## Conclusion

This task provides a complete end-to-end solution for processing multilingual lecture audio — from transcription to synthesized translation. It integrates modern speech and NLP models to demonstrate how real-world speech understanding systems can be built, even when dealing with low-resource languages and personal voice synthesis.

The success of the Bengali pipeline and experimental trials in Assamese both reveal the potential and the challenges ahead in truly inclusive speech AI.

---

## Author
**Jyotishman Das**

## Course Instructor
**Dr. Richa Singh**