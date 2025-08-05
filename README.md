# VIO: A Mamba-Inspired Lightweight Architecture for Sequence Modeling

> **DNA mutation classification made simple, fast, and transformer-free.**

---

## 🔬 Overview

**VIO** is a custom-designed neural architecture inspired by the Mamba state-space model, tailored for efficient sequence modeling tasks — especially in bioinformatics. Unlike traditional transformer-based models, VIO leverages gated depthwise convolutions and layer normalization to model sequential data with drastically reduced computational overhead, making it ideal for environments like Google Colab where transformer variants (like Mamba) are difficult to deploy.

---

## 🧠 Why VIO Instead of Transformers?

Transformers revolutionized sequence modeling but come with major downsides:

* ⚠️ **Quadratic complexity** with respect to sequence length due to attention mechanisms
* ⚠️ High VRAM and compute requirements — infeasible on entry-level GPUs
* ⚠️ Overkill for tasks requiring local pattern recognition rather than global context

**VIO outperforms transformers in practical scenarios like bio-sequence modeling by:**

* ✅ Replacing attention with **depthwise separable convolutions**, ideal for capturing local motifs
* ✅ Using **gated activations**, which mimic selective memory updates seen in Mamba
* ✅ Being **hardware-efficient and deployable in Google Colab** with no specialized libraries
* ✅ Offering **faster training and inference** with simpler backpropagation dynamics
* ✅ Requiring only standard PyTorch layers — minimal overhead, easier debugging

In tasks where sequence locality dominates — such as DNA or protein sequence classification — VIO provides a better accuracy-efficiency tradeoff than full transformers.

---

## 💡 Architecture Highlights

* **VIOBlock**: Performs depthwise 1D convolution on each channel separately

  * Gated pathway via a learnable sigmoid layer
  * LayerNorm to stabilize training across layers
* **VIOModel**:

  * Projects one-hot input into higher-dimensional embeddings
  * Stacks multiple VIOBlocks for deep feature extraction
  * Aggregates final representation via `AdaptiveAvgPool1D`
  * Outputs class predictions through a simple linear classifier

---

## 🧬 Use Case: DNA Mutation Identifier

This project includes a DNA mutation classifier as a real-world use case.

The model:

* Ingests one-hot encoded nucleotide sequences (A, C, G, T, N)
* Processes sequences using 4 stacked VIOBlocks
* Predicts the gene mutation class from learned representations
* Achieves **\~80% test accuracy** on a curated dataset of gene types

---

## 🚀 How to Test the Model Yourself

> ### 🧪 Run your own experiments directly in Google Colab:
* copy the google collab in drive and make sure to upload the test.csv file 
* then run the codes, Simple as that!


🧠 Pro Tip: You can also plug in time-series data, audio signals, or any other 1D sequences with minor modifications to the encoder.

---

## ⚡ Performance & Simplicity

* **\~80% Accuracy** on a curated real-world genomic dataset
* Full training pipeline runs on Colab within minutes
* Zero external model dependencies (no HuggingFace, no Mamba setup required)
* Easy to extend to other domains (protein folding, time-series, ECG, etc.)

---=

## 🔓 License

This project is released under the [MIT License](LICENSE). You can use, modify, and distribute it freely — for research, commercial use, or educational purposes. Just give credit.

---

## 🤝 Contributing

Pull requests are welcome! If you plan to extend VIO to other tasks (e.g., protein classification, sentiment analysis, medical time series), open an issue or drop a fork.

---

## 🌟 Final Note

**VIO is proof that you don’t need heavyweight attention mechanisms to solve real problems.** With a compact, Mamba-inspired core and real-world biological application, VIO makes sequence modeling accessible, fast, and effective.

Made with 🔥 by Shaheer
