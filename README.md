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
Finally, the target variable, 'Scan_Type' was label-encoded, anf each class had its own numeric form. This produced the final target vector Y, and the model used it for supervised learning. 

# Splitting the data
After the preprocessing, I split the dataset into training (80%) and testing (20%) using train_test_split function. This was an important step in order to ensure that the distribution of classes (Normal, PortScan and BotAttack) remained consistent across both training and testing sets. With this splitting, there were 7076 training samples, and 1770 testing samples, with each having 14 features consisting of 2 numeric features and 12 one-hot encoded categorical features.

# Training the data 
