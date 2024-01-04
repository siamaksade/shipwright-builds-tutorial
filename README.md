# Builds for OpenShift Tutorial


1. Install Build on OpenShift
1. Review Build Strategies
1. Run a Source-to-Image Build
1. Run a Dockerfile Build
1. Run a Buildpacks Build
1. Install Community Build Strategies
1. Run a ko Build


## Pre-requisites
* OpenShift 4.14
* OpenShift CLI (install guide)
* Shipwright CLI (install guide)


## Install Builds on OpenShift
TBD

## Review Build Strategies

A build strategy defines the series of steps to assemble an application and is closely coupled with a container image build tool such as Buildpacks, Buildah, Source-to-Build, etc. You can review the build strategies that are supported out-of-the-box on OpenShift using the `shp` CLI:

```
$ oc get clusterbuildstrategy
```

TODO: add the output of the cli command to the above
TODO: `shp buildstrategy list` is missing


In addition to the supported build strategies, you can use community build strategies that are available in the Shipwright community and of course create your own customized build strategies that are tuned to your specific requirements and build tools. Run the following command to install the Cloud-Native Buildpacks (Developer Preview) and community `ko` (Go applications) build strategies on the cluster:

```
$ oc create -f URL-TO-BUILDPACKS-STRATEGY

$ oc create -f https://raw.githubusercontent.com/shipwright-io/build/main/samples/v1beta1/buildstrategy/ko/buildstrategy_ko_cr.yaml
```

TODO: update the url to the dev preview buildpacks strategy

Review the available build strategies on the cluster again:

```
$ oc get clusterbuildstrategy
```


## Run a Source-to-Image Build