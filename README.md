## Setup teleport with custom config using helm and deploy to Kubernetes cluster

[teleport](https://goteleport.com/) 



### Backup old data if exist
check out [ this ](https://goteleport.com/docs/kubernetes-access/helm/guides/migration/) guide on how to migrate current teleport cluster to new one
We just need the backup steps


After the initial installation of helm and teleport helm chart. We go to the necessary part


### Get the teleport configuration file from existing cluster

The first thing you'll need to do is extract the Teleport config file from your existing Teleport cluster

Firstly, check that the `ConfigMap` is present:

`kubectl --namespace teleport get configmap/teleport -o yaml`
