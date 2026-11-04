# Pixel Art Text-to-Image Generation

IE 7615 Deep Learning for AI, Generative Project, Fall 2026
Study Group 6: Bingyan Zhu, Muhan Li, Ruoxi Chen

## Goal

General text-to-image models are good at photos and paintings, but they often fail at real pixel art. Their outputs have uneven pixel grids, blurry edges and too many colors. In this project we fine-tune Stable Diffusion on a pixel art dataset so that it can turn a short text prompt into a clean, low-resolution sprite with a small color palette.

## Approach

1. Text encoder. CLIP turns each caption into text embeddings.
2. Image generator. A pretrained Stable Diffusion model creates the image, guided by the text embeddings.
3. Fine-tuning. We train LoRA weights on pixel art image and caption pairs, so the base model stays frozen and training stays light.
4. Evaluation. We compare the base model and the fine-tuned model with FID, CLIP score and simple pixel art checks such as the number of colors used.

## Dataset

We use a subset of the PixelGPT 24x24 dataset by unstonio.

- Source: https://huggingface.co/datasets/unstonio/pixelgpt-24x24-20k
- License: CC BY 4.0. Images and captions belong to the original authors.
- Changes we make: we select a subset of categories and resize images for training. We keep the original train, validation and test splits.

The images are not stored in this repository. The notebooks download them from Hugging Face.

## Repository layout

```
notebooks/   Colab notebooks for data preparation, generation, training and evaluation
results/     Generated images and result tables
docs/        Proposal, milestone summaries and the final report
```

## How to run

The notebooks are written for Google Colab with a GPU runtime. Open a notebook in Colab, choose a GPU under Runtime, Change runtime type, then run the cells from top to bottom.

## Progress

- [ ] Milestone 1. Project setup, dataset choice and baseline prompt tests
- [ ] Milestone 2. Text encoder and diffusion model integration, first fine-tuned results
- [ ] Milestone 3. Evaluation with FID, CLIP score and parameter studies
- [ ] Milestone 4. Final report, results gallery and presentation
