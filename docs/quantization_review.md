# Neural Audio Codec: Quantization Methods Review

**Author:** Taka Khoo  
**Date:** August 27, 2024  
**Project:** Neural Audio Codec with Minh Bui  

## Overview
This document provides a comprehensive review of different quantization methods for neural audio codecs, focusing on their strengths, weaknesses, and applications in speech/music processing. This review is based on the paper: https://arxiv.org/pdf/2506.10274

## 1. Vector Quantization (VQ)

### How it works
- Maps continuous vectors to discrete codebook entries
- Each vector is replaced by the closest codebook vector (Euclidean distance)
- Codebook is learned during training

### Strengths
- Simple and stable training
- Deterministic encoding/decoding
- Memory efficient
- Fast inference

### Weaknesses
- Limited expressivity (codebook size constraint)
- Codebook collapse risk
- Poor gradient flow (straight-through estimator needed)
- Fixed bitrate per vector

### Usage in Speech/Music Codecs
- EnCodec (Meta): Uses VQ for speech compression
- SoundStream (Google): VQ bottleneck for audio generation
- Jukebox (OpenAI): VQ for music representation

## 2. Residual Vector Quantization (RVQ)

### How it works
- Multiple VQ stages in sequence
- Each stage quantizes the residual from previous stages
- Progressive refinement of quantization

### Strengths
- Higher expressivity than single VQ
- Better reconstruction quality
- Hierarchical representation
- Variable bitrate control

### Weaknesses
- Higher computational cost
- Sequential processing (not parallelizable)
- Accumulation of quantization errors
- More complex training

### Usage in Speech/Music Codecs
- EnCodec: Multi-stage VQ for high-quality compression
- SoundStream: RVQ for progressive audio generation
- Neural speech synthesis systems

## 3. Product Quantization (PQ)

### How it works
- Splits vectors into subvectors
- Each subvector is quantized independently
- Parallel quantization across subspaces

### Strengths
- Highly parallelizable
- Memory efficient
- Good for high-dimensional vectors
- Fast encoding/decoding

### Weaknesses
- Suboptimal for correlated dimensions
- May lose global structure
- Not always perceptually robust
- Fixed subspace partitioning

### Usage in Speech/Music Codecs
- Less common in audio, more in image/video
- Could be applied to mel-spectrogram features
- Useful for large-scale audio retrieval

## 4. Gumbel-Softmax Quantization

### How it works
- Differentiable approximation of discrete sampling
- Uses Gumbel distribution for relaxation
- Continuous during training, discrete during inference

### Strengths
- Differentiable (no straight-through estimator)
- Better gradient flow
- Can learn codebook assignments
- Flexible training

### Weaknesses
- Temperature scheduling complexity
- May not converge to true discrete solution
- Higher computational cost
- Potential mode collapse

### Usage in Speech/Music Codecs
- Emerging research area
- VALL-E (Microsoft): Uses Gumbel-Softmax for speech synthesis
- Could improve training stability

## 5. Comparison Table

| Method | Capacity | Bitrate Control | Train Stability | Inference Cost | Perceptual Quality | Code Complexity |
|--------|----------|-----------------|-----------------|----------------|-------------------|-----------------|
| VQ | Low | Fixed | High | Low | Medium | Low |
| RVQ | Medium | Variable | High | Medium | High | Medium |
| PQ | Medium | Fixed | High | Low | Medium | Medium |
| Gumbel-Softmax | High | Variable | Medium | Medium | High | High |

## 6. Research Questions for Our Project

### Speech Enhancement Focus
1. **Which quantization method works best for denoising?**
   - VQ: Simple baseline
   - RVQ: Better quality, higher cost
   - Gumbel-Softmax: Differentiable alternative

2. **Dataset considerations:**
   - VCTK: Multi-speaker, clean speech
   - LibriSpeech: Large-scale, diverse content
   - Custom noisy speech: Synthetic noise addition

3. **Evaluation metrics:**
   - SI-SDR improvement
   - PESQ/STOI (if available)
   - Perceptual quality (informal listening)

### Implementation Plan
1. **Phase 1:** VQ baseline with simple autoencoder
2. **Phase 2:** RVQ with 2-4 stages
3. **Phase 3:** Gumbel-Softmax comparison
4. **Phase 4:** Ablation studies and optimization

## 7. Next Steps

1. **Read the arXiv paper thoroughly** (2506.10274)
2. **Set up simple speech enhancement baseline**
3. **Implement VQ bottleneck first**
4. **Compare with RVQ variants**
5. **Document results and insights**

## 8. References

- [EnCodec: High Fidelity Neural Audio Compression](https://arxiv.org/pdf/2210.13438)
- [SoundStream: An End-to-End Neural Audio Codec](https://arxiv.org/pdf/2107.03312)
- [VALL-E: Neural Codec Language Models are Zero-Shot Text to Speech Synthesizers](https://arxiv.org/pdf/2301.02111)
- [Neural Speech Synthesis with Transformer Network](https://arxiv.org/pdf/1809.08895)

---

**Note:** This document will be updated as we progress through the experiments and gain deeper insights into each quantization method's performance on speech enhancement tasks.
