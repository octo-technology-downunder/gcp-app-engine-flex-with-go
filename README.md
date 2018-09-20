# Google Cloud - App Engine (Flex / Go) - Lab

## Overview

In this quick lab, we will play with gcloud App Engine.

At the end of the lab you will be able to:
- **deploy a simple Go application** on Google App Engine - Flexible environment (you don't have to understand Go)
- **split traffic** between 2 versions of you app
- do basic operations on your application: **see logs**, **ssh**, debug, view metrics, etc

This lab should take approximately 30 minutes.
You will need to use you own google cloud account.

## The Lab - step by step

### 0. Prerequisites

#### Create a project on GCP and activate billing

- Google to the [Google Cloud console](https://console.cloud.google.com)
- Click on Project List (in the header next to the Google Cloud Platform Logo), the "Create Project"
- Give it a "Name", select a billing account, then use the "Create" button

For more information about this prerequisite step please refer to the [official documentation](https://cloud.google.com/resource-manager/docs/creating-managing-projects#creating_a_project).

#### Install and configure Google Cloud SDK 

- Install the [Google Cloud SDK](https://cloud.google.com/sdk/docs/downloads-interactive) on your machine
- Configure you SDK with you gcloud account, select a project with the command line `$ gcloud init`


### 1. Prepare your application

#### Get the source code

- git clone this repository on you machine
- have a look to the helloworld.go file, it is a simple Go app doing an _Hello World_
- update the string `Hello mate, if you like this lab, please give me a star :)` by any other string, it could be `Hello World`

#### Make you local project ready for GCP

GCP is using a yaml configuration file to know how to deploy your application, let's create it.

Create an **app.yaml** file to describe you application, for that you can use the existing **app.yaml.template** as example.

Only 2 lines required are:
- `env: flex`, type of Google App Engine (GAE) project, GCP provided 2 type of environment: [Flexible or Standard](https://cloud.google.com/appengine/docs/the-appengine-environments).
- `runtime: go`, to tell GAE which runtime do you want to use.

I would also recommend to set the `service: YOUR_APP_NAME`, if not you application will be deployed in the default one (hope you are alone on your project if it is the case).

Please refer to the [official documentation](https://cloud.google.com/appengine/docs/flexible/python/configuring-your-app-with-app-yaml) to see all available options you could put in this file.


### 2. Deploy your application

#### Deploy you have using your terminal

To do so, just use this simple command line in you shell: `gcloud app deploy`.

It will ask you a few questions like in which region you do want to deploy the app. 
Then take a coffee, it could take up to 10 minutes for the app to be created.

#### Check the results in the google cloud online console

##### Notice the Docker image in the registry (Menu > Container Registry)

GCP App Engine Flexible environment is using Docker under the hood to deploy your application. You can see the built image in the registry.


##### Look at the build logs from the online console (Menu > Cloud Build > History)

The build process could fail for many reason: your app is broken, the app.yaml file is not valid...
To take a look to the logs of the build process, go the the GCP Cloud Build service.

##### Notice the created Service  with 1 version (Menu > App Engine > Service)

A service is a kind of application.
You should be able to see the created Service from the GCP console with the name you put in the app.yaml file.


From here, you can:
- see the number of version you service have (should be 1 at this stage)
- access application logs from the "Tool" menu

Then click on "Versions"

##### Notice the Version: status, traffic allocation, #instances  (Menu > App Engine > Version >> select your service)

This screen list all versions available for your service. Basically 1 version is created each time you deploy.
If you can't find your version, use the dropdown at the top to select the good service.

When you application is deployed, you should be able to see:
- Status -> Serving
- Taffic Allocation to 100%
- Instances 1 (or more according to your configuration)
- You can also take a look to the config file GCP linked to this version and look at the logs of your application.

This screen is important, this is where you can control traffic of your app: Stop a version, Start, Migrate or split traffic between several versions. 