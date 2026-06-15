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

## Repository guide (important files)

### Research artifacts
- **`HSMD_COLING.pdf`**  
  Main paper/report describing the method, experiment setup, and final results for combining quantization + distillation.
- **`Algoverse Research proposal draft_.docx`**  
  Proposal/background document with motivation and planned approach for efficiency-focused LLM experiments.

### Data
- **`Code/data/train.jsonl`**  
  GSM8K training split used to build prompts and distillation/evaluation workflows.
- **`Code/data/test.jsonl`**  
  GSM8K test split used for benchmark scoring and model comparison.

### Core experiment notebooks (`Code/`)
- **`hsmd_teacher_primary.ipynb`**  
  Primary teacher-model workflow for loading/evaluating the full model and generating teacher-side references.  
  **Use this as the default teacher notebook for new experiments.**
- **`hsmd_teacher_legacy.ipynb`**  
  Teacher workflow variant retained for comparison/reproducibility of prior runs.
- **`hsmd_student_lora.ipynb`**  
  Student distillation notebook variant with LoRA/fine-tuning workflow on GSM8K.
- **`hsmd_student_variant2.ipynb`**  
  Alternate student distillation notebook variant for iterative tuning/experimentation.
- **`meta_llama_3.ipynb`**  
  Quantized Llama experiment notebook with GSM8K-focused evaluation pipeline.
- **`meta_llama_3_instruct_experiment.ipynb`**  
  Instruction-style Llama experiment flow including quantization/inference setup.
- **`llama_3_1_8b_instruct_baseline.ipynb`**  
  Minimal baseline inference notebook for quick model checks.
- **`quanto_integration.ipynb`**  
  Tutorial-style notebook showing integration of `quanto` with `transformers` for lower-bit workflows.

## Key reported results (from `HSMD_COLING.pdf`)

The PDF reports a direct comparison between a **pretrained quantized student** and a **distilled quantized student** on GSM8K:

- **0-shot (first 100 GSM8K test questions):**
  - Baseline quantized model: **40%**
  - Distilled quantized model: **50%**
  - Improvement: **+10 percentage points**

- **8-shot prompting:**
  - Baseline quantized model: **76.6%**
  - Distilled quantized model: **76.9%**
  - Improvement: **+0.3 percentage points**

### Interpretation of results
- Distillation gives a **large gain in low-context (0-shot) settings**, where the quantized student needs stronger learned reasoning behavior.
- Under heavy prompting (8-shot), the gap narrows because prompting itself already boosts baseline performance.
- The distilled model still remains smaller/efficient due to quantization, while recovering part of the performance loss versus full-sized models.

### Reported limitations in the PDF
- Evaluation scope is limited to **GSM8K** and math reasoning.
- The study focuses on one main model family/setup, so broader cross-domain and cross-model validation is still needed.
