# Black & White Image Colorization using Deep Learning

_A research repo for turning grayscale images into plausible color_

---

## TL;DR

This repo hosts the manuscript for our research on **fully automatic image colorization** using a **convolutional neural network (CNN)** trained on **ImageNet**. We predict chrominance in **LAB color space** from a grayscale input and recombine to produce realistic color images—achieving a top-line accuracy of **~85.47%** on our evaluation. We also ran a small user study where participants judged our outputs to be visually convincing in a majority of cases. The method works best on **natural scenes** and **legacy black-and-white photos**; it’s less reliable on some **man-made/structured objects**.

---

## What’s in this repository?

- **Manuscript (DOCX)** — full paper with background, method, experiments, results, and references.
- **No code or datasets are included here**. If/when we add code or supplementary materials, this README will be updated with instructions.

---

## Why this matters

Colorization breathes life into archival photos and films, enhances scientific illustrations, and can aid creative workflows. Historically, high-quality results required manual hints or exemplar images. Our work aims for **high-quality, fully automatic** colorization—no scribbles, no hand-picked exemplars—so it’s practical at scale.

---

## Method (high level)

1. **Input:** a grayscale image (the **L** channel in LAB).
2. **Model:** a CNN predicts a probability distribution over **a/b** chrominance values per pixel (adapted from prior colorization architectures).
3. **Reconstruction:** combine the predicted **a/b** with the input **L**, then convert **LAB → RGB** for the final colorized image.

**Key design choices**
- Operate in **LAB** (decouples lightness from color).
- **8 convolutional blocks**, up/down-sampling for resolution alignment (no pooling layers).
- **Softmax** over quantized color bins to encourage vivid yet coherent colors.

---

## Data & Evaluation

- **Training data:** Images from **ImageNet** (color images; grayscale items filtered out).
- **Evaluation splits:** stratified train/val/test. We also curated:
  - **Legacy B&W set** (archival-style photos)
  - **Man-made objects set** (more structured/engineered content)
- **Metrics & studies:**
  - **Accuracy:** ~**85.47%** on our primary evaluation.
  - **Human study:** a majority of participants found outputs visually plausible on legacy photos.

> Interpretation tip: Colorization targets **plausibility**, not the one “true” historical color. Some scenes admit multiple valid colorizations.

---

## Results at a glance

- ✅ **Natural scenes & legacy photos:** near ground-truth hues in many cases.
- ⚠️ **Man-made/structured objects:** more failure modes (e.g., color bleeding or implausible materials).
- ↔️ **Comparisons:** Performance compares favorably with well-known baselines reported in the literature (details and citations in the manuscript).

---

## Limitations & responsible use

- **Ambiguity:** Many grayscale scenes have multiple valid colors; treat outputs as **best-guess** colorizations.
- **Historical authenticity:** Avoid presenting colorized images as definitive historical truth without corroborating evidence.
- **Domain shift:** Performance degrades on domains unlike the training data (e.g., diagrams, synthetic content, some man-made objects).

---

## Frequently asked (quick answers)

- **Can I use this for videos?** The paper focuses on images. Video colorization needs temporal consistency; the approach could be extended with temporal models.
- **Can I reproduce your results?** You’ll need an ImageNet-scale training setup and a color-classification CNN in LAB space; see the paper for architecture and training details.

---

## Authors & contact

- **Apurva Anand**
- **Suhaas Srungavarapu**
- **Utkarsh Anand**
- **Anand Bihari** (corresponding author)

For questions: **anand.bihari@vit.ac.in**

---

## Acknowledgments

- **ImageNet** for dataset resources.
- Prior research in scribble-based, exemplar-based, and deep colorization—full citations are in the manuscript’s References section.

---

_Thanks for stopping by! If this work interests you, feel free to ⭐ the repo and open an issue with questions or collaboration ideas._
