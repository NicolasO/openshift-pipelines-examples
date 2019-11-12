# Tekton Pipeline Examples


## Pre-requisites
* [OpenShift 4 cluster](http://cloud.redhat.com)
* [Tekton CLI](https://github.com/tektoncd/cli/releases/latest)

## Prepare Project

```
oc new-project pipeline-demo
oc create -f tasks
oc create -f https://raw.githubusercontent.com/tektoncd/catalog/master/buildah/buildah.yaml
oc create -f https://raw.githubusercontent.com/tektoncd/catalog/master/openshift-client/openshift-client-task.yaml
oc create -f pipelines/mapit-resources.yml
```

## MapIt Build Pipeline

<img align="center" width="600" src="images/mapit-build-pipeline.png">

```
oc create -f pipelines/build-pipeline.yml
tkn pipeline start build-pipeline -s pipeline
```

## MapIt Deploy Pipeline

<img align="center" width="700" src="images/mapit-deploy-pipeline.png">

```
# deploy mapit
oc apply -f apps/mapit-spring.yml

# create pipeline
oc create -f pipelines/deploy-pipeline.yml
tkn pipeline start deploy-pipeline -s pipeline
```

# PetClinic Pipeline Demo

On Kubernetes
```
kubectl apply -k demos/petclinic/k8s
```

On OpenShift
```
oc apply -k demos/petclinic/os --validate=false
```

Start the pipeline
```
tkn pipeline start petclinic-s2i-pipeline -s pipeline -n pipelines-demo
```