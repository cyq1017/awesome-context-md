# CONTEXT.md — ML / AI Project

<!-- Replace "Project Name" with your actual project name -->

## What

**Project Name** is a [classification/generation/retrieval/RAG] system that [does X with Y model for Z users].

- **Task type**: [Text Classification / Image Generation / RAG / Multi-modal]
- **Model**: [GPT-4 / BERT / Custom fine-tuned / CLIP]
- **Inference**: [API call / local GPU / cloud endpoint]

## Architecture

```
project-name/
├── src/
│   ├── data/
│   │   ├── loader.py         # Dataset loading & preprocessing
│   │   ├── augmentation.py   # Data augmentation pipelines
│   │   └── splits.py         # Train/val/test split logic
│   ├── models/
│   │   ├── base.py           # Base model class / interface
│   │   ├── classifier.py     # Main model architecture
│   │   └── losses.py         # Custom loss functions
│   ├── training/
│   │   ├── trainer.py        # Training loop
│   │   ├── evaluation.py     # Metrics computation
│   │   └── callbacks.py      # Early stopping, checkpointing
│   ├── inference/
│   │   ├── predictor.py      # Single/batch prediction
│   │   └── pipeline.py       # End-to-end inference pipeline
│   └── utils/
│       ├── config.py         # Experiment configuration
│       └── logging.py        # Experiment tracking (W&B, MLflow)
├── configs/
│   ├── base.yaml             # Default hyperparameters
│   └── experiment_01.yaml    # Experiment-specific overrides
├── data/
│   ├── raw/                  # Original data (gitignored)
│   └── processed/            # Preprocessed data
├── checkpoints/              # Model weights (gitignored)
├── notebooks/                # Exploration & analysis
├── scripts/
│   ├── train.py              # `python scripts/train.py --config configs/base.yaml`
│   ├── evaluate.py           # `python scripts/evaluate.py --checkpoint best.pt`
│   └── predict.py            # `python scripts/predict.py --input data.json`
├── requirements.txt
└── README.md
```

### Pipeline

```
Raw Data → Preprocessing → DataLoader → Model → Loss → Optimizer → Checkpoint
                                          ↓
                                   Evaluation Metrics → Experiment Tracker
```

## Tech Stack

| Layer | Technology | Notes |
|-------|-----------|-------|
| Framework | PyTorch 2.x | <!-- or TensorFlow, JAX --> |
| Models | HuggingFace Transformers | Pre-trained model hub |
| Data | pandas + datasets | HuggingFace datasets for loading |
| Config | OmegaConf / YAML | Hierarchical config |
| Tracking | Weights & Biases | <!-- or MLflow, TensorBoard --> |
| GPU | CUDA 12.x | Tested on A100/V100 |
| Serving | FastAPI | <!-- or TorchServe, Triton --> |
| Testing | pytest | Unit tests for data/model |

## Key Files

| File | Purpose | Read When |
|------|---------|-----------|
| `configs/base.yaml` | All hyperparameters | Tuning model |
| `models/classifier.py` | Model architecture | Modifying model |
| `training/trainer.py` | Training loop | Debugging training |
| `data/loader.py` | Dataset processing | Data pipeline issues |
| `inference/pipeline.py` | Production inference | Deployment changes |
| `scripts/train.py` | Entry point | Running experiments |

## Conventions

- **Config-driven**: All hyperparameters in YAML, never hardcoded
- **Reproducibility**: Random seeds set in config, logged with each run
- **Data**: Raw data never modified — always create processed versions
- **Checkpoints**: Save model + optimizer + epoch + metrics
- **Logging**: Use structured logging, log all key metrics per epoch
- **Naming**: `experiment_{date}_{description}` for runs

## Current State

| Component | Status | Notes |
|-----------|--------|-------|
| Data pipeline | ✅ Done | Handles [X] samples |
| Base model | ✅ Done | [X]% accuracy on test set |
| Fine-tuning | 🚧 WIP | Testing with [Y] dataset |
| API serving | 📋 Planned | FastAPI endpoint |

## Gotchas

- GPU memory: Batch size > 32 will OOM on 24GB GPUs with this model
- Data loading: Set `num_workers=0` on macOS to avoid multiprocessing issues
- Mixed precision: `torch.cuda.amp` requires CUDA — use CPU fallback for local dev
- Tokenizer: Max sequence length is [512] — longer inputs are silently truncated
- Checkpoints: ~[2GB] each — don't commit to git, use cloud storage
