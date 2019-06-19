# Project_V 
![](https://cdn.evbuc.com/images/30344048/190528843891/2/logo.png)

Zenika DataOps Platform

## Description
Zenika dataops platform is a toolkit to simplify and automate machine learning models development, training, evaluation and deployment.

The platform allows you to train different predictive models, compare them and choose the best one. It also compares the best models with the one already deployed in production and therefore deploys them in production when a better model has been found.  
The platform is based on docker images.

There is 4 main parts :

-   Data buffer : Permit to collect data from different sources and then process this data.
    
-   Processing : Permit to train,evaluate,compare, and deploy multiple models at the same time
    
-   Supervision : Permit to monitor the health of the platform and performance of differents models.
    
-   Repository manager : Permit to collect, store and serve binaries such as models, data etc…

## Installation

 1. Fork github repositories : (**Link**)
 2. In Forge repo, fill .env file
 3. In Forge repo execute : ```docker-compose up```
 4. Edit github access in jenkins configuration

## Usage

Here is how to setup and add a model to the platform.

 ### 1.  Add your data sources to the prepare data module
 
Open prepare_data repository, and edit, ```prepare_data.py``` to add your data sources.

> For more informations about how to implement these scripts, read repository README
Push changes.

### 2. Add your model to the ml_model module
To add a model you need to create a new branch in ml_model repository from master.
You going to have a template to add your model. There is a Jenkinsfile (you don't need to modify it generally) and ```train.py``` script. 
By default ```train.py``` script execute jupyter notebook named ```model.ipynb```.
You just need to copy your notebook's model in this repo and push. 

> For more informations about how implement your notebook, read the
> repository README.

### 3. Choose your evaluation metric in the test and evaluation module

Go into test_and_evalutation module. 
There is two script : 

 - ```evaluate_model.py``` → Calculate metrics on trained model.
- ```compare_models.py``` → Compare each model to each other.

> For more informations about how to implement these scripts, read repository README


