# Psiren

Psiren is a comprehensive, high-performance audio processing application designed for both real-time filtering and post-production audio repair. It leverages a custom C++ backend with optional CUDA acceleration for its core digital signal processing (DSP) and a feature-rich Python frontend built with PyQt5.

## Features

- **Three Powerful Modes:**
  - **Live Mode:** For real-time microphone audio processing.
  - **Studio Mode:** For detailed, file-based audio repair and enhancement.
  - **Warmth Mode:** For applying analog-style saturation and drive.
- **Advanced DSP Core:** Utilizes a 1D Perona-Malik Gradient Filter (PGF) for sophisticated, content-aware audio processing. The algorithm's principles are derived from MTS (Motion-Timrspace) physics engine.
- **Interactive Waveform Editor:** A fully interactive editor in Studio Mode with zoom, pan, a synchronized playhead, and visual markers for detected audio clips.
- **Real-time Recording:** Capture the output of the Live Filter directly to a `.wav` file.
- **Full Undo/Redo System:** A robust, multi-level undo/redo history for all destructive operations in Studio Mode.
- **Batch Processing:** Apply any Studio module's effect to an entire folder of audio files at once.
- **Global Keyboard Shortcuts:** Control playback, saving, and undo/redo from anywhere in the application.
- **Robust Error Handling:** User-friendly dialogs for common issues like loading unsupported audio formats.

---

## Modes of Operation

### 1. Live Mode
Designed for real-time applications like streaming or online communication. It captures audio from a selected microphone, processes it, and routes it to a virtual audio output.

- **Controls:** Denoise Amount, Sensitivity (K), Quality (Steps).
- **Real-time Meters:** Visual feedback for both input and output audio levels.
- **Recording:** Capture the processed audio stream to a timestamped `.wav` file in the `recordings/` directory.

### 2. Studio Mode
The central hub for audio post-production and repair. Load an audio file and use a suite of powerful modules to clean and enhance it.

- **Modules:**
  - **Denoise:** Reduce background noise.
  - **De-Clip:** Reconstruct and repair clipped audio sections.
  - **De-Click:** Remove clicks and pops.
  - **Clarity:** Enhance the presence and detail of the audio.
- **Workflow:**
  1. Load a `.wav` or `.flac` file.
  2. Use the interactive waveform to inspect the audio.
  3. Select a module and adjust its parameters with real-time preview.
  4. For De-Clip, use "Detect Clips" to see visual markers on the waveform, then "Repair Clips" to apply the fix.
  5. Use the Undo/Redo buttons or shortcuts to step through changes.
  6. Save the final processed audio to a new file.

### 3. Warmth Mode
A creative tool for adding analog-style saturation and harmonic distortion.

- **Controls:**
  - **Drive:** A large dial to control the amount of saturation.
  - **Quality (Steps):** Adjusts the fidelity of the algorithm.
- **Workflow:** Load any audio file, adjust the Drive knob to taste, and use "Save As..." to export the result.

---

## Technology Stack

- **Backend:** C++17 with an optional CUDA backend for GPU-accelerated processing of the PGF algorithm.
- **Frontend:** Python 3 with PyQt5 for the graphical user interface.
- **Bridge:** `ctypes` is used to create a high-performance bridge between the Python frontend and the C++ shared library (`pgf_engine.dll`).
- **Core Libraries:**
  - `NumPy`: For all numerical and audio data manipulation.
  - `SoundDevice`: For real-time audio I/O in Live Mode.
  - `SoundFile`: For reliable loading and saving of `.wav` and `.flac` files.

---

## Installation and Usage

### Prerequisites
- Python 3.8+
- CMake (must be in system PATH)
- A C++ compiler (e.g., MSVC on Windows)
- (Optional) NVIDIA GPU with CUDA Toolkit installed for GPU acceleration.

### Steps
1. **Clone the repository:**
   ```bash
   git clone <your-repo-url>
   cd PGF_AUDIO_SUITE
   ```

2. **Install Python dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Build the C++ Engine:**
   The C++ engine is built automatically when you run the `setup.py` script.
   ```bash
   python setup.py build
   ```
   This will create the `pgf_engine.dll` (or `.so` on Linux) in the `pgf_app` directory.

4. **Run the Application:**
   ```bash
   python main.py
   ```

---

## Keyboard Shortcuts

- **`Spacebar`**: Toggle Play/Pause in the active mode.
- **`Ctrl+S`**: Save the currently loaded file (in Studio or Warmth mode).
- **`Ctrl+Z`**: Undo the last action (in Studio mode).

- **`Ctrl+Y`**: Redo the last undone action (in Studio mode).
