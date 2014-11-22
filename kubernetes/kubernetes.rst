**********
Kubernetes
**********


Kubernetes in Core OS
=====================
* https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-kubernetes-on-top-of-a-coreos-cluster


Alternative to Mesos

Design
======
* https://github.com/GoogleCloudPlatform/kubernetes/blob/master/DESIGN.md


Pod
===
Group of docker containers

* https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/pods.md


Networking
==========
https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/design/networking.md

The goal is for each pod to have an IP in a flat shared networking namespace that has full communication with other physical computers and containers across the network. IP-per-pod creates a clean, backward-compatible model where pods can be treated much like VMs or physical hosts from the perspectives of port allocation, networking, naming, service discovery, load balancing, application configuration, and migration.