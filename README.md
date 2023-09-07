[![<ORG_NAME>](https://circleci.com/gh/bugedone/project-ml-microservice-kubernetes.svg?style=svg)](https://app.circleci.com/pipelines/github/bugedone/project-ml-microservice-kubernetes)


## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

---
## Project Files Overview
`.circleci` CircleCI directory for the configuration files
  `config.yml` YAML configuration file with parameters and workflows for building/testing
`model_data` Contains the model data for the Flask app
`docker_out.txt` Log statements from running in Docker
`kubernetes_out.txt` Log statements from running in Kubernetes
`Dockerfile` Docker template
`Makefile` Project makefile
`README.md` Summary of the project and execution
`app.py` Flask app main source file
`make_predictions.sh` Sends input data to the flask app
`requirements.txt` Python app required dependencies and package versions
`run_docker.sh` Builds a Docker image and runs the container
`run_kubernetes.sh` Downloads Docker image, deploys the pod, and forwards the port
`upload_docker.sh` Publishes the built Docker image to DockerHub

---
## Setup the Environment

### Python virtual environment
* Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv. 
```bash
python3 -m pip install --user virtualenv
# You should have Python 3.7 available in your host. 
# Check the Python path using `which python3`
# Use a command similar to this one:
python3 -m virtualenv --python=<path-to-Python3.7> .devops
source .devops/bin/activate
```
* Run `make install` to install the necessary dependencies
* Run `make lint` to lint your source code

### Deploying and running in Docker
* Build docker image + run container (application) locally `./run_docker.sh``
* Run predictions: from another terminal call `./make_prediction.sh`
* `CTRL+C` to terminate the Flask app running in a docker container

### Deploying and running in Kubernetes
* Build the docker image as above (`run_docker.sh`)
* Publish the docker image using `./upload_docker.sh`
* Start a local cluster with `minikube start`
* Verify cluster configurations `kubectl config view` - look for an entry with `certificate authority` and `server` populated
* Run the image in Kubernetes `./run_kubernetes.sh`. This may not be able to forward the port initially which the pod is started. If so wait a few minutes and try again
* Run predictions: from another terminal call `./make_prediction.sh`
* `CTRL+C` to terminate the port forwarding
* To pause the Kubernetes cluster use `minikube stop`
* To terminate the pod and Kubernetes cluster use `minikube delete`
