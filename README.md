VocalSynth

Parametric voice generation built on CosyVoice3. Instead of picking preset voices from a library, you shape a voice with continuous controls: gender, age, brightness, breathiness, all on sliding scales.

Architecture

Two-layer control system, discovered through measurement rather than designed upfront:

Vector layer (CAM++ embedding space)

Steers identity-level voice properties (gender, age) through vector transport in the CAM++ speaker embedding space. These properties have wide, clean separations in the embedding space, which makes interpolation between them reliable. This is the part that works.

DSP layer (post-engine processing)

Handles timbral properties: brightness, breathiness. These don't separate cleanly in the embedding space, so they can't be steered the same way. Current approach uses DSP post-processing after the CosyVoice3 engine output. Functional, but not where it needs to be.

Data pipeline

Source material: 15 years of almost daily studio voice recordings, all made with the same signal chain (Brauner Phantom V, same preamp, same compressor, same room). That consistency is the key asset. The recording chain becomes invisible to the embedding model, so what remains is a clean voice identity signal.

Pipeline stages:

Voice extraction from raw session recordings
Speaker clustering using ECAPA-TDNN embeddings
Quality gating to filter unusable segments
Deduplication across tens of thousands of source files

Current dataset:

2,600+ distinct speakers
300+ hours of clean, processed audio
Roughly the same volume of unprocessed raw material remaining in the archive
Speaker verification

Tested 64 synthesized voices against 5,622 real voice centroids using ECAPA-TDNN speaker embeddings. All 64 were confirmed as strangers (no match to any existing speaker in the dataset). The system generates new voices, not clones.

Stack
Component	Role
CosyVoice3	Speech synthesis engine
CAM++	Speaker embedding space (vector layer control)
ECAPA-TDNN	Speaker verification and clustering
silero-VAD	Voice activity detection
WORLD vocoder	Acoustic decomposition (pitch, spectral envelope, aperiodicity)
Python	Pipeline and tooling
Status

Working prototype. The vector layer (identity control) is solid. The timbral layer (brightness, breathiness) needs better separation methods. The DSP workarounds are functional but the real solution is probably doing this inside a stronger synthesis engine rather than post-processing.
