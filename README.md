Table of contents
=================
  * [Intro](#intro)
  * [Autoscaling](#autoscaling)
  * [configmap](#configmap)
  * [deployment](#deployment)
  * [first-app](#first-app)
  * [ingress](#ingress)
  * [replication-controller](#replication-controller)
  * [resourcesquotas](#resourcesquotas)
  * [service-discovery](#service-discovery)
  * [volumes](#volumes)

Intro
=================

## Kubernetes course
This repository is based in Kubernetes course from: https://github.com/wardviaene/kubernetes-course

We will asumme that we are working in the k8s-course namespace.

kubectl create namespace k8s-course

Autoscaling
=================

## Autoscaling: Horizontal Pod Autoscaling
Example of enabling Horizontal Pod Autoscaling for the php-apache server.

kubectl -n k8s-course create -f hpa-example.yml

### Observe the auto-scaling:
- kubectl -n k8s-course get pods -w
- kubectl -n k8s-course get hpa
- kubectl -n k8s-course describe hpa hpa-example-autoscaler

### Increase the load
kubectl run -i --tty load-generator --image=busybox /bin/sh

while true; do wget -q -O- http://hpa-example.k8s-course.svc.cluster.local:31001; done

### Resources
https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/

https://kubernetes.io/docs/user-guide/horizontal-pod-autoscaling/image/Dockerfile