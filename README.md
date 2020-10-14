# Operationalizing Machine Learning

## **Overview:** 

In this Project, we are a given dataset (Bank-marketing dataset) which is trained using Azure ML. The completed model is then deployed and the endpoint is consumed.

**The steps include:**

1. Loading the given dataset and importing to Azure ML studio

2. Running the Automated ML experiment with the dataset and finding the best performing model with maximum accuracy.

3. To select the Best Model from the top performing models in Auto ML and deploying them.

4. Enabling Application insights in order to check performance of the deployed model's endpoint.

5. Swagger.json file is used for POST requests in the local host. This is done to see if the model is reponsive with POST requests.

6. Consuming the model by running endpoint.py file which will take features from the swagger.json file. 

7. Enabling an automated ML pipeline. 


## Architectural Diagram:

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/architectural-design.PNG)

## Step 1: Authentication

This step was not needed as a Virtual Machine was used where the authentication was already done.

## Step 2: Automated ML Experiment
**Data**

The dataset used in this project can be found [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv).

After creating a new ML run in the ML Studio, the dataset is loaded from the local file system provided in the Virtual Machine.
This dataset is first registered in the Auto ML Studio, shown in the image below. 

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/registered-dataset.PNG)

After launching the ML studio, we can create new ML run from "Create New". We have to select a dataset by either loading from the directory or local system and also 
selecting a target column on which the experiment will be running on. Auto ML run also requires to input a Compute Cluster which can be created in the process. The Virtual Machine type, priority and size can be chosen and also the minimum and maximum number of nodes for the cluster. At last a task type (for e.g here it was Clasification) can be selected for the ML run. 

The ML experiment run in ML Studio is completed, as shown in the image below.
![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/auto-ml-completed.PNG)


After the experiment is completely run, few of the best performing models are listed with the highest accuracies. The top model is shown in the image below:

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/best-model.PNG)


## Step 3: Deploy the Best Model

The best model is selected from the Auto ML model. 

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/best-model.PNG)

The accuracy is close to 92% which shows that this model will be perfect for our dataset. The image below shows the 
details of the best chosen model.

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/step2-show-model.PNG)


## Step 4: Enable Application Insights

After deploying the model we need to enable the application insights. The configuration information in the form of config.json can 
be downloaded from the subscription of ML Studio. Then, keeping the config.json file in the same directory of the project, we can run the log.py file after adding
the system.update(enable_application_insights=TRUE). 


![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/enable-app-insights.PNG)


After **running logs.py:**

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/logs1.PNG)

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/log2.PNG)

This will **enable the application insights** of our model. 

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/application-insights-enabled.PNG)


## Step 5: Swagger Documentation

The swagger.json file is downloaded from the deployed model's details. This file is then kept inside the swagger file of the project directory with
swagger.sh and serve.py file. 

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/swagger-uri.PNG)

The swagger.sh is run to check if the POST requests are responsive. The serve.py is executed the POST request.

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/bank-deploy.PNG)


**Swagger runs on localhost showing the HTTP API methods and responses for the model**

**POST REQUEST**

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/http1.PNG)

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/http2.PNG)

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/http3.PNG)

**GET REQUEST**

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/getresp.PNG)

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/http4.PNG)

## Step 6: Consume Model Endpoints

The restAPI URI and the primary key can be obtained from the deployed model that is completed. 
The image below shows as follows:

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/model-get-restAPI.PNG)

In the endpoint.py file, the rest API and primary key should be copied from the model 
and replaced in the variables **'scoring_uri'** and **'key'**.

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/endpoint_s.PNG)

The endpoint.py is then executed in Powershell after the necessary inclusion of uri and key, against the API producing JSON output from the model. 
The image below shows the action:

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/endpoint_output.PNG)


## Step 7: Create, Publish and Consume a Pipeline

The automation of model experiments and deployment are shown in this section.

After loading the starter code and filling out the necessary model names, workspaces and clusters used, a new pipepline is created. The cluster and experiment
name has to match with our existing experiment which we have been working on.


### Create and publish a pipeline

In the Azure ML Studio, we will go to the Notebooks section and upload an auto-ml notebook from the Virtual Machine that is provided for us. 
In the starter codes all the important details such as experiment name, compute name , dataset name etc are entered. The workspace is initialized through the given code in the aml notebook. By entering the 
The codes with respect to pipeline creation and publish are then run and executed.  


The **pipeline created** successfully is shown in the Pipeline bar:

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/pipeline-created.PNG)

**Bankmarketing Dataset in the AutoML module:**

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/registered-dataset.PNG)

After loading the dataset in the Jupyter Notebook, we can see it running in the notebook:

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/bankdatawithmlmodule.PNG)

*The Pipeline Graph:** 

In the pipeline section of the module, we can click on the created Pipeline and see this graph. This pipeline is ready to be published, and that can be done directly from Azure ML or we can also do it from the SDK.

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/pipeline-graph.PNG)


**Rest Endpoint shown to be ACTIVE:**
In the Pipeline section of the ML module, we can find the created pipeline in the list. The status of the pipeline is "ACTIVE" indicating the creation to be successful. It is shown below:

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/rest-endpoint-active.PNG)


### Configure a pipeline with the Python SDK

**Pipeline Run-Widget:**

From the given codes in the starter_files from the local system in VM, 'pipeline-run' was created during the initialization of our pipeline creation in the previous steps. We then call the 'publish_pipeline' function which will help us to publish the desired pipeline. The 'publish_pipeline.endpoint' will help us acquire
the REST API connection. If it works well, the HTTP POST request will interact with the pipeline successfully.

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/run-details-widget.PNG)



### Use a REST endpoint to interact with a Pipeline

**Scheduled Pipeline Run:**

The pipeline is shown to be "Active" from the image below.
![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/scheduled_runs.PNG)

**Jupyter notebook showing the run details of a pipeline triggered using published pipeline endpoint **

The RunDetails widget is showing the step runs, we can monitor the model using this. 

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/published-pipeline.PNG)

**Published Model Endpoint:**

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/pipeline-endpoint.PNG)


**REST Endpoint Details**

The status shows 'Active' and a REST Endpoint. It shows the connection is successful.

![alt text](https://github.com/Heera773/Operationalizing_ML/blob/main/pipeline-bank.PNG)


## Key Improvements:

1. Given the accuracy being 92% for the best model, training for more time may not bring sufficient change. We could have bigger dataset that has more variations within the data and that could lead to a different algorithm with a better accuracy.

2. We could enable Deep Learning option in the auto-ML experiment. 


## Screencast of Project:

The screencast of the project in given [here.](https://youtu.be/Y6VtDNEmzOg)
