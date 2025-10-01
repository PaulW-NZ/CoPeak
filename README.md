cat # CoPeak
Spectral Peak Co-occurrence Analyser

# Peak Co-occurrence Audio Analyzer

This is a single-file, browser-based audio analysis tool designed to visualize the harmonic structure of various audio files through spectrograms and peak co-occurrence heatmaps.

![Peak Co-occurrence Heatmap Example](cooccurrence.png)
*Example of a peak co-occurrence heatmap generated from a human voice.*

## Description

This tool provides a user-friendly interface for performing spectral analysis on audio recordings. It is entirely self-contained in a single HTML file with no external dependencies, making it easy to use and share.

The primary features are the generation of a standard spectrogram and a more advanced **peak co-occurrence heatmap**. This heatmap is particularly useful for visualizing the relationships between frequency components in a signal, making it excellent for analyzing the harmonic structure of pitched sounds like musical instruments or the human voice.

## Features

- **Zero-Dependency**: The entire tool is in `peak_cooccurrence_analyzer.html`. No setup required.
- **Broad Audio Format Support**: Load and analyze common audio formats (WAV, MP3, FLAC, Ogg, AAC, etc.) using the browser's built-in decoders. Also supports importing **headerless raw PCM data**.
- **Spectrogram Display**: View a traditional time-frequency spectrogram of the audio.
- **Peak Co-occurrence Heatmap**: Visualize which frequency peaks tend to occur at the same time, revealing the underlying harmonic and timbral structure of the sound.
- **Interactive Analysis**:
    - Select a time range on the spectrogram to zoom in and re-process a specific section.
    - Hover over the heatmap to see corresponding frequency lines on the spectrogram.
- **Adjustable Parameters**: Fine-tune the analysis with controls for:
    - FFT Size
    - Window Size & Hop Size
    - Pre-FFT Gain (Pre-emphasis)
    - Number of peaks for co-occurrence
    - "Peaky" threshold to filter for harmonically rich frames.
- **Light & Dark Themes**: Switch between themes for comfortable viewing.

## Usage

1.  Download the `peak_cooccurrence_analyzer.html` file.
2.  Open it in any modern web browser (e.g., Chrome, Firefox, Edge).
3.  Click "Choose File" to load an audio file.
4.  Adjust the analysis parameters in the sidebar as needed.
5.  Click "Process File" to perform the analysis and generate the visualizations.

## How It Works

The analysis is performed entirely in the browser using JavaScript. The core process is as follows:

1.  **Audio Decoding**: The `.wav` file is read and decoded into raw audio samples.
2.  **STFT**: The tool performs a Short-Time Fourier Transform (STFT) by breaking the audio into small, overlapping chunks. Each chunk is multiplied by a Hamming window to reduce spectral leakage.
3.  **Spectrogram**: The power spectrum of each chunk is calculated and plotted as a column in the spectrogram image.
4.  **Peak Co-occurrence**:
    - For each chunk, the algorithm calculates a "peaky" factor (crest factor) to determine if the spectrum is noisy or contains distinct, sharp peaks.
    - In "peaky" frames, the N strongest frequency peaks are identified.
    - A square matrix (the co-occurrence matrix) is updated by incrementing the count for each pair of peaks found in the same frame.
    - This matrix is then normalized and rendered as a grayscale heatmap, where brighter areas indicate a stronger correlation between two frequencies.
