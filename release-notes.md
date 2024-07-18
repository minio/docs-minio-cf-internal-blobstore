
### MinIO Internal Blobstore Release Notes
##<a id="ver1.0.21"></a> v1.0.21

**Release Date:** Jul 18, 2024

* Update bpm-release to 1.2.23

##<a id="ver1.0.20"></a> v1.0.20

**Release Date:** Jul 9, 2024

* Update stemcell from Ubuntu Xenial to Ubuntu Jammy
  for MinIO BOSH Release 2023-03-24T21-41-23Z

##<a id="ver1.0.19"></a> v1.0.19

**Release Date:** March 30, 2023

* Update MinIO BOSH Release to 2023-03-24T21-41-23Z
* Fixes security issue CVE-2023-28432

##<a id="ver1.0.18"></a> v1.0.18

**Release Date:** January 11, 2022

* Update MinIO BOSH Release to 2022-01-08T03-11-54Z
* Fixes security issue: [https://github.com/minio/minio/security/advisories/GHSA-j6jc-jqqc-p6cx](https://github.com/minio/minio/security/advisories/GHSA-j6jc-jqqc-p6cx)


##<a id="ver1.0.17"></a> v1.0.17

**Release Date:** August 25, 2021

* Update MinIO BOSH Release to 2021-08-25T00-41-18Z

##<a id="ver1.0.16"></a> v1.0.16

**Release Date:** May 21, 2021

* Update MinIO BOSH Release to 2021-04-06T23-11-00Z
* Fix tile to remove route advertiser. Now route_registrar runs on minio VMs.

##<a id="ver1.0.15"></a> v1.0.15

**Release Date:** February 24, 2021

* Update MinIO BOSH Release to 2021-02-19T04-38-02Z
* Fix tile to accept '@' character in secret key
* Fix tile to support running errands in a 1 CPU VM

##<a id="ver1.0.14"></a> v1.0.14

**Release Date:** February 10, 2021

* Update MinIO BOSH Release to 2021-02-07T01-31-02Z

##<a id="ver1.0.13"></a> v1.0.13

**Release Date:** February 1, 2021

* Update MinIO BOSH Release to 2021-01-30T00-20-58Z
* MinIO release fixes security issue described here: [https://blog.min.io/p/8b0fc737-709b-4273-9430-93a58860e8e3](https://blog.min.io/p/8b0fc737-709b-4273-9430-93a58860e8e3)


##<a id="ver1.0.12"></a> v1.0.12

**Release Date:** November 18, 2020

* Update MinIO BOSH Release to 2020-11-13T20-10-18Z.1
* MinIO release fixes security issues found in Go libraries.

##<a id="ver1.0.11"></a> v1.0.11

**Release Date:** August 21, 2020

* Update MinIO BOSH Release to 2020-08-16T18-39-38Z.1
* Support for versioning to enable efficient BOSH BBR

##<a id="ver1.0.10"></a> v1.0.10

**Release Date:** May 3, 2020

* Update MinIO BOSH Release to 2020-04-23T00-58-49Z.3
* Includes security fix which allows Admin API access for invalid S3V4 signature.
* Support for BOSH DNS alias for MinIO instances.
* Support for external access through Gorouter.

##<a id="ver1.0.9"></a> v1.0.9

**Release Date:** December 12, 2019

* Hotfix for 2019-10-12T01-39-57Z to fix a bosh rolling upgrade issue

##<a id="ver1.0.8"></a> v1.0.8

**Release Date:** November 22, 2019

Fix the tile version numer as 1.0.8 (no change to the MinIO source code)

##<a id="ver1.0.7"></a> v1.0.7

**Release Date:** November 20, 2019

Features included in this release:

* Update MinIO Version 2019-07-24T02-02-23Z

##<a id="ver1.0.6"></a> v1.0.6

**Release Date:** August 15, 2019

Features included in this release:

* Support HTTPS on minio-servers

##<a id="ver1.0.5"></a> v1.0.5

**Release Date:** August 3, 2019

Features included in this release:

* Updated to Minio Version 2019-07-24T02-02-23Z
* Support for HTTPS configuration for HAProxy load balancer

##<a id="ver1.0.4"></a> v1.0.4

**Release Date:** February 12, 2019

Features included in this release:

* Updated to Minio Version 2019-02-12T21-58-47Z containing performance and security fixes

##<a id="ver1.0.3"></a> v1.0.3

**Release Date:** January 4, 2019

Features included in this release:

* Updated to Minio Version 2018-12-27T18-33-08Z containing a fix related to BOSH upgrades.
* Support Static IPs configuration for minio servers

##<a id="ver1.0.2"></a> v1.0.2

**Release Date:** December 3, 2018

Features included in this release:

* Updated to Minio Version 2018-11-30T03-56-59Z containing a fix related to BOSH upgrades.
* Changed default disk size per VM to 1TB.

##<a id="ver1.0.1"></a> v1.0.1

**Release Date:** November 30, 2018

Features included in this release:

* Support for stand-alone or distributed deployments.

* Derived from Minio Version 2018-11-06T01-01-02Z.

