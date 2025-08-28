# Neural Audio Codec Project

**Author:** Taka Khoo  
**Collaborator:** Minh Bui  
**Date:** August 27, 2024  

## Project Overview

This project investigates different quantization methods for neural audio codecs, focusing on speech enhancement tasks. The goal is to compare Vector Quantization (VQ), Residual Vector Quantization (RVQ), and Gumbel-Softmax quantization in a simple speech denoising pipeline.

## Project Structure

```
audio_codec/
├── datasets/              # Speech datasets (VCTK, LibriSpeech)
├── experiments/           # Experiment configurations
│   └── vq_baseline/      # VQ baseline experiment
│       ├── configs/       # Configuration files
│       ├── models/        # Model implementations
│       └── utils/         # Utility functions
├── results/               # Experiment results and outputs
├── docs/                  # Documentation
│   └── quantization_review.md  # Quantization methods review
└── scripts/               # Helper scripts
```

## Setup

### 1. Environment Setup
```bash
# Create and activate conda environment
conda create -n codec-env python=3.10
conda activate codec-env

# Install dependencies
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install scipy pandas matplotlib tqdm pyyaml soundfile librosa hydra-core
```

### 2. Dataset Preparation
- **VCTK**: Multi-speaker English speech corpus
- **LibriSpeech**: Large-scale audiobook dataset
- **Custom noisy speech**: Clean speech + synthetic noise

## Experiments

### Phase 1: VQ Baseline
- Simple autoencoder with VQ bottleneck
- Speech enhancement (denoising) task
- Basic evaluation metrics

### Phase 2: RVQ Comparison
- Multi-stage VQ implementation
- Progressive refinement
- Quality vs. computational cost analysis

### Phase 3: Gumbel-Softmax
- Differentiable quantization
- Training stability comparison
- Advanced evaluation metrics

## Running Experiments

### Basic VQ Training
```bash
cd experiments/vq_baseline
python train.py \
    --epochs 100 \
    --batch-size 16 \
    --lr 1e-3 \
    --codebook-size 512 \
    --embedding-dim 64 \
    --results-dir ../../results/vq_baseline
```

### RVQ Training
```bash
python train.py \
    --epochs 100 \
    --batch-size 16 \
    --lr 1e-3 \
    --vq-type rvq \
    --num-stages 3 \
    --stage-dims 64,64,64 \
    --codebook-size 256,256,256 \
    --results-dir ../../results/rvq_3stage
```

## Evaluation Metrics

- **SI-SDR**: Scale-invariant signal-to-distortion ratio
- **PESQ**: Perceptual evaluation of speech quality
- **STOI**: Short-time objective intelligibility
- **Audio samples**: Noisy, clean, and denoised comparisons

## Results

Results are saved in the `results/` directory with the following structure:
```
results/
├── vq_baseline/
│   ├── checkpoints/       # Model checkpoints
│   ├── audio/            # Audio samples
│   ├── metrics.csv       # Training metrics
│   └── plots/            # Training curves
└── rvq_3stage/
    ├── checkpoints/
    ├── audio/
    ├── metrics.csv
    └── plots/
```

## Key Files

- `docs/quantization_review.md`: Comprehensive review of quantization methods
- `experiments/vq_baseline/models/`: Model implementations
- `experiments/vq_baseline/train.py`: Training script
- `results/`: All experiment outputs and results

## Next Steps

1. **Implement VQ baseline** with simple autoencoder
2. **Add RVQ variants** for comparison
3. **Implement Gumbel-Softmax** quantization
4. **Conduct ablation studies** on key parameters
5. **Write up results** for potential publication

## Contact

- **Taka Khoo**: f004h1v@dartmouth.edu
- **Minh Bui**: [Contact information]

---

**Note:** This project is part of ongoing research on neural audio codecs and federated learning for speech processing.
