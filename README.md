# Openshift 4: Windows Containers

## Table of Contents
```
Pre-requisites
Demo #1 - To scale machines for OCP cluster 
Demo #2 - To build simple Windows Web Server on OCP
Resources for OCP and Windows Containers
```

## Pre-requisites
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

### To access the Windows node: 
Locate the Windows node: 
```
$ oc get nodes -o wide 
```

SSH into the Windows Machine Config Operator to access the Windows node: 
```
$ oc get pods -n openshift-windows-machine-config-operator
$ oc rsh -n openshift-windows-machine-config-operator winc-ssh-XXXXX
sh-4.4$
```

Using sshcmd.sh to login to the Windows node: 
```
$ sshcmd.sh <name-of-windows-node>
PS C:\Users\Administrator>
```

Install the Windows Server 2019 image via docker: 
```
> docker images
> docker pull mcr.microsoft.com/windows/servercore:ltsc2019
> docker images
> exit
> $ exit
```

### Build Windows Server 2019 container using OCP


## Resources for OCP and Windows Containers 
