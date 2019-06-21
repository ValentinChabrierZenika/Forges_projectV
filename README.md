# Project_V 

Zenika DataOps Platform

## Description
Zenika dataops platform is a toolkit to simplify and automate machine learning models' development, training, evaluation and deployment.

The platform allows you to train different predictive models, compare them and choose the best one. It also compares the best models to the one already deployed in production and deploys them in production when a better model has been found.  
The platform is based on docker images.

There are 4 main parts :

-   Data buffer : Collects data from different sources and then processes this data.
    
-   Processing : Trains, evaluates, compares, and deploys multiple models at the same time
    
-   Supervision : Monitors the health of the platform and performance of different models.
    
-   Repository manager : Collects, stores and serves binaries such as models, data etc…

The platform embeds different services :

- Jenkins → http://localhost:8080
- Prometheus → http://localhost:9090
- Grafana → http://localhost:3000
- Artifactory → http://localhost:8081
- MongoDB → http://localhost:27017

## Installation

 1. Fork github repositories : (**Links**)
 2. In Forge repo, fill .env file
 3. In Forge repo execute : ```docker-compose up```
 4. Edit github access in jenkins configuration available at http://localhost:8080

## Usage

Here is how to setup and add a model to the platform.

 ### 1.  Add your data sources to the "prepare data" module
 
Open prepare_data repository, and edit, ```prepare_data.py``` to add your data sources.

> For more information on how to implement these scripts, read repository [README](https://github.com/ValentinChabrierZenika/prepare_data_projectV/blob/master/README.md)
Push changes.

### 2. Add your model to the "ml_model" module
To add a model you need to create a new branch in ml_model repository from master.
You're going to have a template to add your model. There is a Jenkinsfile (you usually don't need to modify it) and ```train.py``` script. 
By default ```train.py``` script executes the jupyter notebook named ```model.ipynb```.
You just need to copy your notebook's model in this repo and push it.
You can add as many models as you want.

> For more information on how to implement your notebook, read the
> repository [README](https://github.com/ValentinChabrierZenika/ml_model_projectV/blob/master/README.md).

### 3. Choose your evaluation metric in the "test and evaluation" module

Go into the test_and_evalutation module. 
There are two scripts : 

 - ```evaluate_model.py``` → Calculates metrics on trained model.
- ```compare_models.py``` → Compares each model to each other.

You'll need to modify them to choose the right evaluation metrics for you. 

> For more information on how to implement these scripts, read repository [README](https://github.com/ValentinChabrierZenika/test_and_evaluation/blob/master/README.md).

### 4. Compare your model with production model

Go into the production_deployment repository. 

By default, deployment of the production model is into artifactory repo named `ml_model_repo`

If you want to change comparison metric or deployment method, you need to modify the `compare_with_prod.py` script. 

> For more information on how to implement that script, read repository [README](https://github.com/ValentinChabrierZenika/production_deployment/blob/master/README.md)


### 5. (Optional) Search best Hyperparameters

The platform has a module to help the user search for hyperparameters values, for a choosen estimator.
You just have to create a branch from master with the same name as the corresponding model, and fill the `config.json` file.

> For more information on how to use the module, read repository [README](https://github.com/ValentinChabrierZenika/search_best_hyperparameters_projectV/blob/master/README.md).

### 6. Drink a coffee and watch the work do it all by itself

The platform will executes a complete workflow each hours and improve your model in production :)
