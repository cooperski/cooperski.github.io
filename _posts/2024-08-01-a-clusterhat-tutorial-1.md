## A ClusterHAT Tutorial for 2024 (Part 1)

### Introduction

There are a number of existing tutorials online that demonstrate how to assemble and set up a cluster of Raspberry Pi single board computers, and just a few that focus on 8086 Consultancy's ClusterHAT hardware. This is a tutorial for creating a computer cluster using the ClusterHAT hardware for experimenting with Slurm and MPI in 2024.

This tutorial replicates the set up I currently have with my own cluster. Many other configurations are possible; this is just one of them. 

There are two parts to this tutorial: in part one, we assemble the cluster, install operating systems, configure each of the nodes, and install and test Slurm; in part two, we install and test MPICH for writing and executing parallelized software on the Pi cluster.

### Acknowledgements

I based my set up on Garrett Mills' tutorial [Building a Raspberry Pi Cluster](https://glmdev.medium.com/building-a-raspberry-pi-cluster-784f0df9afbd), Davin L's [Missing ClusterHat Tutorial](https://medium.com/@dhuck/the-missing-clusterhat-tutorial-45ad2241d738) tutorial, and ejolson's [
Super-cheap Computing Cluster for Learning](https://forums.raspberrypi.com/viewtopic.php?f=49&t=199994) thread on the Raspberry Pi forums.

### Hardware Requirements

My setup uses the following hardware:

-1 x ClusterHAT, available for purchase [here](https://clusterhat.com/buy)
-1 x Raspberry Pi 4 (2GB) to serve as the manager node (earlier Pi models may be used instead)
-4 x Raspberry Pi Zero 
-1 x 64GB micro SD card to serve as storage for all nodes in the cluster

### Basic Setup
#### Assembling the cluster

Assembly of the ClusterHAT and each of the Pi Zero nodes is straightforward: attach the ClusterHAT on top of the Pi 4's GPIO pins and connect the USB cable from one of the Pi 4's USB ports to the ClusterHAT, and finally, attach each of the Pi Zeros to the OTG ports using the Pi Zero's USB (not PWR IN) port. Each of the Pi Zero nodes will receive both power and data through the USB port. 

A full description of the assembly process is available [here](https://clusterhat.com/setup-assembly) from 8086 Consultancy.

#### Installing the operating system

Custom Raspberry Pi OS images for the ClusterHAT (both for controller and worker nodes) are available for download [here](https://clusterctrl.com/setup-software). Due to the limited amount of RAM in my Pi 4 as well as the Pi Zero nodes, I am electing to use the 32-bit images for this tutorial. For the Pi 4 controller, we will be using the CNAT Lite Bullseye[^1] image. This will share the controller's Ethernet or WiFi connection with each of the Pi Zero nodes.

The CNAT image may be written to the micro SD card using the Raspberry Pi Imager following the instructions [here](https://www.raspberrypi.com/documentation/computers/getting-started.html#using-raspberry-pi-imager). 

Within Raspberry Pi Imager, choose the custom Raspberry Pi OS images by first clicking the *CHOOSE OS* button on the main menu.

// image1

Scroll to the bottom of the list and select the *Use custom* option.

// image2

Navigate to where you have downloaded the custom Bullseye image and select it.

// image3 

Insert the micro SD card into your computer. From the main menu of Raspberry Pi Imager, select the target storage device by clicking the *CHOOSE STORAGE* button.

Finally, after you have selected the custom image and the target storage device, you can configure the usrename and passowrd for SSH along with the SSID of your home LAN if applicable. For this tutorial, I am using the default username *pi* with a custom password.
In a later step, from the controller Pi we will download and configure the custom Raspberry Pi OS image for each of the Pi Zero nodes.
 
#### First Boot on the Controller

Assuming you have configured your Pi to automatically connect to your home network, you can connect your Pi 4 to power, wait for it to boot, and SSH by entering the following command into your terminal:

`ssh pi@controller.local`

By default, the hostname of the controller image is configured to be *controller*.  

[^1]: As of this writing, custom Bookworm images are available here, but only for testing purposes
