# Introduction to Anyscale Services

**⏱️ Time to complete**: 5 min

This tutorial shows you how to:

1. Deploy Anyscale Services
2. Query the service
3. View and monitor the service in Anyscale UI.

## When to use Anyscale Services
We recommend deploying [Ray Serve apps](https://docs.ray.io/en/latest/serve/index.html) as Anyscale Services when you move to production or if the following features are needed: 
- Zero down time upgrade / canary rollout
- High availability
- Programmatic submission API & CI/CD integration

**Note**: 
- In open source Ray, users deploy Ray apps with Ray Serve API. Anyscale Services leverage Ray Serve API to deploy Ray apps on standalone Ray Clusters and manage the lifecycle of them. It also provides the additional features listed above. No code change to your Ray script is needed when deploying your existing Ray apps as Anyscale Services.
- For development work that requires rapid iteration, it is better to use [Anyscale Workspaces](https://docs.anyscale.com/platform/workspaces/) or other development environments.

## Deploy an Anyscale Service

You can deploy services from any machines, using the Anyscale CLI or SDK. In this tutorial, we use Anyscale CLI as an example. 
### Step 1: install Anycale CLI and authenticate
```bash
# Install the lastet version of Anyscale CLI
$ pip install -U anyscale
# Authenticate
$ anyscale login
```

### Step 2: Deploy an Anyscale Service
This example includes a simple Ray app that sends greetings upon request. Run the following command to deploy it as an Anyscale Service

```bash
$ anyscale service deploy -f service.yaml -n {provide a name for your service}
```
This example includes two important files
- service.yaml: set the import path of your app and the configs of your service. Learn more about the [supported fields](https://docs.anyscale.com/reference/service-api#serviceconfig).
- main.py: the Ray script that defines your app

 It's also possible to set the import path and other configs directly without using YAML files. However, YAML files are recommended for better flexibility, maintainability, etc. For more details, check out the [Anyscale Service reference](https://docs.anyscale.com/reference/service-api).


### Step 3: Query the service

#### 3.1 What is needed in your query
- base URL: the base URL of the service you want to query
- bearer token: if query authentication is enabled, a unique token will be generated for one service to authenticate all requests
- route: the path or endpoint to query. It is mapped to some functionality defined in your Ray Serve app. By default, `/` is used.
- query parameters: query parameters specific to a route or path


#### 3.2 Query the endpoint
- Set the bearer token and base URL (do not include `/` at the end) below which should be printed in the output of the deployment command
- Hit the path defined in your Ray script  (`/hello` in this example) with proper parameters (`world` is used as an example. Try change it!)

```bash
curl -H "Authorization: Bearer {enter bearer token}" "{enter base URL}/hello?name=world"
```

##  View services in UI

The output from the deployment command should also print the URL to your service in Anyscale UI. You can view the service state, logs, metrics, and Ray Dashboard in UI.

<img src="assets/anyscale-service.png" height=400px>


##  Clean up the resources
Terminate the service by clicking the button in the top right corner of the UI or run the follow command:
```bash
$ anyscale service terminate -n {name of your service}
```

## Summary

This tutorial shows your how to:
1. Deploy Anyscale Services
2. Query the service
3. View and monitor the service in Anyscale UI.

Check out [Anyscale Services documentation](https://docs.anyscale.com/platform/services/) for more guides:
- upgrade a service
- configure the autoscaling of deployment replicas
- monitor and debug
- and more
