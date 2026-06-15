# Knowledge-Distillation-GSM8k
Comparison of Model Performance with Knowledge Distillation and Quantization (PyTorch, Python) 

## What this project does
This project studies how to make math reasoning models more efficient on the GSM8K benchmark by combining:
- **Knowledge distillation** (transferring reasoning behavior from a stronger teacher model to a smaller student model)
- **Quantization** (reducing model precision to lower memory usage and improve inference efficiency)

The repository includes:
- **Experiment notebooks** under `Code/` for teacher/student setup, distillation workflows, model inference, and quantization experiments
- **GSM8K dataset files** under `Code/data/` (`train.jsonl` and `test.jsonl`) used for training and evaluation
- **Result comparison workflows** to evaluate student vs. teacher performance and understand accuracy-efficiency trade-offs

In short, the project demonstrates how much performance can be retained on GSM8K while reducing model size and computational cost through distillation and quantization techniques.
