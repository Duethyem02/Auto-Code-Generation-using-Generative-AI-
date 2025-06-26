
# 🚀 Auto Ada Code Generation using Generative AI for NGC Systems

This project demonstrates the use of a fine-tuned Generative AI model to automatically generate **Ada code** from structured inputs describing computational tasks, specifically for **Root Sum Square (RSS)** vector operations in **Navigation, Guidance, and Control (NGC)** systems used in launch vehicles.

---

## 📌 Project Overview

In safety-critical domains like aerospace and embedded systems, writing reliable and syntactically correct Ada code can be time-consuming. This project leverages a **lightweight Large Language Model (LLM)** — **TinyLlama-1.1B-Chat** — fine-tuned using **LoRA (Low-Rank Adaptation)** and **4-bit quantization** to generate Ada procedures from structured pseudo-specifications.

---

##  Model Highlights

-  **Base Model**: [TinyLlama-1.1B-Chat-v1.0](https://huggingface.co/TinyLlama/TinyLlama-1.1B-Chat-v1.0)
-  **Fine-Tuning Technique**: PEFT (Parameter-Efficient Fine-Tuning) with LoRA
-  **Task Type**: Causal Language Modeling
-  **Precision**: bfloat16 with 4-bit NF4 quantization using BitsAndBytes
-  **Dataset**: Synthetic dataset of RSS vector computation tasks (structured <input>, <output> format)

---

## 📂 Dataset Format

Each data point is structured as follows:
```
<input>
v = [a, b, c]
rss_value = rss of vector v
<output>
-- Ada code computing RSS
<|endoftext|>
```

---

## 🔧 Installation & Setup

Install dependencies:

```bash
pip install transformers peft accelerate datasets bitsandbytes
```

Login to Hugging Face:

```python
from huggingface_hub import notebook_login
notebook_login()
```

---

## 🏋️‍♂️ Training Summary

- Tokenized data using `AutoTokenizer` with truncation and padding
- Used `DataCollatorWithPadding` for dynamic batching
- Fine-tuned only LoRA layers using Hugging Face `Trainer` API
- Training done on resource-constrained hardware (NVIDIA T4)
- Training hyperparameters:  
  - `learning_rate=2e-5`, `batch_size=1`, `epochs=2`, `fp16=True`

---

## 🤖 Inference Example

```python
prompt = "v = [3.0, 4.0]\nrss_value = rss of vector v"
prompt_with_cue = prompt + "\nwith Ada.Text_IO;"
inputs = tokenizer(prompt_with_cue, return_tensors="pt").to(model.device)
outputs = model.generate(**inputs, max_new_tokens=300)
generated_code = tokenizer.decode(outputs[0], skip_special_tokens=True)
```

---

## 📈 Results

- Model generated correct and structured Ada code for varied vector inputs
- Average inference time: ~2.4 seconds per prompt on GPU
- Demonstrated strong generalization on unseen task descriptions

---

## 🚀 Future Scope

- Extend to more complex mathematical and control operations
- Add validation layer to check Ada code syntax and compilation
- Integrate voice or natural language input for real-world usage

---

## 📝 License

This project is for academic and research purposes only.

---
