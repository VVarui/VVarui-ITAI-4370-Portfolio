# Lab 5: Edge Computing — Model Compression for IoT Deployment

**Notebook:** [`lab5-edge-model-optimization.ipynb`](../labs/lab5-edge-model-optimization.ipynb)

## Problem Statement
AI models trained in the cloud are often too large and slow for deployment on resource-constrained edge devices (IoT sensors, microcontrollers, edge gateways). This lab simulates classifying IoT sensor/device state and evaluates model compression techniques that make cloud-trained models viable for real-world edge deployment.

## Methods and Tools
- **Tools:** Python, TensorFlow/Keras, scikit-learn (`make_classification`, `train_test_split`, `accuracy_score`)
- **Data:** A synthetic IoT sensor dataset — 10,000 samples, 20 features, 3 device-state classes (8,000 train / 2,000 test).
- **Baseline model:** A fully-connected neural network ("cloud model"), 13,123 parameters, 51.26 KB.
- **Compression techniques compared:**
  1. **Pruning** — removing small/near-zero weights (target sparsity 50%).
  2. **Quantization (INT8)** — converting model weights from 32-bit float to 8-bit integers via TFLite conversion.
  3. **Knowledge distillation** — training a much smaller "student" model to mimic the baseline "teacher" model's outputs.
- **Evaluation:** Measured accuracy, average inference time (ms, over 100 runs), model size (KB), and parameter count for each variant.

## Results
| Model | Accuracy | Inference Time (ms) | Size (KB) | Parameters |
|---|---|---|---|---|
| Baseline (Cloud) | 93.75% | 92.35 | 51.26 | 13,123 |
| Pruned | 93.80% | 80.21 | 13.76 | 3,523 |
| Quantized (INT8) | 92.40% | — | — | — |
| Distilled | 91.45% | 90.16 | 4.89 | 1,251 |

## Deployment Recommendations
- **Microcontrollers (MCUs):** Quantized INT8 — minimal memory footprint (<50 KB), suited to sensor nodes and battery-powered wearables.
- **Edge gateways:** Pruned or distilled models — a balance of accuracy and efficiency, suited to industrial IoT and smart-city gateways.

## Interpretation
The most striking result was that **pruning slightly improved accuracy (93.75% → 93.80%) while cutting model size by roughly 73%** and reducing inference time by about 13%. This shows that a large model isn't automatically a more accurate one — many of the baseline's parameters were redundant, and removing them acted almost like a regularizer.

Distillation achieved the most extreme compression (10x fewer parameters than baseline) at the cost of about 2.3 percentage points of accuracy, which is an acceptable tradeoff for constrained devices where model size and power are the binding constraint rather than raw accuracy. This lab connected directly to the telecom/AI theme of the course: as networks push more intelligence to the edge (5G edge computing, smart sensors), understanding these accuracy-vs-efficiency tradeoffs is essential for real deployment decisions.
