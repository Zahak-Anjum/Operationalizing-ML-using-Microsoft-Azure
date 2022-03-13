# Operationalizing-ML-using-Microsoft-Azure

## Table of contents

   * [Overview](#Overview)
   * [Architectural Diagram](#Architectural-Diagram)
   * [Set up configurations](#Set-up-configurations)
   * [Deploy the best model using ACI](Deploy-the-best-model-using-ACI)
   * [Consume Model Endpoints and interact with deployed model using swagger UI](Consume-Model-Endpoints-and-interact-with-deployed-model-using-swagger-UI)
   * [Create and Publish a pipeline using Azure Python SDK using Jupyter Notebook](Create-and-Publish-a-pipeline-using-Azure-Python-SDK-using-Jupyter-Notebook)
   * [Screen Recording](#Screen-Recording)
   * [Comments and future improvements](#Comments-and-future-improvements)
   * [References](#References)

***

Note: All the files to reprodeuce the results are present in Execise_starter_files in folder nd00333_AZMLND_C2-master. Datset is present in dataset folder contains the dataset used for the experiments and screenshots are in screen-shot folder.

## Dataset
## Overview

This project is formed by two parts:

- The first part consists of creating a machine learning production model using AutoML in Azure Machine Learning Studio, and then deploy the best model and consume it with the help of Swagger UI using the REST API endpoint and the key produced for the deployed model. 
- The second part of the project is following the same steps but this time using Azure Python SDK to create, train, and publish a pipeline. For this part, I am using the Jupyter Notebook provided. The whole procedure is explained in this README file and the result is demonstrated in the screencast video.


## Architectural Diagram

![Architectural Diagram](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/Architectural%20diagram.PNG)


## Set up configurations

### Authentication

Install Azure ML extension to interact with Azure ML Studio, create Service Principal and associate it to specific workspace.

### Register Data on Azure Machine Learning Studio


In this project I use the dataset that can be obtained from [here](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/dataset/bankmarketing_train.csv) and contains marketing data about individuals. The data is related with direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict whether the client will subscribe a bank term deposit. I have uploaded dataset on Azure ML Studio. The screenshot is below. 

![dataset register](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/dataset%20bank%20marketing.PNG)

### Create an AutoML run

After registering the dataset the next step I did was making a compute cluster and run the the AutoML experiment. The experiment completed is shown below in the screenshot. 

![automl experiment completed](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/automl%20experiment%20completed.PNG)

### Get the best model

The best model was VotingEnsemble model with the accuracy of '0.92'. The screenshot is below.

![best automl](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/best%20model%20automl.PNG)

## Deploy the best model using ACI

The best model is deployed using webservices with ACI container. Also the key based autherntication is also enabled. We can access endpoints through which other service can interact with our deployed model.

### Enable logging and Application Insights

After deploying our best model, we can enable Application Insights and retrieve log. The logs.py was used to enable application insights.

![log file](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/application%20insights%20logs.py%20file.PNG)
![Application insight](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/application%20insights%20true%20azure%20ml%20studio.PNG)
![Both in one screenshot](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/application%20insights%20true.PNG)

## Consume Model Endpoints and interact with deployed model using swagger UI

### Consume deployed model using Swagger UI

Azure provides a swagger.json URL that can be used to create a web site that documents the HTTP endpoint for a deployed model. Here we consumed our deployed model using swagger and displayed the contents of the API for the model as shown below

![swagger](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/swagger%20ui%20best%20model.PNG)


### Interact with endpoints

Once the model is deployed, we use the python script endpoint.py provided to interact with the trained model and return an output predictions.

![endpoint interact](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/endpoint%20response.PNG)

## Create and Publish a pipeline using Azure Python SDK using Jupyter Notebook

In this second part of the project, I use the Jupyter Notebook provided: `aml-pipelines-with-automated-machine-learning-step.ipynb`. The notebook is updated as to have the same dataset, keys, URI, cluster, and model names that I created in the first part using AutoML. 

The purpose of this step is to create, publish and consume a pipeline using the Azure Python SDK. We can see below the relevant screenshots.

#### Pipeline Run

![](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/python%20sdk%20status.PNG)
![](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/python%20sdk%20azure%20ml%20studio%20run%20completed%20screenshot.PNG)

### Run Widget

![](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/python%20sdk%20status.PNG)

### Status Active
![](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/pipeline%20run%20active.PNG)

### Rest Endpoint

![](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/python%20sdk%20pipeline%20run%20submitted%20and%20getting%20post%20and%20get%20request.PNG)
![](https://github.com/Zahak-Anjum/Operationalizing-ML-using-Microsoft-Azure/blob/main/screen-shots/published%20pipeline%20run%20details%20widget.PNG)

## Screen Recording

The screen recording can be found [here](https://drive.google.com/file/d/1HlcTMLp2nT408nZED4DiLI5HjN6OMv4Y/view) and it shows the project in action. More specifically, the screencast demonstrates:

* The working deployed ML model endpoint
* The deployed Pipeline
* Available AutoML Model
* Successful API requests

## Comments and future improvements

- Test a local container with a downloaded model
- Use a parallel run step in the pipeline
- Using pipelines to automate the whole workflow from data preparation, to machine learning tasks and deployment
- Using the Apache Benchmark tool to set a measure of optimal performance

## References

- Udacity Nanodegree material
- [Imbalanced Data : How to handle Imbalanced Classification Problems](https://www.analyticsvidhya.com/blog/2017/03/imbalanced-data-classification/)
- [Consume an Azure Machine Learning model deployed as a web service](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-consume-web-service?tabs=python)
- [Deep learning vs. machine learning in Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-deep-learning-vs-machine-learning)
- [A Review of Azure Automated Machine Learning (AutoML)](https://medium.com/microsoftazure/a-review-of-azure-automated-machine-learning-automl-5d2f98512406)
- [Online screencast video](https://app.screencastify.com/)
