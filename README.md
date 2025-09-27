# intrusion-detection-ml
Intrusion detection system using ML on Kaggle dataset

# Overview of the Project
With this project, I built an intrusion detection system using ML. I trained the model using KNN and RandomForest, and compared the results. I've handled the class imbalances in the data and prevented data leakage.

# Overview of the Dataset
- **Rows**: ~8,846 synthetic network log records.  
- **Features used**:  
  - Numeric → `Port`, `Payload_Size`  
  - Categorical → `Request_Type`, `Protocol`, `Status`  
- **Target**: `Scan_Type` (Normal, BotAttack, PortScan)  
- **Dropped**:  
  - `Source_IP` and `Destination_IP`: These were dropped because they were not generalizable.
  - `User_Agent`: This was dropped because it was too specific.
  - `Intrusion`: This was dropped because it caused label leakage.
 
# Preprocessing of Data
Before training the models, I had to takeseveral preprocessing steps to ensure that all data and features were in a machine-readable format. First of all, the categories 'User_Agent', 'Source_IP', and 'Destination_IP' were removed, as these categories did not offer any distinguising features and would potentially mislead the model. 
Then, I transformed the categorial features 'Request_Type', 'Protocol' and 'Status' using one-hot encoding. This enabled for the creation of a new binary column, where the value is 1 if the category is present and 0 if not. Through this transformation, each type of data within each category had its own binary coding, which allowed for a smoother training for the model.
The numeric features, 'Port' and 'Payload_Size' were extracted into a seperate DataFrame, which were later combined with one-hot encoded categorial features, producing the final feature matrix X. This matrix had all features in numeric form, which meant it was ready to be used for training and testing ML models. 
Finally, the target variable, 'Scan_Type' was label-encoded, and each class had its own numeric form. This produced the final target vector Y, and the model used it for supervised learning. 

# Splitting the data
After the preprocessing, I split the dataset into training (80%) and testing (20%) using train_test_split function. This was an important step in order to ensure that the distribution of classes (Normal, PortScan and BotAttack) remained consistent across both training and testing sets. With this splitting, there were 7076 training samples, and 1770 testing samples, with each having 14 features consisting of 2 numeric features and 12 one-hot encoded categorical features.

# Training the data 
After splitting data into training and testing sets, I trained the models with two different ML Models: **K-Nearest Neigbours (KNN)** and **Random Forest**. The KNN model was chosen as a simple baseline that classifies each sample based on the majority label among its closest neighbors. With k=5, it achieved high overall accuracy (~99%) but struggled with detecting minority classes, as seen in its BotAttack recall score of 0.83. To address the imbalance, I also trained a Random Forest classifier with 300 trees and class weighting enabled. This model not only maintained ~99% accuracy but also improved recall for BotAttacks to 0.93, making it more reliable for intrusion detection. The Random Forest also provided better generalization compared to KNN, particularly for rare events.

# Evaluation
**K-Nearest Neighbors (KNN, k=5)**  
- Accuracy: ~99%  
- BotAttack recall: 0.83  
- Struggled with minority class detection.  

**Random Forest (300 trees, class_weight="balanced")**  
- Accuracy: ~99%  
- BotAttack recall: 0.93  
- Performed better on minority classes and provided more robust predictions.

## Key Insights
- Accuracy alone can be misleading in imbalanced datasets.  
- Removing the `Intrusion` column was critical to avoid data leakage.  
- Random Forest outperformed KNN by capturing more BotAttack cases.  
- Normal and PortScan traffic were easy to classify, while BotAttack was the hardest to detect.

## How to Run
When prompted in Colab, upload the dataset file `Network_logs.csv`.  
The notebook will then load the data and run preprocessing, training, and evaluation.
