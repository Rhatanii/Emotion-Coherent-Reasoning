# Emotion-Coherent Reasoning for Multimodal LLMs via Emotional Rationale Verifier

Our ERV project handles interpretable and consistent explanation about Multimodal Emotion Recognition.

🎉 Accepted to **AAAI 2026**! 
[[paper]](https://arxiv.org/pdf/2510.23506)

---
![image](figures/Figure1.png)


## 🚀 Environment Setup

Follow these steps to set up the environment required to run this project.

1.  **Base Repository Installation**
    First, follow the installation guide from the main [R1-V repository](https://github.com/StarsfieldAI/R1-V).

2.  **Install Flash Attention**
    ```bash
    pip install flash_attn==2.7.4.post1
    ```

3.  **Install Additional Python Libraries**
    ```bash
    pip install imageio decord moviepy==1.0.3 ipdb==0.13.13 h5py
    ```

---

## 📂 Model Checkpoints

| Model Name | Download Link (Hugging Face) |
| :--- | :--- |
| **Emotion_Verifier** | [https://huggingface.co/Rhatanii/Emo_Classifier](https://huggingface.co/Rhatanii/Emo_Classifier) |
| **ERV-0.5B** | [https://huggingface.co/Rhatanii/ERV-0.5B](https://huggingface.co/Rhatanii/ERV-0.5B) |
| **ERV-7B** | [https://huggingface.co/Rhatanii/ERV-7B](https://huggingface.co/Rhatanii/ERV-7B) |

---

## 💡 Training & Evaluation

### 🛠️ Training Code

The model training consists of two main stages.

1.  **SFT (Supervised Fine-Tuning) for Cold Start**
    * **Description:** The initial supervised learning phase to establish baseline model performance with formatted output.
    ```bash
    bash scripts/finetune_omni_add_reasoning.sh
    ```

2.  **GRPO Training with ERV**
    * **Description:** The RL phase using GRPO to optimize for emotion-coherent reasoning.
    ```bash
    bash src/r1-v/run_grpo_ERV.sh
    ```

### 📊 Evaluation Code

Scripts for evaluating reasoning coherence and core performance metrics.

1.  **Emotion Recognition Performance**
    * **Objective:** Measure the accuracy of the Emotion Recognition task.
    * **Execution:**
        ```bash
        python eval_score.py
        ```

2.  **Novel Metrics about Reasoning**
    * **Objective:** Measure the consistency and quality of the generated emotional rationales.

    * **A. Emotional Judgment via GPT API**
        * **Description:** Uses the GPT API to assess the emotional coherence of the generated reasoning.
        * **Execution:**
            ```bash
            bash tools/response_gpt_check.sh
            ```
        * **Note:** Requires GPT API key setup in the `tools/utils.py` directory.

    * **B. EEA / FCR / EPC Metric Check**
        * **Description:** Calculates key reasoning metrics: **E**xplanation **E**motion **A**ccuracy (EEA), **F**aithgul **C**onsistency **R**ate (FCR), and **E**xplanation-**P**rediction **C**onsistency (EPC).
        * **Execution:**
            ```bash
            cd tools/compare
            python compare_reason_recognition.py
            ```

---

## ⚡ Inference

Run inference to generate interpretable and consistent emotional reasoning.

```bash
bash eval_shard.sh
```
---

## 📚 Datasets

The datasets used in this project can be accessed from the following public sources.

| Dataset | Download Link |
| :------ | :------------ |
| **MAFW** | [https://mafw-database.github.io/MAFW/](https://mafw-database.github.io/MAFW/) |
| **DFEW** | [https://dfew-dataset.github.io/download.html](https://dfew-dataset.github.io/download.html) |
| **MERR** | [https://github.com/zebangcheng/emotion-llama](https://github.com/zebangcheng/emotion-llama) |
| **EMER** | [https://huggingface.co/datasets/MERChallenge/MER2024/tree/main](https://huggingface.co/datasets/MERChallenge/MER2024/tree/main) |

For the **EMER** dataset, please refer to `final-EMER-reason.csv` in the linked repository.

---

## Acknowledgement
This repository is built upon [R1-Omni](https://github.com/HumanMLLM/R1-Omni), [R1-V](https://github.com/StarsfieldAI/R1-V), and [HumanOmni](https://github.com/HumanMLLM/HumanOmni). 

We appreciate the open-source of the projects.
