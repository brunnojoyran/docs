---
title: Node Requirements
weight: 1
---

K3s is very lightweight, but has some minimum requirements as outlined below.

Whether you're configuring a K3s cluster to run in a Docker or Kubernetes setup, each node running K3s should meet the following minimum requirements. You may need more resources to fit your needs.

## Prerequisites
*    Two nodes cannot have the same hostname. If all your nodes have the same hostname, pass `--node-name` or set `$K3S_NODE_NAME` with a unique name for each node you add to the cluster.

## Operating Systems

K3s should run on just about any flavor of Linux. However, K3s is tested on the following operating systems and their subsequent non-major releases.

*    Ubuntu 16.04 (amd64)
*    Ubuntu 18.04 (amd64)
*    Raspbian Buster (armhf)

> If you are using Alpine Linux, follow [these steps]({{<baseurl>}}/k3s/latest/en/advanced/#additional-preparation-for-alpine-linux-setup) for additional setup.

## Hardware

Hardware requirements scale based on the size of your deployments. Minimum recommendations are outlined here.

*    RAM: 512MB Minimum
*    CPU: 1 Minimum

#### Disks

K3s performance depends on the performance of the database. To ensure optimal speed, we recommend using an SSD when possible. Disk performance will vary on ARM devices utilizing an SD card or eMMC.

## Networking

The K3s server needs port 6443 to be accessible by the nodes. The nodes need to be able to reach other nodes over UDP port 8472 (Flannel VXLAN). If you do not use flannel and provide your own custom CNI, then port 8472 is not needed by K3s. The node should not listen on any other port. K3s uses reverse tunneling such that the nodes make outbound connections to the server and all kubelet traffic runs through that tunnel.

IMPORTANT: The VXLAN port on nodes should not be exposed to the world as it opens up your cluster network to be accessed by anyone. Run your nodes behind a firewall/security group that disabled access to port 8472.

If you wish to utilize the metrics server, you will need to open port 10250 on each node.
