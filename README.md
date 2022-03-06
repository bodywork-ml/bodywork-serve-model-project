# Serve ML Models on Kubernetes with Bodywork

![bodywork](https://bodywork-media.s3.eu-west-2.amazonaws.com/serve_model_qs.png)

This repository demonstrates how to deploy a ML prediction service service on Kubernetes, using Bodywork. For information on this demo, take a look [here](https://bodywork.readthedocs.io/en/latest/quickstart_serve_model/). To run this project, follow the steps below. If you are new to Kubernetes, then take a look at our [Kubernetes Quickstart Guide](https://bodywork.readthedocs.io/en/latest/kubernetes/#quickstart).

## Install Bodywork

Bodywork is distributed as a Python package that can be installed using Pip,

```shell
$ pip install bodywork
```

## Deploy the Service

To deploy the service defined in this repository run,

```shell
$ bodywork create deployment https://github.com/bodywork-ml/bodywork-serve-model-project
```

Logs will be streamed to your terminal until the job has been successfully completed.

## Make this Project Your Own

This repository is a [GitHub template repository](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template) that can be automatically copied into your own GitHub account by clicking the `Use this template` button above.

After you've cloned the template project, use official [Bodywork documentation](https://bodywork.readthedocs.io/en/latest/) to help modify the project to meet your own requirements.
