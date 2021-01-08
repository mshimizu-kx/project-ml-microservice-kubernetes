# Project of CloudDevOps Engineer Course4

![CircleCI](https://img.shields.io/circleci/build/github/mshimizu-kx/project-ml-microservice-kubernetes?label=circleci)


## Overview

The project is to deploy a pre-trained machine-learning web application with a container and kubernetes in automatic way. This deployment requires following tasks:

- Build a dedicated environment with specific python version.
- Check linting of python files and a Dockerfile.
- Build a docker image with installing dependencies.
- Check behavior of application by posting data.
- Deploy the container image with Kubernetes.
  
## Files

- `model_data/`: Containins data and pre-trained model for prediction.
- `output_txt_files/`: Contains output from docker and kubernetes when checking a behavior of the application.
- `app.py`: Web application script run on a container.
- `Dockerfile`: Template for building the container.
- `make_prediction.sh`: Script to post data to the application.
- `Makefile`: Script to set up environment and validating files.
- `requirements.txt`: List of python dependencies.
- `run_docker.sh`: Build and run the docker container.
- `run_kubernetes.sh`: Script to run the container with proper port-forwarding.
- `upload_docker.sh`: Script to upload the built container image to a registry.

## Quick Tour

The intructions below guide you from setup of the environmemt to running the ML application and get a prediction of housing price.

### 1. Setup the Environment

To avoid dependency collision of python packages, we will create a dedicated environment to run this appication.

1.  Create a virtualenv and activate it

        $ make setup

2. Install necessary dependencies

        $ make install

### 2. Running ML Web Application

There are three ways to launch the ML application:

1. Standalone
2. Run in Docker
3. Run in Kubernetes

#### 2.1 Launch Standaone Application

This option does not require anything. Just run python script:

```bash

$ python app.py

```

#### 2.2 Launch with Docker

**Requirement:**

- Docker

Ensure docker is running. If you are using CentOS, the command should be like this:

```bash

$ sudo systemctl start docker

```

You need to build a docker image containing the application and dependencies. However, you can omit everything by running the provided script!! 🍕🍕🍕

The script does:

- Build a docker image
- List images
- Run the container on the port 8000

```bash

$ ./run_docker.sh

```

#### 2.3 Launch with Kubernetes

**Requirements:**

- Minikube (or Kubernetes)
- Docker Hub account

In order to lauch a docker image with Kubernetes you need to upload the docker image to your registry. If you have not built an image you can build with the provided `run_docker.sh` (See [Launch with Docker](#22-launch-with-docker) section).

In order to upload the associated image to an online registry, use the provided script `upload_docker.sh` 🍟🍟🍟.

```bash

$ docker login
$ ./upload_docker.sh

```

Then start kuberenetes (We will use minikube here) and launch a pod with the image, again with the prepared script!! 🍔🍔🍔

```bash

$ minikube start
$ ./run_kubernetes.sh

```

### 3. Get Prediction

Now ML application is waiting for data on port 8000. You can post data there ... with the simple script!! 😂😂😂 (Be my guest!!)

```bash

$ ./make_prediction.sh

```

**Note:** The script may fail in the first run because deploying a pod takes a little of time. Wait until the status becomes `RUNNING` and run again. You can check status of pod by:
        
        $ kubectl get pod
        

Play around by changing data properties in the script!!
