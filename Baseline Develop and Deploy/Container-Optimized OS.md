# Container-Optimized OS

[Container-Optimized OS: Google's Solution for Containerized Workloads](https://youtu.be/79UP4L9vcSU)

Container-Optimized OS is an operating system image for your Compute Engine VMs that is optimized for running Docker containers, and is Google's recommended OS for running containers on Google Cloud Platform. In this lab you will create a Container-Optimized instance using the Cloud Console and the CLI.

Since it comes with all container-related dependencies preinstalled, Container-Optimized OS allows your cluster to quickly scale up or down in response to traffic or workload changes, optimizing your spend and improving your reliability.

Container-Optimized OS powers many GCP services such as Kubernetes Engine and Cloud SQL, making it Google's go-to solution for container workloads.

## Container-Optimized OS benefits
* Run Containers Out of the Box: Container-Optimized OS instances come pre-installed with the Docker runtime and cloud-init. With a Container-Optimized OS instance, you can bring up your Docker container at the same time you create your VM, with no on-host setup required.

* Smaller attack surface: Container-Optimized OS has a smaller footprint, reducing your instance's potential attack surface.

* Locked-down by default: Container-Optimized OS instances include a locked-down firewall and other security settings by default.

* Automatic Updates: Container-Optimized OS instances are configured to automatically download weekly updates in the background; only a reboot is necessary to use the latest updates.

## Use cases for Container-Optimized OS
Container-Optimized OS can be used to run most Docker containers. You should consider using Container-Optimized OS as the operating system for your Compute Engine instance if you have the following needs:

* You need support for Docker containers or Kubernetes with minimal setup.

* You need an operating system that has a small footprint and is [security hardened](https://cloud.google.com/container-optimized-os/docs/concepts/security) for containers.

* You need an operating system that is tested and verified for running Kubernetes on your Compute Engine instances.

## Container-Optimized OS features
Compute Engine provides several [public VM images](https://cloud.google.com/compute/docs/images#os-compute-support) that you can use to create instances and run your container workloads. Some of these public VM images have a minimalistic container-optimized operating system that includes newer versions of Docker, rkt, or Kubernetes preinstalled. The following public image families are designed specifically to run containers:

* [Container-Optimized OS from Google](https://cloud.google.com/container-optimized-os/docs/)
* Includes: Docker, Kubernetes
* Image project: cos-cloud
* Image family: cos-stable
* [CoreOS](https://coreos.com/)
* Includes: Docker, rkt, Kubernetes
* Image project: coreos-cloud
* Image family: coreos-stable
* [Ubuntu](https://www.ubuntu.com/)
* Includes: LXD
* Image project: ubuntu-os-cloud
* Image family: ubuntu-1604-lts
* [Windows](https://www.microsoft.com/)
* Includes: Docker
* Image project: windows-cloud
* Image family: windows-1709-core-for-containers
  
In a production environment, if you need to run specific container tools and technologies on images that do not include them by default, [install those technologies](https://cloud.google.com/compute/docs/containers/#installing) manually.

## Steps

### Create an instance using the console
To run a Compute Engine instance with the Container-Optimized OS and a Docker container of your choice:

1. Click on Compute Engine > VM instances, then click on Create.

2. Click Create.


### Verify your Docker environment
1. Click SSH on the containerized-vm line to SSH into the containerized-vm instance.

2. List all available Docker containers:
    ```sh
    sudo docker ps
    ```
3. On the VM instance console, click on the External IP for containerized-vm instance, which will open a new tab. 

4. You can also see the web page by adding the External IP to http://EXTERNAL_IP in a new browser window or tab.

### Create an instance using CLI
Now you use the Cloud Shell command line to create a Container-Optimized OS instance.

1. In Cloud Shell, enter the following command to see what Container-Optimized OS images are available on Google Cloud Platform to create an instance.
    ```sh
    gcloud compute images list --project cos-cloud  --no-standard-images
    ```
2. Use the gcloud compute instances create command with --image and --image-project flags to create a cos node image instance:
    ```sh
    gcloud beta compute instances create-with-container containerized-vm2 \
        --image cos-stable-72-11316-136-0 \
        --image-project cos-cloud \
        --container-image nginx \
        --container-restart-policy always \
        --zone us-central1-a \
        --machine-type n1-standard-1
    ```
    In the above example, cos-stable-72-11316-136-0 is one of the available cos releases. Please use the latest available image from cos-stable family and replace it with an image for your VM instance. It is recommended to use --preemptible flag for one-off experimental instances.
3. In the Cloud Shell enter the following commands to create firewall rules to allow HTTP traffic from the internet and to enable all internal traffic within the VPC:
    ```sh
    gcloud compute firewall-rules create allow-containerized-internal\
    --allow tcp:80 \
    --source-ranges 0.0.0.0/0 \
    --network default
    ```
4. For this step, you need the external IP address of your containerized-vm2 instance. You can look up the address in the VM Instances page in the Cloud Platform Console.
5. 
    In a browser, enter your external IP address to verify that nginx is running:
    ```url
    http://[YOUR_EXTERNAL_IP_ADDRESS]
    ```
