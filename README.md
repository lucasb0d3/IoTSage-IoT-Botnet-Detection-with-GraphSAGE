# 🚀 IoTSage: IoT Botnet Detection with GraphSAGE

[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)  
[![PyTorch](https://img.shields.io/badge/PyTorch-2.6+-EE4C2C)](https://pytorch.org/)  
[![Torch Geometric](https://img.shields.io/badge/PyG-GraphSAGE-orange)](https://pytorch-geometric.readthedocs.io/)  
[![scikit-learn](https://img.shields.io/badge/Scikit--Learn-ML-yellow)](https://scikit-learn.org/stable/)  
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)  

---

## 📊 Overview  

This project implements **IoT Botnet Detection** (Mirai attacks) using **GraphSAGE**, a Graph Neural Network (GNN) architecture.

Instead of treating IoT traffic as raw tabular data, we **represent device activity as a graph** where:
- Each node = snapshot of device activity
- Edges = temporal relationships (successive time windows)

The **GraphSAGE model** learns powerful embeddings from this graph and classifies malicious vs benign activity.

---

## 📂 Dataset  

The model uses IoT network traffic data:

- 🟢 **Benign** → Normal IoT device traffic
- 🔴 **Mirai** → Botnet attack traffic

Preprocessing steps:
- Handle missing values / NaNs / infinities
- Drop irrelevant columns (timestamps separated out)
- Scale features with `StandardScaler`

---

## ⚙️ Setup  

<details>
<summary>📥 Installation Steps (click to expand)</summary>

```bash
git clone https://github.com/meanderinghuman/IoTSage
cd BotNet-Insight
pip install -r requirements.txt
```

Or manually install:  

```bash
pip install torch torch-geometric scikit-learn pandas numpy matplotlib gradio
```

⚠️ Ensure `torch-geometric`, `torch-scatter`, and `torch-sparse` versions match your PyTorch version.  

</details>

---

## 🏗️ Code Structure  

- **📂 Data Loading & Preprocessing**  
  - Loads benign & Mirai CSVs  
  - Cleans, scales, and labels data  

- **🔗 Graph Construction**  
  - Nodes = activity snapshots  
  - Edges = temporal adjacency  
  - Creates `torch_geometric.data.Data` object  

- **🧠 GraphSAGE Model**  
  - 2 × `SAGEConv` layers  
  - BatchNorm + ReLU + Dropout  
  - Final linear classifier  

- **🎯 Training & Evaluation**  
  - Train/val/test split  
  - Weighted cross-entropy for imbalance  
  - Early stopping on validation accuracy  
  - Metrics: Accuracy, Precision, Recall, F1, ROC-AUC  

- **📈 Visualization**  
  - Training curves  
  - Confusion matrix  
  - ROC curve  
  - Streamlit dashboard  

---

## 🧠 Model Architecture  

Below is the pipeline flow (inline SVG):  

<?xml version="1.0" encoding="utf-8" ?>
<svg baseProfile="full" height="300px" version="1.1" width="900px" xmlns="http://www.w3.org/2000/svg" xmlns:ev="http://www.w3.org/2001/xml-events" xmlns:xlink="http://www.w3.org/1999/xlink"><defs /><rect fill="white" height="100%" width="100%" x="0" y="0" /><rect fill="#4CAF50" height="80" rx="15" ry="15" stroke="black" stroke-width="2" width="160" x="20" y="110" /><text fill="white" font-size="14px" font-weight="bold" text-anchor="middle" x="100" y="140">Data</text><text fill="white" font-size="14px" font-weight="bold" text-anchor="middle" x="100" y="160">(Benign &amp; Mirai CSVs)</text><rect fill="#2196F3" height="80" rx="15" ry="15" stroke="black" stroke-width="2" width="160" x="220" y="110" /><text fill="white" font-size="14px" font-weight="bold" text-anchor="middle" x="300" y="140">Graph</text><text fill="white" font-size="14px" font-weight="bold" text-anchor="middle" x="300" y="160">Construction</text><rect fill="#9C27B0" height="80" rx="15" ry="15" stroke="black" stroke-width="2" width="160" x="420" y="110" /><text fill="white" font-size="14px" font-weight="bold" text-anchor="middle" x="500" y="140">GraphSAGE</text><text fill="white" font-size="14px" font-weight="bold" text-anchor="middle" x="500" y="160">Model</text><rect fill="#FF9800" height="80" rx="15" ry="15" stroke="black" stroke-width="2" width="160" x="620" y="110" /><text fill="white" font-size="14px" font-weight="bold" text-anchor="middle" x="700" y="140">Classifier</text><text fill="white" font-size="14px" font-weight="bold" text-anchor="middle" x="700" y="160">&amp; Evaluation</text><line stroke="black" stroke-width="2" x1="180" x2="220" y1="150" y2="150" /><polygon fill="black" points="220,150 212,146.0 212,154.0" /><line stroke="black" stroke-width="2" x1="380" x2="420" y1="150" y2="150" /><polygon fill="black" points="420,150 412,146.0 412,154.0" /><line stroke="black" stroke-width="2" x1="580" x2="620" y1="150" y2="150" /><polygon fill="black" points="620,150 612,146.0 612,154.0" /></svg>

---

## 🚀 Usage  

1. Place your datasets:  
   ```
   /content/drive/My Drive/IOT/benign/
   /content/drive/My Drive/IOT/mirai/
   ```  
   (or update `benign_dir` and `mirai_dir` in the script).  

2. Run the script:  

```bash
python iot_final.py
```

3. Start the dashboard:  

```bash
streamlit run web_app.py
```

---

## 📈 Evaluation Results  

| Metric     | Value      |
|------------|------------|
| ✅ Accuracy   | **96.12%** |
| 🎯 Precision  | **96.11%** |
| 🔁 Recall     | **96.12%** |
| 📊 F1-Score   | **96.11%** |
| 📉 AUC-ROC    | **0.9935** |

---

## 🌟 Future Improvements  

- Explore richer graph construction (e.g., IP addresses, port numbers, flow features).  
- Try advanced GNNs (e.g., GAT, GCN with attention).  
- Tune hyperparameters systematically.  
- Use sliding windows / causal sampling for temporal dynamics.  
- Test on more IoT botnets beyond Mirai.  

---

## 📜 License  
MIT License – free to use and modify.  

---

✨ **Project maintained by [Siddharth Pal](https://github.com/meanderinghuman)**
