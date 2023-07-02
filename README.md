
#CONTAINERISED APPLICATION

Test it via local and cloud using Kubernetes

Tools

Kubectl

The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs. For more information including a complete list of kubectl operations.

Minikube

Like kind, minikube is a tool that lets you run Kubernetes locally. minikube runs an all-in-one or a multi-node local Kubernetes cluster on your personal computer (including Windows, macOS and Linux PCs) so that you can try out Kubernetes, or for daily development work.

Kubeadm

You can use the kubeadm tool to create and manage Kubernetes clusters. It performs the actions necessary to get a minimum viable, secure cluster up and running in a user friendly way.


Kops 

AWS EKS


OBJECTIVES
Set up cluster on local and cloud

Install kubectl binary with curl on macOS

Download the latest release:
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl" 

Validate the binary (optional)Download the kubectl checksum file:   curl -LO "https://dl.k8s.io/release/$(curl -L -s 

https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl.sha256"

Validate the kubectl binary against the checksum file:echo "$(cat kubectl.sha256)  kubectl" | shasum -a 256 --check

If valid, the output is:kubectl: OK

If the check fails, shasum exits with nonzero status and prints output similar to:kubectl: FAILEDshasum: WARNING: 1 computed checksum did NOT match

Note: Download the same version of the binary and checksum.

Make the kubectl binary executable.chmod +x ./kubectl
 
Move the kubectl binary to a file location on your system PATH.sudo mv ./kubectl /usr/local/bin/kubectl

sudo chown root: /usr/local/bin/kubectl

Note: Make sure /usr/local/bin is in your PATH environment variable.

Test to ensure the version you installed is up-to-date:kubectl version --client

Note:The above command will generate a warning:WARNING: This version information is deprecated and will be replaced with the output from kubectl version --short.

You can ignore this warning. You are only checking the version of kubectl that you have installed.Or use this for detailed view of version:kubectl version --client --output=yaml
 
After installing the plugin, clean up the installation files:rm kubectl kubectl.sha256

Create a minikube cluster

minikube start

Open the Dashboard

Open the Kubernetes dashboard. You can do this two different ways:
 		Launch a browser
 		URL copy and paste

Open a new terminal, and run:

Start a new terminal, and leave this running.

minikube dashboard

Now, switch back to the terminal where you ran minikube start.

Note:

The dashboard command enables the dashboard add-on and opens the proxy in the default web browser. You can create Kubernetes resources on the dashboard such as Deployment and Service.

If you are running in an environment as root, see Open Dashboard with URL.

By default, the dashboard is only accessible from within the internal Kubernetes virtual network. The dashboard command creates a temporary proxy to make the dashboard accessible from outside the Kubernetes virtual network.

To stop the proxy, run Ctrl+C to exit the process. After the command exits, the dashboard remains running in the Kubernetes cluster. You can run the dashboard command again to create another proxy to access the dashboard.

Create a Deployment

A Kubernetes Pod is a group of one or more Containers, tied together for the purposes of administration and networking. The Pod in this tutorial has only one Container. A Kubernetes Deployment checks on the health of your Pod and restarts the Pod's Container if it terminates. Deployments are the recommended way to manage the creation and scaling of Pods.

Use the kubectl create command to create a Deployment that manages a Pod. The Pod runs a Container based on the provided Docker image.# Run a test container image that includes a webserver

kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
 
View the Deployment:kubectl get deployments

The output is similar to:NAME         READY   UP-TO-DATE   AVAILABLE   AGE

 hello-node   1/1     1            1           1m

cat .kube/config to see the Minikube config file

 View the Pod:kubectl get pods
 
 The output is similar to:NAME                          READY     STATUS    RESTARTS   AGE

 hello-node-5f76cf6ccf-br9b5   1/1       Running   0          1m
 
 View cluster events:kubectl get events
 
  View the kubectl configuration:kubectl config view


<img width="1276" alt="Screenshot 2023-07-02 at 23 16 24" src="https://github.com/stacksimplify/docker-fundamentals/assets/67044030/8247a44f-8787-443b-8794-3bc916a31d7f">

<img width="1279" alt="Screenshot 2023-07-02 at 23 17 00" src="https://github.com/stacksimplify/docker-fundamentals/assets/67044030/5277f65a-054c-4b2c-9cf8-85f82160c9f2">

<img width="1280" alt="Screenshot 2023-07-02 at 23 17 47" src="https://github.com/stacksimplify/docker-fundamentals/assets/67044030/ca1b0bfa-e48d-46fe-8453-55098424f675">



