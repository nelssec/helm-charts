Qualys Cloud Agent Helm Chart

This Helm chart installs the Qualys Cloud Agent across all nodes in a Kubernetes cluster using a DaemonSet. 
It deploys a privileged container that mounts the host filesystem and installs the agent directly onto each node.

Prerequisites

You need Helm 3 installed and cluster admin permissions. 
You'll also need your Activation ID, Customer ID, and the Qualys server URI for your environment. These values are available from the Qualys console.

Adding the Repository

Run the following commands to add the Helm repository and update your local cache:

helm repo add nelssec https://nelssec.github.io/helm-charts  
helm repo update

Installation

The chart will be installed in the qualys namespace. 
It will be created if it doesn't exist. The install requires four values: activationId, customerId, serverUri, and logLevel. 
These are passed in using set-string flags.

Example:

helm install qualys-agent nelssec/qualys-agent \
  --namespace qualys --create-namespace \
  --set-string secrets.activationId=your-activation-id \
  --set-string secrets.customerId=your-customer-id \
  --set-string config.serverUri=https://your.qualys.server.uri \
  --set-string config.logLevel=INFO

The install command creates a Kubernetes Secret containing the activationId and customerId. 
It also creates a ConfigMap with the serverUri and logLevel. 
These values are passed into the container as environment variables.

Uninstalling

To remove the agent and clean up the resources, run:

helm uninstall qualys-agent --namespace qualys
