## The PiCluster Lives!

After many months of trial-and-error, I have finally gotten my Pi Cluster to function as I want it to! 

![The Pi Cluster in an earlier configuration.](/img/picluster.jpeg)

The Pi Cluster is a kind of tabletop scale model of a supercomputer cluster. In its present state, it is comprised of:
- 1 x Raspberry Pi 4B (2Gb RAM) serving as the head node
- 2 x Raspberry Pi Zero W's serving as compute nodes
- 2 x Raspberry Pi Zero 2W's serving as compute nodes
- 1 x [ClusterHAT](https://clusterhat.com) serving as the network interface between the head and compute nodes

The ClusterHAT is the equipment that makes this cluster possible, along with the custom Raspberry Pi OS images provided from its accompanying website. All nodes currently run off a single 64GB SD card inserted into the Raspberry Pi 4B; the compute nodes are booted from NFS shares set up on the custom OS image with assitance from the ClusterHAT unit itself. I've set up a shared directory for all five nodes to use for Slurm jobs and programs requiring MPI.

At the moment, I have the Pi 4B and the Zero 2W's each running [BOINC clients][https://boinc.berkeley.edu/] performing jobs for [Asteroids@home][https://asteroidsathome.net]. I had considered running the BOINC clients through Docker Swarm, and while these three nodes are capable of doing so, I think it would be best to devote all possible compute resources to simply running the clients bare metal.

I hope to use this cluster to learn as much as I can about high performance computing. Victor Eijkhout's [The Art of HPC][https://theartofhpc.com/] series of books look to be promising on this end, giving ample examples of programs written in C, C++, and Fortran that make use of parallelization as well as providing a good coverage of the theoretical background of HPC. 

In setting up this cluster (particularly configuring Slurm and MPICH), I tried to follow a number of resources online of people who have built similar Raspberry Pi clusters over the years. Some of the information in the guides is out of date, so I'd like to write up short guides soon of how I set up this cluster. I hope to have them written by the end of this upcoming week.
