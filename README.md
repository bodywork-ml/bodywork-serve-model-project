![bodywork](https://bodywork-media.s3.eu-west-2.amazonaws.com/serve_model.png)

---

# Serve ML Models on Kubernetes using Bodywork

This repository contains a Bodywork project that demonstrates how to deploy a machine learning service on Kubernetes (k8s), with Bodywork. To run this project, follow the steps below.

## Get Access to a Kubernetes Cluster

In order to run this example project you will need access to a k8s cluster. To setup a single-node test cluster on your local machine you can use [minikube](https://minikube.sigs.k8s.io/docs/) or [docker-for-desktop](https://www.docker.com/products/docker-desktop). Check your access to k8s by running,

```shell
$ kubectl cluster-info
```

Which should return the details of your cluster.

## Install the Bodywork Python Package

```shell
$ pip install bodywork
```

## Setup a Kubernetes Namespace for use with Bodywork

```shell
$ bodywork setup-namespace scoring-service
```

## Deploy the Service

To test the service-deployment workflow, using a workflow-controller running on your local machine and interacting with your k8s cluster, run,

```shell
$ bodywork workflow \
    --namespace=scoring-service \
    https://github.com/bodywork-ml/bodywork-serve-model-project \
    master
```

The workflow-controller logs will be streamed to your shell's standard output until the service is successfully deployed.

## Testing the Service

Service deployments are accessible via HTTP from within the cluster - they are not exposed to the public internet. To test a service from your local machine you will first of all need to start a proxy server to enable access to your cluster. This can be achieved by issuing the following command,

```shell
$ kubectl proxy
```

Then in a new shell, you can use the curl tool to test the service. For example,

```shell
$ curl http://localhost:8001/api/v1/namespaces/scoring-service/services/bodywork-serve-model-project--scoring-service/proxy/iris/v1/score \
    --request POST \
    --header "Content-Type: application/json" \
    --data '{"sepal_length": 5.1, "sepal_width": 3.5, "petal_length": 1.4, "petal_width": 0.2}'
```

Should return,

```json
{
    "species_prediction":"setosa",
    "probabilities":"setosa=1.0|versicolor=0.0|virginica=0.0",
    "model_info": "DecisionTreeClassifier(class_weight='balanced', random_state=42)"
}
```

According to how the payload has been defined in the `scoring-service/serve.py` module.

## Cleaning Up

To clean-up the deployment in its entirety, delete the namespace using kubectl - e.g. by running,

```shell
$ kubectl delete ns scoring-service
```

## Make this Project Your Own

This repository is a [GitHub template repository](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template) that can be automatically copied into your own GitHub account by clicking the `Use this template` button above.

After you've cloned the template project, use official [Bodywork documentation](https://bodywork.readthedocs.io/en/latest/) to help modify the project to meet your own requirements.
