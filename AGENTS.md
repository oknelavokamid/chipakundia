# AGENTS.md — Base44 Dev Environment

## Project Overview
Chipakundia is a music creation platform using speech-to-music / RNN-based music generation.
The repo contains:
- `Chipakundia` — standalone Python script for analyzing complex musical meters (odd time signatures, accent patterns). Pure Python, no external deps.
- `site/en/tutorials/audio/music_generation.ipynb` — Jupyter notebook based on TensorFlow's music generation tutorial, adapted for Chipakundia. Uses TensorFlow, pretty_midi, fluidsynth.

## Running the App
```bash
docker compose -f docker-compose.base44.yml up -d --build
```
Serves Jupyter Lab on port 3000 (no token/password — dev mode).

## Key Notes
- The notebook was originally designed for Google Colab. Several cells reference `/content/` paths and use `!sudo apt install` / `!pip install` commands. These Colab-specific cells will error in Jupyter but the notebook is still viewable and most analysis cells work.
- The `Chipakundia` script can be run standalone: `python Chipakundia`
- Dependencies are pre-installed in the Docker image (Dockerfile.base44): TensorFlow, pretty_midi, pyfluidsynth, pandas, numpy, seaborn, matplotlib, jupyterlab.
- No external credentials are required.

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/lab` should return 200
- Healthcheck: `docker compose -f docker-compose.base44.yml ps` shows status "healthy"
