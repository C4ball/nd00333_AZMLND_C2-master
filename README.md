
# Project: Operationalizing Machine Learning	

## Overview	
This project is part of the Udacity Azure ML Nanodegree. The objective of this project is to configure a cloud-based machine learning production model, deploy it, and consume it and create automated process creating, publishing and consuming a pipeline.	

The dataset contain data about a direct marketing campaign of a financial institution, based on phone calls. The aim of the campaign was to increase the number of subscribers to the bank term deposit. In this project, we seek to predict a binary variable "y" ,i.e., whether a client will subscribe to the product -marked with "yes" - or not - marked with "no".	

Reference: https://archive.ics.uci.edu/ml/datasets/bank+marketing	

Dataset link: https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv

## Architectural Diagram	

The diagram below shows the steps followed in implementing the project:		

![Architectural-Diagram](./Screenshots/Architectural-Diagram.png)	

## Key Steps	

#### Step 1: Authentication
Step skipped, once I worked with Udacity lab and I'm not authorized to create a security principal. 

#### Step 2: Automated ML Experiment
Step to create a new experiment using Automated ML, the bank marketing registered dataset, created and configured a compute cluster, and used it to run the experiment. In the dataset, the column 'y' was selected as the target column.

###### Screenshot 1: Registerd Dataset
![](./Screenshots/Step_2/Registered_Datasets.png)

After selecting the registered bank marketing dataset, a Standard_DS12_v2 compute cluster type was created with 1 minimum number of nodes. 

##### Screenshot 2: Creating Automl Experiment 
![](./Screenshots/Step_2/Experiment_Condiguration.png)

##### Screenshot 3: Automl Experiment Completed 
![](./Screenshots/Step_2/Experiment_Models.png)

##### Screenshot 4: Best Model
The best model was using the XGBoostClassifier algorithm, with 0.91958 accuracy rate. 
![](./Screenshots/Step_2/Experiment_Best_Model.png)

#### Step 3: Deploy the Best Model
In this step, I deployed the best model while enabling authentication and Azure Container Instance (ACI). Later, the deployed model showed in the endpoints section.

##### Screenshot 5: Deploy Best Model 
![](./Screenshots/Step_3/Experiment_Completed.png)

##### Screenshot 6: Deployed Model Endpoint
![](./Screenshots/Step_3/Experiment_Best_Model.png)

#### Step 4: Enable Application Insights
From the deployed best model, I have enabled application insights and retrieve logs. This step will help in detecting failures, anomalies...etc in the model. The executed code in logs.py enables Application Insights. Application Insights were disabled before running logs.py script.

##### Screenshot 7: Application Insights Enabble
![](./Screenshots/Step_4/Application_Insights_enabled.png)

##### Screenshot 8: Enable Logs by running logs.py script
![](./Screenshots/Step_4/Logs_result.png)


#### Step 5: Swagger Documentation
A swagger is a tool used to document and consume RESTful web services with APIs in GET & POST HTTP requests. To enable swagger I have run serve.py script in port 8000 and swagger.sh in port 9000. Then, interact with the swagger instance and retrieve its response from localhost. 

##### Screenshot 9, 10, 11: API Interaction 
Best model documentation showed by swagger 

![](./Screenshots/Step_5/swagger-1.png)
![](./Screenshots/Step_5/swagger-2.png)
![](./Screenshots/Step_5/swagger-3.png)


#### Step 6: Consume Model Endpoints
In this step, throgh the endpoint.py script, the REST endpoint was used updating the score_url & Key. After running the code, it produced a JSON output response. Also, to load & test my model, the benchmark bash script was executed. 

##### Screenshot 12: Consume Endpoint 
![](./Screenshots/Step_6/endpoint-run.png)

##### Screenshot 13, 14: Benchmark 
![](./Screenshots/Step_6/benchmark-result-1.png)
![](./Screenshots/Step_6/benchmark-result-2.png)

#### Step 7: Create, Publish and Consume a Pipeline
I have updated the Jupyter Notebook with the dataset, cluster, keys, and model names and created the pipline.Then, published the pipeline using python SDK.

##### Screenshot 15: Creating Pipeline 
![](./Screenshots/Step_7/1-Pipeline_Created.png)

##### Screenshot 16: Pipeline Endpoint
![](./Screenshots/Step_7/2-Pipeline_Endpoint.png)

##### Screenshot 17: Bankmarketing dataset with AutoML module 
![](./Screenshots/Step_7/3-BankMarketing_Dataset_with_AutoML_Module.png)

##### Screenshot 18: Published Pipeline 
![](./Screenshots/Step_7/4-Published_pipeline_overview.png)

##### Screenshot 19: RunDetails Widget of the Pipeline
![](./Screenshots/Step_7/5-RunDetails_Widget.png)

##### Screenshot 20: Scheduled Pipelines 
![](./Screenshots/Step_7/6-Scheduled_Run.png)


## Screen Recording
[Click Here](https://youtu.be/WW3NyYr3w9A)

## Future work
We will need to tackle the issue outlined below by introducing techniques for handling imbalanced data. This will reduce the bias towards one class and, therefore, produce a more reliable model capable of recognising both classes. Alternatively, we can use a metric that is more suitable for working with imbalanced data, for example, AUC_weighted , to get more reliable predictions.
* Font 1: https://aka.ms/AutomatedMLImbalancedData
* Font 2: https://docs.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls

I would recommend to separate the data in 3 sets (Test, Training and Validation), in order the be sure the models are not overfitted
