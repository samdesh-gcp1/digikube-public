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

	a. create-digikube-master
		Edit the following lines and update with appropriate values for your environment.
  ```DIGIKUBE_MASTER_PROJECT="digikube-master3"
  DIGIKUBE_CLOUD_REGION="us-central1"
  ```
 		This script creates the master project in GCP to securly hold the digikube private repo access token.
		
	b. create-digikube
		Edit the following lines and update with appropriate values for your environment.
		`digikubeInstanceRawRepoUrl="https://raw.githubusercontent.com/samdesh-gcp1/c1-dev1/master"`
		`digikubeMasterProject="digikube-master3"`
		`digikubeCoreRepoAccessTokenVersion="1"`
		`digikubeInstanceRepoAccessTokenVersion="1"`
		
	c. delete-digikube
		Edit the following lines and update with appropriate values for your environment.
		`digikubeInstanceRawRepoUrl="https://raw.githubusercontent.com/samdesh-gcp1/c1-dev1/master"`
		`digikubeMasterProject="digikube-master3"`
		`digikubeCoreRepoAccessTokenVersion="1"`
		`digikubeInstanceRepoAccessTokenVersion="1"`
		`forcedFlag="--forced"`
		
5.  wget --quiet --no-cache -O - https://raw.githubusercontent.com/samdesh-gcp1/digikube-public/master/create-digikube | bash





### 0.26.1

**Image:** `quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.26.1`

_Changes:_

- [X] [#4617](https://github.com/kubernetes/ingress-nginx/pull/4617) Fix ports collision when hostNetwork=true
- [X] [#4619](https://github.com/kubernetes/ingress-nginx/pull/4619) Fix issue #4244

### 0.26.0

**Image:** `quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.26.0`

_New Features:_

- Add support for NGINX [proxy_ssl_* directives](https://github.com/kubernetes/ingress-nginx/pull/4327)
- Add support for [FastCGI backends](https://github.com/kubernetes/ingress-nginx/pull/4344)
- [Only support SSL dynamic mode](https://github.com/kubernetes/ingress-nginx/pull/4356)
- [Add nginx ssl_early_data option support](https://github.com/kubernetes/ingress-nginx/pull/4412)
- [Add support for multiple alias and remove duplication of SSL certificates](https://github.com/kubernetes/ingress-nginx/pull/4472)
- [Support configuring basic auth credentials as a map of user/password hashes](https://github.com/kubernetes/ingress-nginx/pull/4560)
- Caching support for external authentication annotation with new annotations [auth-cache-key and auth-cache-duration](https://github.com/kubernetes/ingress-nginx/pull/4278)
- Allow Requests to be [Mirrored to different backends](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#mirror) [#4379](https://github.com/kubernetes/ingress-nginx/pull/4379)
- Improve connection draining when ingress controller pod is deleted using a lifecycle hook:

  With this new hook, we increased the default `terminationGracePeriodSeconds` from 30 seconds to 300, allowing the draining of connections up to five minutes.

  If the active connections end before that, the pod will terminate gracefully at that time.

  To efectively take advantage of this feature, the Configmap feature [worker-shutdown-timeout](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#worker-shutdown-timeout) new value is `240s` instead of `10s`.

  **IMPORTANT:** this value has a side effect during reloads, consuming more memory until the old NGINX workers are replaced.

  ```yaml
  lifecycle:
    preStop:
      exec:
        command:
          - /wait-shutdown
  ```

- [mimalloc](https://github.com/microsoft/mimalloc) as a drop-in replacement for malloc.

  This feature can be enabled using the [LD_PRELOAD](http://man7.org/linux/man-pages/man8/ld.so.8.html) environment variable in the ingress controller deployment

  Example:

  ```yaml
  env:
  - name: LD_PRELOAD
    value: /usr/local/lib/libmimalloc.so
  ```

  Please check the additional [options](https://github.com/microsoft/mimalloc#environment-options) it provides.

_Breaking Changes:_

- The variable [$the_real_ip variable](https://github.com/kubernetes/ingress-nginx/pull/4557) was removed from template and default `log_format`.
- The default value of configmap setting [proxy-add-original-uri-header](https://github.com/kubernetes/ingress-nginx/pull/4604) is now `"false"`.



# digikube-public

digikube-public is the starting point for deploying digikube environment.



