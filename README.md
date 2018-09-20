# Google Cloud - App Engine (Flex / Go) - Lab

## Overview

In this quick lab, we will play with gcloud App Engine:
- we will deploy a simple Go app (you don't have to understand Go)
- then deploy a new version and split traffic between the 2

This lab should take approximately 30 minutes.
You will need to use you own google cloud account.

## Overview

- Install SDK

Check for Account / Project
$ gcloud init
[ $ gcloud auth login ]

Git clone
Check the go script inside

Create app.yaml
env: flex

Deploy
$ gcloud app deploy
Do you want to continue: Y
Region: australia-southeast1
Do you want to continue: Y

- It could take up to 10 min!
Notice the Docker image in the registry (Menu > Container Registry)
Look at the build logs in the console (Menu > Cloud Build > History)
Notice the Service create with 1 version (Menu > App Engine > Service)
Notice the Version: status, traffic allocation, #instances  (Menu > App Engine > Version >> select your service)

