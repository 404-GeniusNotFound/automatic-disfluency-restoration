# Automatic Disfluency Restoration 🎙️📝

![Status](https://img.shields.io/badge/Status-Completed-success) ![Metric](https://img.shields.io/badge/Metric-Word_Error_Rate-blue) ![Language](https://img.shields.io/badge/Python-3.x-yellow)

## 🏆 Achievements
* **Competition:** NPPE-2: Automatic Disfluency Restoration.
* **Status:** Late Submission.
* **Participant:** Sathvik V (Roll No: 22f2001468)

## 📖 Overview
This project was developed for the NPPE-2: Automatic Disfluency Restoration competition. The challenge sits at the intersection of Automatic Speech Recognition (ASR) and Natural Language Generation (NLG). The objective was to build a system capable of predicting the original, disfluent transcript from a clean text and its corresponding audio. 

My solution utilizes multi-modal fusion to effectively combine audio and text signals to make nuanced predictions. It features a robust data cleaning pipeline and a fine-tuned Hugging Face sequence-to-sequence model designed to work within strict compute constraints.

## 📊 Dataset
The dataset consists of audio clips in Hindi, their corresponding transcripts, and a list of common disfluencies.
* **Train Set:** Contains labeled examples for training the model. The `train.csv` file provides the disfluent ground truth transcript, which contains all original hesitations and filled pauses.
* **Test Set:** The `test.csv` file serves as the input for predictions. It contains the clean transcript, with all disfluencies removed.
* **Audio Data:** The `downloaded_audios/` directory contains 1003 audio files in `.wav` format. The total size of the audio data is 860.25 MB.
* **Disfluencies:** The `unique_disfluencies.csv` is a helper file that contains a list of all unique disfluent words/phrases, such as "अं" and "हम्म".

## 🛠️ Methodology

### 1. Data Processing & Preparation
* **Data Cleaning Pipeline:** A key part of the competition was data preparation, requiring participants to programmatically create a "clean" version of the training data. I mapped clean inputs to disfluent outputs by removing the words listed in `unique_disfluencies.csv` from the training transcripts.
* **Audio Processing:** Loaded and resampled the `.wav` audio files to 16kHz using `librosa` to prepare the input features for the model.

### 2. Model Selection & Fine-Tuning
* **Base Model:** Fine-tuned `collabora/whisper-base-hindi` to process both the audio and the clean text. 
* **Compute Constraints:** The challenge required participants to work within strict compute constraints, specifically utilizing Kaggle Notebooks only. To optimize memory, I employed gradient accumulation, FP16 half-precision, and gradient checkpointing.
* **Customization:** Added a 10% dropout rate (`0.1`) to the Whisper configuration to prevent overfitting on the training data.

### 3. Evaluation & Optimization
* **Metric:** Submissions were evaluated using the Word Error Rate (WER), the standard metric for assessing ASR systems. This metric measures the number of substitutions, deletions, and insertions between the predicted transcript and the ground truth.
* **Hybrid Prediction Strategy:** Built a custom prediction loop that only generated new transcripts for the null values in the test set, seamlessly merging them with existing clean text.

## 📈 Performance
* **Metric Optimized:** Word Error Rate (WER).
* **Goal:** Minimized the difference between the predicted and actual verbatim transcript. A score of 0.0 means a perfect prediction.

## 🚀 How to Run
1. Clone the repository.
2. Ensure you have the required libraries: `transformers`, `datasets`, `librosa`, `jiwer`, `evaluate`.
3. Place `train.csv`, `test.csv`, `unique_disfluencies.csv`, and the `downloaded_audios/` directory in your data folder.
4. Run the notebook (`automatic_disfluency_restoration.ipynb`).

---
*Created by Sathvik V*
