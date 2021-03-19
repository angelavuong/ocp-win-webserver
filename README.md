# 3/18 Central Lunch and Learn: Windows Containers

## Pre-requisites:
In order to do this demo, we assume that:
```
1) Running OCP 4.6+
1) Appropriate networking has been configured for OCP to support Windows Containers (OVN Hybrid)
2) The Windows Machine Config Operator has already been installed via Operator Hub
```

## Demo #1 - To scale machines for OCP cluster
In this demo, we will increase the replica count of our Windows machineset from 1 to 2.

To view the list/describe the machinesets configured for Openshift: 
```
$ oc get machinesets -n openshift-machine-api
$ oc describe machineset -n openshift-machine-api <machine-set-name>
```

To view our list/details of machines built for Openshift: 
```
$ oc get machines -n openshift-machine-api
```

To increase/scale our Windows machineset to 2: 
```
$ oc scale machineset <machine-set-name> --replicas=2 -n openshift-machine-api
```

Validate 2 Windows nodes exist in our OCP cluster (could take up to 10 mins):
```
$ oc get machines -n openshift-machine-api
$ oc get nodes -o wide
```

## Demo #2 - To build simple Windows Web Server on OCP
In this demo, we will deploy a simple Windows Web Server on Openshift.

