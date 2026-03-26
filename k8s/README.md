# Quick Start Guide

This guide is designed to help you deploy the `linux-command` application in Kubernetes based on the `wcjiang/linux-command` image. This application provides a `Deployment` and exposes the service port through a `Service`.

## Prerequisites

- A functioning Kubernetes cluster.
- `kubectl` installed and configured to connect to your Kubernetes cluster.

## Installation Steps

We will use the `kubectl` YAML application file from this repository to install the `linux-command` application.

```bash
$ kubectl apply -f https://raw.githubusercontent.com/jaywcjlove/linux-command/refs/heads/master/k8s/linux-command.yaml
```

Check the `Deployment` status:

```bash
$ kubectl get deployments -n linux-command
NAME            READY   UP-TO-DATE   AVAILABLE   AGE
linux-command   1/1     1            1           17m
```

You can check the `Pod` status to ensure it is running correctly:

```bash
$ kubectl get pods -n linux-command
NAME                            READY   STATUS    RESTARTS   AGE
linux-command-fff454654-427zp   1/1     Running   0          12m
```

Verify that the `Service` was successfully created and retrieve the exposed port:

```bash
$ kubectl get services -n linux-command
NAME                    TYPE       CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
linux-command-service   NodePort   10.96.2.225   <none>        9665:30204/TCP   18m
```

## Accessing the Application

Access the application by retrieving the `NodePort`. Use the following command to get the `NodePort` service information:

```bash
$ kubectl get svc linux-command-service -n linux-command
```

Based on the output, access the service using `EXTERNAL-IP:PORT`. For example:

```
http://<Node-IP>:<NodePort>
```

## Uninstalling the Application

If you need to delete the deployed resources, you can do so with the following command:

```bash
kubectl delete -f linux-command.yaml
```

This will clean up all the Kubernetes resources created.
