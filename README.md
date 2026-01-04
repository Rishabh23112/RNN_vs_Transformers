# ⚔️ LSTM vs. Transformer: The Speed vs. Memory Benchmark

> **"We didn't switch to Transformers because they are efficient. We switched because LSTMs are forgetful."**

## 🚀 Overview
This project benchmarks **Long Short-Term Memory (LSTM)** networks against **Transformers** from scratch using PyTorch. 

The goal was to empirically verify the engineering trade-offs between the two architectures:
1.  **Inference Speed:** Which architecture is computationally lighter?
2.  **Memory Retention:** Which architecture handles long-range dependencies better?

The results challenge the common misconception that Transformers are "universally faster" and highlight the true reason for their dominance: **Context.**

## 📊 Key Findings

### 1. The Speed Surprise 🏎️
**Winner:** LSTM (Linear Complexity $O(N)$)

Contrary to popular belief, **LSTMs are faster** for inference on sequential data.
* **LSTM:** Processes tokens sequentially with very low overhead.
* **Transformer:** Processes tokens with Quadratic Complexity $O(N^2)$. The Self-Attention mechanism computes a massive matrix for every step, creating significant computational overhead.

### 2. The Memory Test 🧠
**Winner:** Transformer (Direct Attention)

I tasked both models to remember the first token of a long sequence.
* **LSTM:** Failed. The **Vanishing Gradient problem** caused the signal to degrade over time, leading to high loss.
* **Transformer:** Succeeded instantly. **Self-Attention** provides "Direct Access" to any point in the sequence history, regardless of distance.

---

## 📈 Benchmark Results

### Experiment 1: Inference Speed (Time vs. Sequence Length)
<img width="433" height="355" alt="time" src="https://github.com/user-attachments/assets/8baf01e4-3112-4e27-9e07-3b451f940d0e" />

*Observation: The LSTM (Red) maintains a linear time profile, while the Transformer (Blue) sees computational costs explode as sequences lengthen.*

### Experiment 2: Long-Term Memory (Loss vs. Training Steps)
<img width="433" height="357" alt="memory" src="https://github.com/user-attachments/assets/075738ce-28d9-4b39-9862-d8687434e491" />

*Observation: The Transformer's loss drops to zero almost immediately. The LSTM struggles to learn long-range dependencies.*

---

This uses standard full self-attention, not optimized variants like Flash or linear attention.

## 🛠️ Reproducing the Results

You can run this benchmark on your local machine or Google Colab/Kaggle.

### 1. Clone the Repository
```bash
git clone https://github.com/Rishabh23112/RNN_vs_Transformers.git
cd RNN_vs_Transformers
