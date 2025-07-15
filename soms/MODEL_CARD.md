# Model Card: CLIPedia SOM (240805)

**Model:** CLIPedia Self-Organizing Maps  
**Date:** 2024-08-05

## Description
SOM models trained on CLIP-encoded Wikipedia embeddings.

## Files
- `globalSom.wxf` — global SOM
- `localSoms_0-512.wxf` — local SOMs, part 1
- `localSoms_513-1024.wxf` — local SOMs, part 2

## Training
- **Data:** Wikipedia dump (Apr 2024)
- **Framework:** Mathematica 13.2 + GTX 3080 Ti
- **Iterations:** Trained for 32, 18 picked
- **Neighborhood:** exponential decay