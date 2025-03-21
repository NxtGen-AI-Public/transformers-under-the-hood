# Transformer Architecture - README

## Overview

This repository contains a detailed PowerPoint presentation on the Transformer architecture, including self-attention, multi-head attention, positional encoding, and other crucial concepts. Below is a comprehensive explanation of the key concepts covered in the presentation.

---

## **Self-Attention Mechanism**

1. **Word Embeddings**: Capture the semantic meaning of words.
2. **Contextual Understanding Issue**: Static embeddings may fail to differentiate between polysemous words (e.g., "apple" as fruit vs. "apple" as a company).
3. **Dynamic Contextual Embeddings**: Self-attention helps adjust embeddings dynamically based on context.
4. **Process**:
   - Static embeddings → Self-attention → Contextual embeddings.
   - Example:
     - "Money bank grows" → `bank = 0.3(money) + 0.7(bank) + 0.1(grows)`.
     - "River bank flows" → `bank = 0.5(river) + 0.4(bank) + 0.1(flows)`.
5. **Mathematical Representation**:
   - Compute similarity between embeddings using dot product.
   - Normalize using Softmax and apply dot product to get new contextual representation.
   - This process provides a general contextual embedding but needs task-specific embeddings.
6. **Query, Key, Value Concept**:
   - Every word has three components: **Query (Q)**, **Key (K)**, and **Value (V)**.
   - These components help the model learn different aspects of words.
7. **Mathematical Computation of Q, K, V**:
   - Apply separate linear transformations to a word vector using weight matrices.
   - The weight matrices are learned through backpropagation.
   - `Q, K, V = Wq * X, Wk * X, Wv * X` (where X is input word vector).
   - The attention score is computed as `Q * K^T` (dot product).
8. **Importance**:
   - Helps determine what the model "sees" and "responds" to.

## **Limitations of Self-Attention**

1. **Ambiguous Sentences**:
   - "The man saw the astronomer with a telescope" → Unclear if the telescope belongs to the man or the astronomer.
   - Self-attention may not always capture multiple interpretations.

## **Multi-Head Attention**

1. **Concept**:
   - Instead of a single attention mechanism, multiple sets of weight matrices (**Wq, Wk, Wv**) are used.
   - Multiple contextual vectors are obtained.
2. **Computation**:
   - The vectors are concatenated and passed through a linear transformation.
   - Example:
     - If two heads are used, the vectors are of size `2x4`, concatenated to form a `2x8` matrix.
     - A weight matrix `W0 (8x4)` is applied to transform it back to `2x4`.

## **Positional Encoding**

1. **Why Needed?**
   - Self-attention processes words in parallel, losing the word order information.
2. **Solution**:
   - Introduce positional encodings using periodic functions (sine, cosine).
   - Provides a bounded, continuous, periodic function to capture relative positioning.
3. **Mathematical Representation**:
   - `PE(pos, 2i) = sin(pos / 10000^(2i/d))`
   - `PE(pos, 2i+1) = cos(pos / 10000^(2i/d))`
   - This encoding is added to the word embeddings.

## **Layer Normalization**

1. **Purpose**:
   - Normalizes activations to stabilize training, speed up convergence, and mitigate internal covariate shift.
2. **Difference from Batch Normalization**:
   - Batch normalization is applied across the batch, while layer normalization is applied to each individual sample.
   - Self-attention benefits more from layer normalization.

## **Transformer Encoder**

1. **Feed-Forward Network (FFN)**:
   - 2-layer network:
     - First layer: **2048 neurons, ReLU activation**.
     - Second layer: **512 neurons, Linear activation**.
2. **Residual Connections**:
   - Inspired by ResNet to stabilize training and reduce vanishing gradient problems.
3. **Why 6 Encoder Layers?**
   - Helps increase reasoning and language understanding.
   - The number of layers can be modified.

## **Transformer Decoder & Masked Self-Attention**

1. **Autoregressive vs. Non-Autoregressive**:
   - Training: Non-autoregressive (teacher forcing used).
   - Inference: Autoregressive (predict one word at a time).
2. **Masked Self-Attention**:
   - Ensures the decoder does not see future tokens to prevent data leakage.
   - Implements masking by setting future token scores to `-inf`, forcing attention weights to zero.
3. **Cross-Attention**:
   - Occurs between encoder output and decoder input.
   - Helps the decoder focus on relevant parts of the input sequence.
4. **Final Decoder Output**:
   - Passed through a linear layer (`size = vocabulary size`).
   - Softmax applied to get word probabilities.
   - The word with the highest probability is selected as output.

## **Inference Process**

1. **Training Mode**:
   - The entire target sequence is provided at once (non-autoregressive).
2. **Prediction Mode**:
   - The decoder generates words one-by-one (autoregressive).
   - The first token `<sos>` is passed through the decoder.
   - The output word is fed back into the decoder at the next time step.
   - The process repeats until the end token `<eos>` is generated.

---

## **Conclusion**

This repository serves as a resource to understand the Transformer architecture in depth. It covers self-attention, multi-head attention, positional encoding, layer normalization, and the encoder-decoder structure. The included PPT visually illustrates these concepts.

### **References**

- Vaswani et al., "Attention Is All You Need," NeurIPS 2017.
- Campusx youtube channel

**Happy Learning! 🚀**

