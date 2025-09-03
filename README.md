# Intrusion Detection with Machine Learning
Intrusion detection system using ML (KNN & Random Forests) on Kaggle dataset. The project classifies network traffic as **Normal**, **BotAttack** or **PortScan**

# Overview
Intrusion detection systems are considered of huge significance in cybersecurity. Thus, it is critical to have systems that address logs that may potentially cause issues with the aim of mitigating harm. Therefore, this project uses two different machine learning algorithms to synthetic network logs to detect malicious traffic patterns. The reason for using the syntetic network logs is that the real network logs are not shared by companies publicly, as such data is considered private.

# 📊 Dataset
- Source: [Kaggle – Intrusion Detection Logs](https://www.kaggle.com/datasets/developerghost/intrusion-detection-logs-normal-bot-scan)  
- ~8,846 rows  
- Features: `Port`, `Payload_Size`, `Request_Type`, `Protocol`, `Status`  
- Target: `Scan_Type` (Normal, BotAttack, PortScan)  
- Dropped: `Source_IP`, `Destination_IP`, `User_Agent`, `Intrusion` (leakage risk)

## ⚙️ Preprocessing
- One-Hot Encoding: `Request_Type`, `Protocol`, `Status`
- Label Encoding: `Scan_Type`
- Train/test split: 80/20 (stratified)
- Scaling: applied to numeric features for KNN

## 🤖 Models
- **K-Nearest Neighbors (KNN, k=5)**
  - Accuracy: 99%
  - Weakness: BotAttack recall only 0.83
- **RandomForest (300 trees, class_weight="balanced")**
  - Accuracy: 99%
  - Strength: BotAttack recall improved to 0.93
We stratified the train/test split to preserve class proportions. However, class imbalance remained in the training data. KNN struggled with this imbalance, missing 17% of BotAttacks. RandomForest with class weighting reduced this issue, improving BotAttack recall to 93% while keeping overall accuracy at 99%.

## 📈 Results
RandomForest performed better on minority class detection.  

Confusion Matrix (RandomForest):  
![RandomForest Confusion Matrix](images/randomforest_cm.png)

## 🔑 Key Insights
- Accuracy alone is misleading in imbalanced datasets.
- Removing `Intrusion` was crucial to avoid label leakage.
- RandomForest is more reliable for BotAttack detection than KNN.

Open the notebook in Google Colab / Jupyter and run all cells.
