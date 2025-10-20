
#  BERT2GPT2: English → French Neural Machine Translation

This project implements a **Neural Machine Translation (NMT)** system using a hybrid **BERT (encoder)** and **GPT-2 (decoder)** architecture.  
It translates English sentences into French through a transformer-based encoder–decoder pipeline with a custom-built cross-attention mechanism.

---

##  Project Overview

The goal of this project is to build a complete translation system by combining two pretrained models:  
- **BERT-base-uncased** as the **encoder** for English sentence understanding  
- **dbddv01/gpt2-french-small** as the **decoder** for French text generation  

A **custom cross-attention layer** was designed to connect the encoder’s output (context representations) to the decoder’s input, allowing the model to learn the alignment between English and French sentences.

---

##  Model Architecture

1. **Encoder (BERT):** processes the English text and extracts contextual embeddings for each token.  
2. **Cross-Attention:** computes the relationship between the decoder queries and encoder outputs using:

   \[
   \text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^\top}{\sqrt{d_k}}\right)V
   \]
   
   This mechanism lets the decoder "attend" to relevant parts of the input sentence when predicting the next word.
3. **Decoder (GPT-2):** generates the French translation word by word, guided by the encoder’s information.  
4. **Training:** the model was fine-tuned end-to-end on a bilingual dataset using a CrossEntropy loss.

---

##  Dataset

Dataset used: **Kaggle - Language Translation (English–French)**  
Contains around **175,000** sentence pairs with English and French equivalents.  
After cleaning, filtering, and splitting:
- **Train:** 90% of the data  
- **Validation:** 10% of the data  

---

##  Training Process

The training loop was built from scratch using **PyTorch** and supports mixed-precision (FP16) training on GPU.  
For each epoch:
- The model encodes the English sentence.  
- The decoder generates the corresponding French sentence.  
- The cross-attention module fuses the two representations.  
- The loss is computed and backpropagated to update weights.

---

##  Results

The trained model produces coherent and accurate translations for simple sentences:

| English | French |
|----------|---------|
| I love you | Je vous aime. |
| He is strong | Il est fort. |
| I feel sick | Je me sens mal. |

These results show that the encoder–decoder structure and the custom cross-attention mechanism effectively learn translation mappings.

---

## Author

**Nawfal Benhamdane**  
Student at CentraleSupélec
 Contact: [nawfal.benhamdane@student-cs.fr]




