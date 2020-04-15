# Digikube

Digikube is integrated stack cosnsisting of various digital platform technologies packaged on top of Kubernetes.
Current Digikube version is specifically designed for GCP and Kubernetes v1.14+

There are three github repositories for digikube.  These are:
1. digikube-public : This is public repository with public read access
2. digikube-core : This is private repository with bulk of the digikube code.  Access token for this repository will be shared on need basis.
3. c1-dev1 : This is private repository for storing the configuration details of your digikube environment. (Currently this repo is configured as public with read access to all.  But it can also be created as private repo.)

## Preparation
To setup your digikube environment, follow the steps below.

1. Request the access token for digikube-core
2. Clone the digikube-public repository
3. Clone the c1-dev1 repository
4. edit cloned digikube-public repository to modify the following:
   - create-digikube-master
     Edit the following lines and update with appropriate values for your environment.
     ```
     DIGIKUBE_MASTER_PROJECT="digikube-master3"
     DIGIKUBE_CLOUD_REGION="us-central1"
     ```
     This script created the master project in GCP to securly hold the digikube private repo access token.	
   - create-digikube
     Edit the following lines and update with appropriate values for your environment.
     ```
     digikubeInstanceRawRepoUrl="https://raw.githubusercontent.com/samdesh-gcp1/c1-dev1/master"
     digikubeMasterProject="digikube-master3"
     digikubeCoreRepoAccessTokenVersion="1"
     digikubeInstanceRepoAccessTokenVersion="1"
     ```
   - delete-digikube
     Edit the following lines and update with appropriate values for your environment.
     ```
     digikubeInstanceRawRepoUrl="https://raw.githubusercontent.com/samdesh-gcp1/c1-dev1/master"
     digikubeMasterProject="digikube-master3"
     digikubeCoreRepoAccessTokenVersion="1"
     digikubeInstanceRepoAccessTokenVersion="1"
     forcedFlag="--forced"
     ```

## Setting up digikube-master 

   - Login to your GCP web console
   - Launch cloud shell
   - Unset the cloud project setting by executing the following command:
     ```
     gcloud config unset project
     ```
   - Execute the following command to create master project and populate github access token secret:
     ```
     wget --quiet --no-cache -O - https://raw.githubusercontent.com/samdesh-gcp1/digikube-public/master/create-digikube-master | bash
     ```
     Modify the url to refer to the public repo you have created in step 2 above
   - Verify if the master project is successfully created
   - Verify that the github access token secrete is created

## Setting up digikube cluster

   - Login to your GCP web console
   - Launch cloud shell
   - Unset the cloud project setting by executing the following command:
     ```
     gcloud config unset project
     ```
   - Execute the following command to create digikube cluster:
     ```
     wget --quiet --no-cache -O - https://raw.githubusercontent.com/samdesh-gcp1/digikube-public/master/create-digikube | bash
     ```
     modify the url to refer to the public repo you have created in step 2 above
   - Verify if execution is successfull (it may take upto 10 min to complete the entire process).  Verify if the cluster resources are successfully created.
   - SSH to the bastion host and go to digikube directory.
     ```
     cd /opt/digikube/
     ```
   - digikube directory should have three folders
     - core - contains all the code for digikube
     - clusters/cluster1 - contains artifacts related to your cluster (config files)
     - exec - contains logs and cluster lock files
   - View the logs to verify the cluster deployment process
   - Execute the following command to verify cluster status:
     ```
     digiops cluster validate
     ```
   - The cluster is up and ready
	
## Stopping and starting the cluster (without deleting)
   
   - SSH to the bastion host
   - Execute the following command to stop the cluster:
     ```
     digiops cluster stop
     ```
   - Execute the following command to start the cluster:
     ```
     digiops cluster start
     ```
   - Validate the cluster status using the following command:
     ```
     digiops cluster validate
     ```
	
## Deleting digikube cluster
  
   - Login to your GCP web console
   - Launch cloud shell
   - Unset the cloud project setting by executing the following command:
     ```
     gcloud config unset project
     ```
   - Execute the following command to delete digikube cluster:
     ```
     wget --quiet --no-cache -O - https://raw.githubusercontent.com/samdesh-gcp1/digikube-public/master/delete-digikube | bash
     ```
     Modify the url to refer to the public repo you have created in step 2 above
   - Verify if execution is successfull (it may take upto 5-7 min to complete the entire process).  Verify if the cluster resources are successfully deleted.
   - The cluster is deleted
