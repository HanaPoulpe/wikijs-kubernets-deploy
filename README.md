# Startup deployment for [Wiki.JS](https://js.wiki/) using kubernetes

## Setup
The manifests to find in the manifest directory need you to update a few parameters:
* namespace: I'm using a namespace named wiki for this example, you'll need to create the workspace,
or update the data in all documents
* secrets.yaml: Here you have the base structure for the secret, but you'll need to setup the correct values
  * The secret string must be base64 encoded. You can find an encoder right here: https://www.base64encode.org/
  * To know what are the values you can use for DB_TYPE, check [wiki.js wiki](https://docs.requarks.io/install/docker)

To install your wiki.js on kubernetes you'll have to run:
```
kubectl apply -f secret.yaml
kubectl apply -f deploy.yaml
kubectl apply -f service.yaml
```

Once done you'll be able to connect to your wiki.js instance by connecting to any of your nodes 
on port 11080.

## SSL
To enable SSL: you only have to uncomment the SSL related parts in deploy.yaml and service.yaml.

Super important: To get let's encrypt to work you need to have you wiki accessible on port 80 from
your public IP, otherwise it won't work.

For more options: check [wiki.js wiki](https://docs.requarks.io/install/docker)

## High Availability
The deployment file will run with HA set to enable.

You will still need to run only 1 instance the time to setup your wiki.js. Once it's setup and running
you can add more replicas.