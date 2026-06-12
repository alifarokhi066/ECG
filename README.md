## 🚀 Quick Start & Execution Guide (How to Run the Project)

This project is designed to be fully reproducible. Anyone (from professors to open-source developers) can execute the entire pipeline in less than 5 minutes by following these steps:

### Step 1: Open the Project in Google Colab
You do not need to install anything on your local machine or download huge datasets. Everything runs on the cloud. 
* Click the badge below to open the complete notebook directly in Google Colab:
  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ali15121372/ECG/blob/main/Deep_thesis_Ali_Farokhi.ipynb)

### Step 2: Set Up the Environment
Once the notebook is open in Colab:
1. Go to the top menu and click on **Runtime** -> **Change runtime type**.
2. Select **GPU** (T4 or any available) from the Hardware Accelerator dropdown. *This is crucial for speeding up the Deep Learning (CNN/LSTM) training phases.*
3. Click **Save**.

### Step 3: Execute the Notebook
You can run the cells one by one to see the step-by-step transformations, or execute everything at once:
* Press `Ctrl + F9` or go to **Runtime** -> **Run all**.

---

## 🗺️ Notebook Structure & Code Roadmap

To make it easy to follow, the code is logically divided into sequential blocks. Here is what happens when you run the notebook:

### 📦 1. Dependency Installation & Environment Setup
* The notebook automatically installs required biomedical libraries and downloads the benchmark **PTB-XL** dataset ($100\text{Hz}$ and $500\text{Hz}$ signals) directly via Python scripts. 

### 🧹 2. Signal Processing Sandbox (The DSP Section)
* This is where the magic happens. The raw 12-lead ECG signals are fetched.
* The code applies the custom **Cascaded Median Filters** and **Butterworth Bandpass Filters**.
* **What to look for:** Look for the generated plots showing the *Before vs. After* filtering. You will clearly see how the wavy baseline and high-frequency noise disappear, leaving clean ECG waves ($P, QRS, T$).

### 🏷️ 3. Clinical Data Engineering
* The code reads the complex clinical target labels (`ptbxl_database.csv`) and aggregates them into the 5 clinical superclasses (`NORM`, `MI`, `STTC`, `CD`, `HYP`).
* It automatically handles train-test splitting based on the recommended clinical folds to prevent data leakage.

### 🧠 4. Deep Learning Model Training (CNN & LSTM)
* **1D-CNN Model:** Compiles and trains a convolutional architecture optimized for spatial feature learning.
* **LSTM Model:** Compiles and trains a recurrent architecture optimized for temporal/rhythm variations.
* *Note: The training epochs will display real-time loss and accuracy curves.*

### 📊 5. Evaluation & Performance Metrics
* Generates **Confusion Matrices** and **Classification Reports (Precision, Recall, F1-Score)**.
* Plots the final curves so you can visually compare which model performed better in diagnosing cardiac conditions.

---

##  Troubleshooting & Common FAQs

* **Q: I am getting a `NameError` or missing variable error in the evaluation cells.**
  * *A: Make sure you have executed all previous cells in order. The evaluation cells depend on variables generated during the model training phase.*
* **Q: The training is taking too long.**
  * *A: Check if your Colab Runtime is set to GPU. Training these deep architectures on a standard CPU will be extremely slow.*
* **Q: Where is the dataset stored?**
  * *A: The script downloads the dataset directly into the temporary Colab storage environment. It will be automatically deleted once you close the Colab session, keeping your local computer clean.*
