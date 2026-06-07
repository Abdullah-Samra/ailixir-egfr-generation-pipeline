---
pretty_name: EGFR AI Backend Bundle
license: other
tags:
- egfr
- drug-discovery
- reinvent4
- deeppurpose
- autodock-gpu
- backend-bundle
private: true
---

# EGFR AI Backend Bundle

Minimal private backend artifact bundle for the EGFR AI demo.

This package is designed for internal backend integration only. It intentionally does not include the original research RL scoring files, raw training dataset, or full experiment history.

## Components

### 1. Generator

Packaged checkpoint:

- `models/generator/egfr_generator.chkpt`

Sampling config:

- `configs/sampling_model.bundle.toml`

This mode samples molecules from the packaged generator checkpoint. It does not continue RL training.

### 2. Affinity service

Server:

- `services/deeppurpose/serve_affinity.py`

Model files:

- `models/affinity/model.pt`
- `models/affinity/config.pkl`
- `models/affinity/target_sequence.txt`

Run:

```bash
cd ai_artifacts_release
export PYTHONPATH="$PWD:$PYTHONPATH"
uvicorn services.deeppurpose.serve_affinity:app --host 127.0.0.1 --port 8001
```

## Demo status

This Space is a CPU demo for backend/frontend integration.

Real AutoDock-GPU docking is disabled in this Space, but docking fields are included in the response schema for database and frontend implementation.