# 🚀 Auto Ada Code Generation using Generative AI for NGC Systems

This project demonstrates the use of a fine-tuned Generative AI model to automatically generate **Ada code** from structured inputs describing computational tasks, specifically for **Root Sum Square (RSS)** vector operations in **Navigation, Guidance, and Control (NGC)** systems used in launch vehicles.

---

## 📌 Project Overview

In safety-critical domains like aerospace and embedded systems, writing reliable and syntactically correct Ada code can be time-consuming. This project leverages a **lightweight Large Language Model (LLM)** — **TinyLlama-1.1B-Chat** — fine-tuned using **LoRA (Low-Rank Adaptation)** and **4-bit quantization** to generate Ada procedures from structured pseudo-specifications.

---

##  Model Highlights

- **Base Model**: [TinyLlama-1.1B-Chat-v1.0](https://huggingface.co/TinyLlama/TinyLlama-1.1B-Chat-v1.0)
- **Fine-Tuning Technique**: PEFT (Parameter-Efficient Fine-Tuning) with LoRA
- **Task Type**: Causal Language Modeling
- **Precision**: bfloat16 with 4-bit NF4 quantization using BitsAndBytes
- **Dataset**: Synthetic dataset of RSS vector computation tasks (structured <input>, <output> format)

---

## 📂 Dataset Format

Each data point is structured as follows:

```<input> v = [a, b, c] rss_value = rss of vector v <output> -- Ada code computing RSS <|endoftext|> ```
