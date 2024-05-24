



# Power User Determination and VM Setup

## Power User Determination Steps

In this project, power users were identified through a detailed process involving feature engineering, model selection, and evaluation. The methodology used for identifying power users is outlined below:

### 1. Feature Engineering
- **Data Augmentation**: Additional features were created, such as the average number of products in a basket, to enrich the dataset and improve model performance.
- **Target Column**: Initially, power users were identified based on a z-score method. However, this method resulted in very few power users, making it insufficient. Therefore, based on the distributions, users who spent more than $110 were identified as power users, forming the basis for the classification target.

### 2. Model Training and Oversampling
- **Training Dataset Preparation**: The training dataset was adjusted using various oversampling methods to handle class imbalances.
- **Oversampling Techniques**: Methods like RandomOverSample, SMOTE, and ADASYN were employed to balance the dataset, ensuring that the models could effectively learn from both the majority and minority classes.

### 3. Model Selection
- **Hyperparameter Optimization**: GridSearchCV was used for hyperparameter tuning to find the best model configurations.
- **Comparison of Models**: Several models were compared based on their performance metrics, including KNN, XGBoost, Logistic Regression, and Random Forest. The XGBoost model with ADASYN oversampling showed the best performance.


| Model                                       | Recall  | Precision | Log Loss |
|---------------------------------------------|---------|-----------|----------|
| KNN                                         | 51.65%  | 88.70%    | 6.88%    |
| KNN_RandomOverSample                        | 47.25%  | 23.50%    | 15.45%   |
| KNN_SMOTE                                   | 62.64%  | 19.40%    | 19.13%   |
| KNN_ADASYN                                  | 28.57%  | 35.60%    | 24.31%   |
| XGBoost                                     | 71.43%  | 100.00%   | 5.23%    |
| XGBoost_RandomOverSample                    | 71.43%  | 55.60%    | 2.70%    |
| XGBoost_SMOTE                               | 71.43%  | 97.00%    | 1.41%    |
| **XGBoost_ADASYN**                          | 71.43%  | 100.00%   | 1.33%    |
| Logistic Regression                         | 67.03%  | 89.70%    | 1.21%    |
| Logistic Regression_RandomOverSample        | 78.02%  | 10.50%    | 14.46%   |
| Logistic Regression_SMOTE                   | 76.92%  | 11.60%    | 12.64%   |
| Logistic Regression_ADASYN                  | 84.62%  | 6.40%     | 24.08%   |
| RandomForest                                | 70.33%  | 100.00%   | 4.49%    |
| RandomForest_RandomOverSample               | 63.74%  | 87.90%    | 5.12%    |
| RandomForest_SMOTE                          | 72.53%  | 42.00%    | 3.16%    |
| RandomForest_ADASYN                         | 74.73%  | 32.70%    | 4.43%    |


### 4. Threshold Adjustment and Model Evaluation
- **Threshold Tuning**: The threshold value of the model was adjusted to optimize performance. Despite testing various thresholds, the default value of 0.5 was retained as it provided the best balance between recall and precision.
- **ROC AUC Curve Analysis**: The performance of the XGBoost ADASYN model was further validated using the ROC AUC curve, demonstrating strong predictive capabilities.

## 5. VM Setup and Docker Image Deployment

A virtual machine (VM) was created on GCP Compute Engine. After the VM creation, an SSH connection was established to this VM. Following the SSH steps, the interface was accessed through the IP address. The steps below detail this process:

### 1. VM Creation
Initially, an Ubuntu VM was created with the necessary configurations and settings.

### 2. SSH Connection
An SSH connection was established to the created VM using the command:
# Docker Image Setup
The Docker image previously uploaded to Docker Hub was pulled into this VM and run. The necessary SSH commands are as follows:

    sudo apt update
    sudo apt upgrade
    sudo apt install docker.io
    sudo docker login
    # Enter Docker Hub credentials
    # Login Succeeded
    sudo docker pull yaseminbellioglu/xgboost_adasyn_poweruser_image:v1
    sudo docker run -d -p 80:8000 yaseminbellioglu/xgboost_adasyn_poweruser_image:v1
    sudo docker images
    sudo docker ps
    sudo docker stop busy_cohen
    sudo docker rmi image_id


## 4. Accessing the API
As shown in the fastApi_VM.png file, the API can be accessed by connecting to the machine via the External IP Address.







