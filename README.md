# digikube-public

digikube-public is the starting point for deploying digikube environment.

There are three github repositories for digikube.  These are:
1. digikube-public : This is public repository with public read access
2. digikube-core : This is private repository with bulk of the digikube code.  Access token for this repository will be shared on need basis.
3. c1-dev1 : This is private repository for storing the configuration details of your digikube environment. (Currently this repo is configured as public with read access to all.  But it can also be created as private repo.)

To setup your digikube environment, follow the steps below.

1. Request the access token for digikube-core
2. Clone the digikube-public repository
3. Clone the c1-dev1 repository
4. edit cloned digikube-public repository to modify the following:
		a. create-digikube-master
				Edit the following lines and update with appropriate values for your environment.
					DIGIKUBE_MASTER_PROJECT="digikube-master3"   <= Change the value as required.
					DIGIKUBE_CLOUD_REGION="us-central1"			 <= Change the value as required.
				This script creates the master project in GCP to securly hold the digikube private repo access token.
		b. create-digikube
				Edit the following lines and update with appropriate values for your environment.
					digikubeInstanceRawRepoUrl="https://raw.githubusercontent.com/samdesh-gcp1/c1-dev1/master"  <= Change this to the repo created in step 3 above
					digikubeMasterProject="digikube-master3"     <= Change the value as required.
					digikubeCoreRepoAccessTokenVersion="1"		 <= This should be 1 unless you have renewed the access token
					digikubeInstanceRepoAccessTokenVersion="1"	 <= This should be 1 unless you have renewed the access token
		c. delete-digikube
				Edit the following lines and update with appropriate values for your environment.
					digikubeInstanceRawRepoUrl="https://raw.githubusercontent.com/samdesh-gcp1/c1-dev1/master"  <= Change this to the repo created in step 3 above
					digikubeMasterProject="digikube-master3"     <= Change the value as required.
					digikubeCoreRepoAccessTokenVersion="1"		 <= This should be 1 unless you have renewed the access token
					digikubeInstanceRepoAccessTokenVersion="1"	 <= This should be 1 unless you have renewed the access token
					forcedFlag="--forced"                        <= Forced deletion of resources even after errors during deletion process
5.  wget --quiet --no-cache -O - https://raw.githubusercontent.com/samdesh-gcp1/digikube-public/master/create-digikube | bash



