# Digikube

There are three github repositories for digikube.  These are:
1. digikube-public : This is public repository with public read access
2. digikube-core : This is private repository with bulk of the digikube code.  Access token for this repository will be shared on need basis.
3. c1-dev1 : This is private repository for storing the configuration details of your digikube environment. (Currently this repo is configured as public with read access to all.  But it can also be created as private repo.)

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

5. Setting-up digikube-master
	a. Login to your GCP web console
	b. Launch cloud shell
	c. Unset the cloud project setting by executing the following command:
	   `gcloud config unset project`
	d. Execute the following command to create master project and populate github access token secret:
           `wget --quiet --no-cache -O - https://raw.githubusercontent.com/samdesh-gcp1/digikube-public/master/create-digikube-master | bash`
            Modify the url to refer to the public repo you have created in step 2 above
	e. Verify if the master project is successfully created
	f. Verify that the github access token secrete is created

6. Setting up digikube cluster
	a. Login to your GCP web console
	b. Launch cloud shell
	c. Unset the cloud project setting by executing the following command:
			gcloud config unset project
	d. Execute the following command to create digikube cluster:
			wget --quiet --no-cache -O - https://raw.githubusercontent.com/samdesh-gcp1/digikube-public/master/create-digikube | bash
			modify the url to refer to the public repo you have created in step 2 above
	e. Verify if execution is successfull (it may take upto 10 min to complete the entire process).  Verify if the cluster resources are successfully created.
	f. SSH to the bastion host and go to digikube directory.
			cd /opt/digikube/
	g. digikube directory should have three folders
			core - contains all the code for digikube
			clusters/cluster1 - contains artifacts related to your cluster (config files)
			exec - contains logs and cluster lock files
	h. View the logs to verify the cluster deployment process
	i. Execute the following command to verify cluster status:
			digiops cluster validate
	j. The cluster is up and ready
	
7. Stopping and starting the cluster
	a. Execute the following command to stop the cluster:
			digiops cluster stop
	b. Execute the following command to start the cluster again:
			digiops cluster start
			
8. Deleting digikube cluster
	a. Login to your GCP web console
	b. Launch cloud shell
	c. Unset the cloud project setting by executing the following command:
			gcloud config unset project
	d. Execute the following command to delete digikube cluster:
			wget --quiet --no-cache -O - https://raw.githubusercontent.com/samdesh-gcp1/digikube-public/master/delete-digikube | bash
			modify the url to refer to the public repo you have created in step 2 above
	e. Verify if execution is successfull (it may take upto 5-7 min to complete the entire process).  Verify if the cluster resources are successfully deleted.
	f. The cluster is deleted
