# ML-lab

## Machine Learning with Spark ML

[<img src="https://github.com/mhuchette/ML-lab/blob/master/images/IBM.Cloud.png" height="150"/>](http://datascience.ibm.com/) 
[<img src="https://github.com/mhuchette/ML-lab/blob/master/images/Spark_logo.png" height="100"/>](http://spark.apache.org/)
[<img src="https://github.com/mhuchette/ML-lab/blob/master/images/jupyter.png" height="150"/>](http://jupyter.org/) 

In this lab we will use Spark ML and Jupyter Notebook to create a model that is capable of classifying breast cancer tumors as benign or malignant. 

We will use a data set from the University of California, Irvine (UCI) Machine Learning Repository in order to train and test our breast cancer prediction model. The data set contains measurements of the area, permimeter, concavity, smoothness, and more of each tumor.

## Objectives:
Upon completing the lab, you will know how to:

1. Connect to cloud object storage and read data used for machine learning.
2. Identify labels and transform data.
3. Use PixieDust to visualize data
4. Conduct feature engineering for algorithm data.
5. Declare a machine learning model.
6. Setup the Pipeline for data transforms and training.
7. Train the data.
8. Show and evaluate machine learning results.
9. Automatically tune machine learning results.
10. Score data and load results into cloud object storage.

## Instructions:  

## Part 1: Create a Watson Studio project and set up the required services.

### Step 1.  Log into your [Watson Studio](http://datascience.ibm.com/) account, then select `View All Projects`.

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/Select%20View%20All%20Projects.png"/>

### Step 2.  Click on `New Project`. 
> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/Select%20New%20Project.png"/>

### Step 3. Enter the project name (eg. Watson Studio Labs), optionally a description, and then click on `Add` in the Storage section. Note if you have already provisioned cloud object storage (you shouldn't see an Add button) , then just click on the `Create` button, and skip to Step 8. 

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/New%20Project%20Panel%20-%20Add%20Storage.png"/>

### Step 4. Click on the Lite plan, and then click on `Create`. 

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/Create%20Object%20Storage.png"/>

### Step 5. Optionally change the storage name, and then click on `Confirm`

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/Confirm%20Creation.png"/>

### Step 6. Click on `Refresh`. 

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/Click%20Refresh.png"/>

### Step 7.  The cloud object storage should appear. Now click on `Create`. 

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/Click%20Project%20Create.png"/>

### Step 8. 

This will require the following services to be created and associated with your project. 
1. Object Storage
1. Watson Machine Learning
1. Apache Spark  

The Object Storage service instance should already exist, having been created when the Watson Studio Labs (or whatever you named it) project was created. Both the Watson Machine Learning service, and the Apache Spark service need to be created and then associated with the project.  

### Step 9.  Click on the project `Settings` tab.

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/choose%20settings.png"/>

### Step 10. Scroll down to `Associated Services`, then select `Add service` and select `Watson`.

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/SelectWatsonService.png"/>

### Step 11. Select the `Machine Learning` service 

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/SelectMachineLearningService.png"/>

### Step 12. Select `New`.

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/Select%20New%20Service.png"/>

### Step 13. Select the `Lite` plan. 

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/Select%20Lite%20ML.png"/>

### Step 13. Scroll down and click `Create`, then change the `Service name` to `Machine Learning` in the `Confirm Creation` panel and click `Confirm`.  

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/ConfirmMachineLearningCreation.png"/>

### Step 14. The Machine Learning service that you created should now appear in `Associated Services`. 

> <img src="https://github.com/mhuchette/ML-lab/blob/master/images/See%20ML%20in%20Associated%20Services.png"/>

### Step 15. Follow the same process as in steps 10-14, except this time add a Spark service. 

## Part 2:

### Step 1. Click on the [link](https://github.com/mhuchette/ML-lab/blob/master/cancer_data.csv) and then right click on `Raw` and then click the `Save link as...` and then click `Save` to download the `cancer_data.csv file` to your computer. Don't change the name of the file. 
<img src="https://github.com/mhuchette/ML-lab/blob/master/images/data.png"/>

### Step 2.  Log into your [Watson Studio](http://datascience.ibm.com/) account, then click Projects in the top menubar and select the project you created at the beginning of this lab.
<img src="https://github.com/mhuchette/ML-lab/blob/master/images/Select%20Project.png"/>

### Step 3.  Click the `Add to project > Data Asset` link in the top right of your project pane. 
<img src="https://github.com/mhuchette/ML-lab/blob/master/images/Add%20to%20Project%20Data%20Asset.png"/>

### Step 4.  Click on `browse`. 
<img src="https://github.com/mhuchette/ML-lab/blob/master/images/Click%20Browse.png"/>

### Step 5. Navigate to the folder on your computer where you downloaded the `cancer_data.csv` file. Click on the file, and then click on `Open`.

### Step 6. Click on the `Assets` tab (if you are not already on that panel) and you should see `cancer_data.csv` listed under the `Data Assets` category. 
<img src="https://github.com/mhuchette/ML-lab/blob/master/images/assets.png"/>

### Step 7.  Click the `Add to project > Notebook` link in the top right of your project pane.
<img src="https://github.com/mhuchette/ML-lab/blob/master/images/Add%20to%20Project.png"/>

### Step 8.  Click the `From URL` tab under `Create Notebook`. Give the notebook a name in the `Name` field, for example `Machine learning with SparkML` and optionally you can give it a description. In the Notebook URL field, use

`https://github.com/mhuchette/ML-lab/blob/master/Breast_Cancer_Predict.ipynb` 

In the `Select runtime` field, make sure to select the Spark service, and then click on `Create Notebook`

<img src="https://github.com/mhuchette/ML-lab/blob/master/images/new%20notebook.png"/>

### Step 9.  Follow the instructions in the notebook.

