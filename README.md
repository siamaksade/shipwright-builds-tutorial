# Builds for OpenShift Examples

### Pre-requiestives
* Install Builds for OpenShift from OperatorHub on OpenShift cluster
* Download `shp` CLI from [here](https://developers.redhat.com/content-gateway/rest/browse/pub/openshift-v4/clients/openshift-builds/latest/)

### Create project

```
oc new-project demo
```

### Source-to-Image Build

1. Create build

    ```
    shp build create sample-s2i-nodejs \
        --source-url="https://github.com/shipwright-io/sample-nodejs" \
        --source-context-dir="source-build" \
        --strategy-name="source-to-image" \
        --builder-image="image-registry.openshift-image-registry.svc:5000/openshift/nodejs:16-ubi8" \
        --output-image="image-registry.openshift-image-registry.svc:5000/demo/sample-nodejs" 
    ```

2. List builds

    ```
    shp build list
    ```


3. Start build

    ```
    shp build run sample-s2i-nodejs --follow 
    ```


### Buildah Build with Dockerfile


1. Create build

    ```
    shp build create sample-buildah-go \
        --strategy-name="buildah" \
        --source-url="https://github.com/shipwright-io/sample-go" \
        --source-context-dir="docker-build" \
        --output-image="image-registry.openshift-image-registry.svc:5000/demo/go-app" 
    ```

2. Start build

    ```
    shp build run sample-buildah-go --follow 
    ```

3. Check buildruns status

    ```
    shp buildrun list
    ```


### Buildpacks Build 

> Buildpacks build strategy is not installed on the cluster by default since it is Developer Preview

1. Install Buildpacks build strategy 

    ```
    oc apply -f https://raw.githubusercontent.com/redhat-developer/openshift-builds-catalog/main/clusterBuildStrategy/buildpacks/buildpacks.yaml
    ```

2. Create build

    ```
    oc apply -f https://raw.githubusercontent.com/siamaksade/shipwright-builds-tutorial/main/build/buildpacks-build.yaml
    ```

3. Start build

    ```
    shp build run sample-buildpacks-nodejs --follow
    ```