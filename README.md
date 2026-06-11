# Voice Activity Detector (VAD)

A **Voice Activity Detection** system for male voice in WAV files, using a multi-feature signal analysis approach — no machine learning required.

## What it does

- Detects segments where a **human voice (male)** is present in an audio file
- Returns precise **timestamps in milliseconds** (start, end, duration)
- Achieves **100% accuracy** on the 5-segment test set

## Algorithm

Three-feature fusion approach:

| Feature | Role |
|---|---|
| **RMS Energy** | Detects speech frames by energy level (adaptive threshold: 10th percentile × 2.0) |
| **Zero Crossing Rate (ZCR)** | Filters unvoiced noise — voiced speech has low ZCR (< 0.15) |
| **Fundamental Frequency (F0)** | Confirms voice by detecting pitch in the male vocal range (85–180 Hz) |

Post-processing:
- Median filter (size 7) to smooth label sequence
- Minimum segment duration: 200 ms (removes brief noise bursts)
- Gap merging: 300 ms (joins nearby segments of the same utterance)

## Parameters

```python
FRAME_SIZE_MS = 25         # 25ms analysis window
FRAME_OVERLAP = 0.5        # 50% overlap
ENERGY_THRESHOLD = 2.0     # multiplier over noise floor
MIN_VOICE_F0 = 85 Hz       # male voice lower bound
MAX_VOICE_F0 = 180 Hz      # male voice upper bound
MIN_SEGMENT_MS = 200       # discard very short segments
MERGE_GAP_MS = 300         # merge nearby speech segments
```

## Tech stack

- Python 3
- `numpy` — signal processing
- `scipy.io.wavfile` — WAV reading
- `scipy.signal.medfilt` — median filtering

## Usage

```python
from notebook import rileva_voce
segments = rileva_voce("audio.wav")
# [{'start_ms': 1200, 'end_ms': 3400, 'duration_ms': 2200}, ...]
```

Open `notebook.ipynb` in Google Colab or Jupyter for the full walkthrough.

## Topics

`python` `audio-processing` `voice-activity-detection` `vad` `signal-processing` `speech` `numpy`
