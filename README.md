# Dash on OpenShift

This repository contains basic bits to get started with running Dash applicatons on OpenShift

## Content

This repository uses s2i ([source-to-image](https://github.com/openshift/source-to-image)) to build a container image for OpenShift with basic useful dependencies preinstalled to start with [Dash](https://github.com/plotly/dash) applications.

Dependencies are added through `requirements.txt` file.

OpenShift artifacts needed for build and subsequent use of the image are defined in `images.yaml`

File `wsgi.py` simplifies the deployment of your applications as you do not have worry about how to configure ports or IP addresses to bind to - you simply need to privide a file `app.py` which contains variable `app` referencing `dash.Dash()` (as described in Dash's [tutorial](https://dash.plot.ly/getting-started)).

## How to run

To import OpenShift artifacts and run a build, call the following command:

```
oc apply -f images.yaml
```

Once the build is finished, you can deploy a Dash application. For example:

```
oc new-app s2i-dash-base~https://github.com/vpavlin/dash-example
```

To be able to access it, you need to expose the route

```
oc expose svc/dash-example
```
