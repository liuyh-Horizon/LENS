# LENS

**LENS: Replacing LayerNorm and Softmax in Transformers with Learnable Normalization States**

Yuhao Liu, Salim Ullah, and Akash Kumar

[Paper on arXiv](https://arxiv.org/abs/2611.20331)

## Overview

LENS replaces LayerNorm and attention Softmax with small learnable MLPs:

* **LENSNorm** learns input-dependent scale and bias states for each token.
* **LENSMax** learns a row state and uses an element-wise MLP to generate attention weights.

The goal is to simplify the design of Transformer hardware accelerators by shifting these computations primarily to existing matrix-computation cores, such as systolic arrays, and removing the dedicated LayerNorm and Softmax units while maintaining model performance. 

## Current Release

This repository currently provides source code and corresponding results for **11 experimental configurations on CIFAR-10 and CIFAR-100**, including the baseline, LENS variants, and ablation experiments. The released experiments cover:

* A single-head Vision Transformer baseline with LayerNorm and Softmax.
* Training with LENSNorm, LENSMax, or both from scratch.
* Recovery training after replacing LayerNorm, Softmax, or both in a trained baseline.
* Training only the LENS modules while freezing the inherited baseline weights.
* Additional ablations, including **LENSNorm+**, which predicts a separate scale and bias pair for each hidden dimension instead of broadcasting one pair across dimensions.

The DeiT/ImageNet and Pythia experiment code is not included in this release.

The standard single-head ViT uses 4 × 4 image patches, a hidden dimension of 128, three Transformer blocks, and one attention head. The main experiments use five seeds: **42, 886, 1024, 1991, and 2333**. Baseline and from-scratch training use 400 epochs; recovery training uses 50 epochs. Refer to each notebook for its complete settings and any ablation-specific differences.

## Results

The corresponding experimental results are provided alongside the released code. ChatGPT (web interface) was used to help organize the released code and remove redundant code.

The paper contains the full result tables and discussion of the training settings, recovery behavior, and ablations.

## Citation

If you find this work useful, please cite:

```bibtex
@misc{liu2026lensreplacinglayernormsoftmax,
      title={LENS: Replacing LayerNorm and Softmax in Transformers with Learnable Normalization States},
      author={Yuhao Liu and Salim Ullah and Akash Kumar},
      year={2026},
      eprint={2611.20331},
      archivePrefix={arXiv},
      primaryClass={cs.LG},
      url={https://arxiv.org/abs/2611.20331},
}
```

