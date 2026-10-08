# VocalSynth

Parametric voice generation. Instead of picking preset voices from a list, shape a voice with continuous controls: gender, age, brightness, breathiness, all on sliding scales.

## What it does

Built on CosyVoice3. Two-layer control architecture, discovered through measurement:

- **Vector layer** (CAM++ embedding space): steers identity properties like gender and age. Wide separations make this reliable.
- **DSP layer** (post-engine): timbral properties like brightness and breathiness. These don't separate cleanly in the embedding space. Functional, not solved yet.

## Dataset

Curated from 25 years of studio recordings. Same microphone (Brauner Phantom V), same preamp and compressor chain, same room. That consistency makes the recording chain invisible to the embedding model.

- 2,600+ distinct speakers
- 300+ hours clean audio
- Roughly the same volume of unprocessed raw material remaining

## Verification

64 synthesized voices tested against 5,622 real voice centroids using ECAPA-TDNN speaker embeddings. All 64 confirmed as strangers. The system generates voices that don't exist, not clones.

## Tools

- ECAPA-TDNN (speaker embeddings)
- silero-VAD (voice activity detection)
- WORLD vocoder (pitch, spectral envelope, aperiodic decomposition)
- Python

## Status

Working prototype. Vector layer works well. Timbral layer needs better separation.
