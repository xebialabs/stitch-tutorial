Stitch tutorial
===============

This tutorial will teach you how to use Stitch capability of digital.ai Deploy, when deploying to a Kubernetes cluster. For more information about Stitch, please see https://lalala/introductiontoStitch documentation secion.

## Prerequisites

1.Install digital.ai Deploy 9.8 or later. Please refer to the installation guide http://lalalal/deployinstallation

- For the purpose of this tutorial it is advised not to run Deploy in a container, since it will be harder to deploy to the same host if Docker Desktop Kubernetes is used.

2.Download XL CLI version 9.8
https://docs.xebialabs.com/v.9.8/release/how-to/install-the-xl-cli

3.Check that your K8s context points to your Kubernetes cluster (`kubectl cluster-info`)

## Configuration

3.Configure the Deploy with Infrastructure CIs to point to your Kubernetes cluster

- Kubernetes cluster configuration CI - `Infractructure - New - k8s - Master`
- Name it `kubernetes-cluster`
- Provide `TLS certificate`', `TLS private key`, `API server URL`, `CA certificate`. You can obtain these from your `.kube\config`
- Once created, find this CI in the Explorer, and using its context menu create a namespace CI. Name it `default`.

4.Please verify if connecton to your Kubernetes cluster works by running a connection check on `Infrastructure/kubernetes-cluster`.

5.Configure the Deploy with the Environment CI to point to the 'default' namespace of your Kubernetes CI

- Kubernetes environment CI - `Environments - New - Environment`
- Name it `kubernetes-env-prod`
- In `Containers` filed find your `Infrastructure/kubernetes-cluster/default`

## Setup

1.Configure a sample 'PetClinic' application.

Run `xl apply -f xebialabs.yaml` from the 'PetClinic'  directory of the tutorial repository "https://pampam/stitch-tutorial". It will create for you the Petclinic kubernetes application under `Applications/PetClinic/1.0`.

2.Add a source of Stitch sample customization to Deploy

- In Deploy UI navigate to 'Stitch' section. Find 'Sources' tab and use 'Add Git source'.
- Give it a name `stitch-tutorial`
- For `Repository Url` property use "https://pampam/stitch-tutorial"
- Leave other fields default
- Click 'Test' to verify the connection, and 'Save'
- Use a 'Refresh' button to mionitor for when a synchronization of customizations from the GutHub repository into the Deploy finishes.
- In case of issues use 'View log' button for troubleshooting.

3.Check available customizations

In Deploy UI navigate to 'Stitch' section. Find 'Rules' tab and click on 'k8s-tutorial' namespace. It should give you a list of customization rules now available in Deploy.

4. Goto 'Explorer' section to deploy the 'Petlinic' app.
- check preview
[tbd]