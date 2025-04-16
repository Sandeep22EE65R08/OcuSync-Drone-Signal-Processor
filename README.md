author: Sandeep kumar

# jupyter notebook


# OcuSync-Drone-Signal-Processor
developed DSP pipeline for ocusync drone signal

# DJI OcuSync Signal Processing Project

This project provides a complete digital signal processing (DSP) pipeline for analyzing raw complex baseband recordings of DJI's OcuSync communication systems (OcuSync 1, 2, and 3). The recordings are stored in `.dat` files as complex64 I/Q samples and are processed using a suite of Jupyter notebooks to detect signal packets, perform frequency offset correction, analyze spectrum and power features, and extract meaningful patterns.

All the code is written and executed using **Jupyter Notebooks**, which allows easy visualization, step-by-step debugging, and interactive parameter control.

---

## 🔧 Project Workflow

The project consists of the following key processing steps:

### ✅ Step 1: Spectrogram Visualization
- **Objective**: Generate time-frequency spectrograms of complex baseband signals.
- **Notebook**: `01_spectrogram_viewer.ipynb`
- **Data**:  "1": ("/home/sandeep/Ocusync1_40msps.dat", 40e6),
    "2": ("/home/sandeep/Ocusync2_50msps.dat", 50e6),
    "3": ("/home/sandeep/Ocusync3_40msps.dat", 40e6),
- **Highlights**: Interactive CLI to select files and plot spectrograms using `matplotlib.specgram`.

### ✅ Step 2: PSD Analysis using Welch's Method
- **Objective**: Analyze signal power distribution using Power Spectral Density.
- **Notebook**: `02_psd_analysis.ipynb`
- **Technique**: Welch's method with Hamming window, FFT shift for baseband.
- **Output**: Mean PSD values in V²/Hz printed per file.

### ✅ Step 3: Frequency Spectrum (FFT)
- **Objective**: Compute and plot magnitude spectrum.
- **Notebook**: `03_fft_spectrum.ipynb`
- **Method**: Uses `np.fft.fft` and `fftshift` to center spectrum at 0 Hz.

### ✅ Step 4: Bandpass Filter and Energy-Based Packet Detection
- **Objective**: Isolate frequency bands and detect bursts based on signal energy.
- **Notebook**: `04_packet_detection.ipynb`
- **Filters**: 4th-order Butterworth, custom frequency bands per dataset.
- **Detection**: Sliding window energy thresholding. Packet duration filtering.

### ✅ Step 5: Frequency Offset Estimation & Correction
- **Objective**: Estimate and correct carrier frequency offset of signal packets.
- **Notebook**: `05_frequency_offset_correction.ipynb`
- **Steps**:
  - Welch PSD of each packet
  - Identify high-energy spectral bands
  - Apply frequency correction with complex exponential
- **Output**: Offset values printed per packet (e.g. -12.07 MHz)

### ✅ Step 6: PSD and FFT Analysis of Corrected Packets
- **Notebook**: `06_filtered_psd_fft.ipynb`
- **Features**: 
  - Welch PSD (mean)
  - FFT spectrum and peak frequency (e.g. 5175.78 kHz)

### ✅ Step 7: DFT-Based Lowpass Filtering
- **Objective**: Clean signal using FFT-domain low-pass filtering.
- **Notebook**: `07_dft_filtering.ipynb`
- **Cutoff Frequency**: 7.5 or 8.5 MHz depending on signal type.

### ✅ Step 8: Spectral Visualization of Filtered Packets
- **Objective**: Analyze frequency characteristics of filtered packets.
- **Notebook**: `08_filtered_spectrum.ipynb`
- **Plots**: Magnitude spectrum using `fft` and `fftshift`.

### ✅ Step 9: PSD of Filtered Packets
- **Notebook**: `09_filtered_psd.ipynb`
- **Goal**: Validate frequency domain filtering.
- **Output**: PSD mean values (V²/Hz) per packet.

### ✅ Step 10: Pattern Detection (Matched Filtering)
- **Objective**: Detect fixed-length patterns within filtered packets.
- **Notebook**: `10_pattern_detection.ipynb`
- **Method**:
  - Use reference pattern (e.g. 70 µs) from first packet
  - Cross-correlation with entire signal
  - Adaptive thresholding and peak detection
  - Plot time-frequency spectrogram per pattern

### ✅ Step 11: Statistical Feature Extraction (Skewness, Kurtosis)
- **Notebook**: `11_moment_stats.ipynb`
- **Features**: Moment-based analysis on magnitude of patterns
- **Output**: Skewness, excess kurtosis, and KDE plots

---

## 🗂️ Data Files and Configuration

| Index | File Path                                                                 | Sample Rate |
|-------|---------------------------------------------------------------------------|--------------|
| 1     | `/home/sandeep/Ocusync1_40msp.dat`                                        | 40 MSps      |
| 2     | `/home/sandeep/Ocusync2_50msps.dat`                                       | 50 MSps      |
| 3     | `/home/sandeep/Ocusync3_40msps.dat`                                       | 40 MSps      |

All notebooks allow selection of the dataset using numeric index (1, 2, 3).

---

## 📊 Project Highlights
- Full end-to-end signal processing of real RF drone recordings
- Compatible with OcuSync 1, 2, 3
- Modular Jupyter Notebook architecture
- Spectral and temporal analysis
- Pattern-level detection and visualization
- Statistical signal feature extraction

---

## ⚙️ Requirements
```
pip install numpy scipy matplotlib seaborn tqdm jupyterlab
```

---

## ▶️ How to Run
Launch JupyterLab or Jupyter Notebook:
```bash
jupyter lab
```
Open and execute the notebooks in order or as needed:
- `01_spectrogram_viewer.ipynb`
- `02_psd_analysis.ipynb`
- ...

---

## 👁️ Visualization Examples
- Spectrograms of each OcuSync mode
- Frequency spectra before and after filtering
- KDE plots of pattern distributions

---

## 💡 Future Work
- Integrate SNR-based packet classification
- Add decoding support for packet content
- Train ML classifier using extracted pattern stats

---

## 🔐 License
MIT License

---



