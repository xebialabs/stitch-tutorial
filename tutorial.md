Stitch tutorial
===============

This tutorial will teach you how to use Stitch capability of digital.ai Deploy, when deploying to a Kubernetes cluster. For more information about Stitch, please see [Introduction to Stitch](https://docs.xebialabs.com/v.9.8/deploy/stitch/introduction-to-stitch).

## Prerequisites

1. Install digital.ai Deploy 9.8 or later. Please refer to the [installation guide](https://docs.xebialabs.com/v.9.8/deploy/how-to/set-up-xl-deploy-in-production/).


 - For the purpose of this tutorial it is advised not to run Deploy in a container, since it will be harder to deploy to the same host if Docker Desktop Kubernetes is used.


2. Download XL CLI [version 9.8](https://docs.xebialabs.com/v.9.8/release/how-to/install-the-xl-cli)

3. Check that your K8s context points to your Kubernetes cluster (`kubectl cluster-info`)

## Configuration

1. Configure Deploy with Infrastructure CIs to point to your Kubernetes cluster


 - Create Kubernetes cluster configuration CI - `Infractructure - New - k8s - Master`
 - Name it `kubernetes-cluster`
 - Provide `TLS certificate`, `TLS private key`, `API server URL`, `CA certificate`. You can obtain these from your `.kube\config` values ('client-certificate-data', ' client-key-data', 'server', and 'certificate-authority-data' respectively)
 - Once created, find this CI in the Explorer, and use CI's context menu to create a namespace CI. Name it `default`.


2. Please verify if the connecton to your Kubernetes cluster works by running a connection check on `Infrastructure/kubernetes-cluster`.

3. Configure the Deploy with the Environment CI to point to the 'default' namespace of your Kubernetes infractruecture CI


 - Create Kubernetes environment CI - `Environments - New - Environment`
 - Name it `kubernetes-env-prod`
 - In `Containers` filed find your `Infrastructure/kubernetes-cluster/default`

## Setup

1. Configure a sample 'PetClinic' application as CI in Deploy.


 - Download 'PetClinic' folder from the [Stitch tutorial](https://github.com/xebialabs/stitch-tutorial) GitHub repository to your local machine.
 - Run XL CLI command `xl apply -f xebialabs.yaml` in the 'PetClinic'  directory. It will use 'DevOps as Code' to create the Petclinic kubernetes application for you, under the `Applications/PetClinic/1.0` CI path.
 - This is a Kubernetes-packaged application that contains YAML manifest with 'Deployment' and 'Service'.


2. Add a source of Stitch tutorial sample customizations to Deploy:


 - In Deploy UI navigate to 'Stitch' section. Find 'Sources' tab and use 'Add Git source'.
 - Give it a name `stitch-tutorial`
 - For `Repository Url` property use "https://github.com/xebialabs/stitch-tutorial"
 - For `Branch` property use "main"
 - Leave other fields default
 - Click 'Test' to verify the connection, and 'Save'
 - Use a 'Refresh' button to mionitor for when a synchronization of customizations from the GutHub repository into the Deploy finishes.
 - In case of issues use 'View log' button for troubleshooting.


3. Check available Stitch customizations

In Deploy UI navigate to 'Stitch' section. Find 'Rules' tab and click on 'k8s-tutorial' namespace. It should give you a list of customization rules now available in Deploy.


4. Build a deployment plan for the 'Petlinic' app


 - Goto 'Explorer' section to find the application under `Applications/PetClinic/1.0`
 - Start a Deployment and map this application to your Kubernetes environment `Environments/kubernetes-env-prod`
 - Click 'Preview' to investigate the deployment plan created, including applied Stitch customization to application's YAML
 - Navigate to 'Stitch Preview' tab for details on the effect of each customization
   - 'Invocation 1' would be a 'kind:Deployment' manifest.
   - Look at the difference between 'Original' and 'Modified' content for the manifest under the 'Stitch invocation output'.
   - It shows the effect of all customization applied to this manifest.
   - Click on 'Show processing steps' and click on a particular customization step under 'Processor Execution' to observe the effect of change by each step.


5. Proceed to deploying the application by using 'Deploy' button, or Cancel the deployment.

 ## Summary
 This tutorial has shown you how to configure Deploy to use customizations for Kubernetes deployments, and observe the effect of customization during the planning phase of a deployment.

 For more information on authoring customizations, please refer to the product documentation.
