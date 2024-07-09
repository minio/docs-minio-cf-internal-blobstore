
### MinIO Internal Blobstore Operator Guide

This topic describes how to install and configure Minio Internal Blobstore for VMware Tanzu.

##<a id='install'></a> Install Minio Internal Blobstore for VMware Tanzu

To install Minio Internal Blobstore for VMware Tanzu, do the following:

<ol>
<li>Download the <strong>Minio Internal Blobstore for VMware Tanzu</strong> tile from VMware Tanzu Network.</li>
<li>Navigate to the Ops Manager Installation Dashboard and click <strong>Import a Product</strong> to upload the tile.</li>
<li>Under the <strong>Import a Product</strong> button, click <strong>+</strong> next to the version number of Minio Internal Blobstore for VMware Tanzu.
This adds the tile to the staging area.</li>
</ol>

##<a id='configure'></a> Configure Minio Internal Blobstore for VMware Tanzu

To configure Minio Internal Blobstore for VMware Tanzu, do the following:

<ol>
<li>Click on the newly added <strong>Minio Internal Blobstore for VMware Tanzu</strong> tile.</li>
<li>Assign AZs and Networks.<br/>
<img src="images/az.png">

  <ul>
  <li>Configure regions.</li>
  <li>Configure the Network.</li>
  <li>Click <strong>Save</strong>.</li>
  </ul>

<li>Configure System Domain.<br/>
<img src="images/system-domain.png">

<ul>
<li>Configure the System Domain. This should be the same System Domain that will be configured in the VMware Tanzu Application Service for VMs (TAS for VMs) tile. System Domain is used to construct the BOSH-DNS Alias for the MinIO Internal Blobstore. For ex. if System Domain is configured as <i>system.example.com</i> then the BOSH-DNS Alias for the MinIO Blobstore will be <i>minio-internal-blobstore.system.example.com</i>. This can be used as S3 endpoint in the Tanzu Application Servcie Tile.</li>
<li>Click <strong>Save</strong>.</li>
</ul>

<li>Configure Credentials.<br/>
<img src="images/creds.png">

  <ul>
  <li>Configure AccessKey for Minio, at least 5 characters. This can be left to the default value of "minio".</li>
  <li>Configure SecretKey for Minio, at least 8 characters. Type in a strong secret key.</li>
  <li>The configured AccessKey and SecretKey should be used for S3 Credentials in the Tanzu Application Service Tile's File Storage configuration.</li>
  <li>Click <strong>Save</strong>.</li>
  </ul>

<li>Configure bucket names.<br/>
<img src="images/buckets.png">

  <ul>
  <li>Configure the bucket names. The default values can be left as is.</li>
  <li>The same bucket names has to be entered in the VMware Tanzu Application Service for VMs (TAS for VMs) tile while configuring the "External S3 Compatible blobstore" section.</li>
  <li>Click <strong>Save</strong>.</li>
  </ul>

<li>Configure static IPs (optional)<br/>
<img src="images/static-ips.png">

<ul>
<li>Configure static IPs for minio servers. This is optional. However if the TLS Certificates needs to be configured for HTTPS access (described in the next section), then the Static IPs must be configured and also the same static IPs must be provided for TLS Certificates (described in the next section).</li>
<li>Click <strong>Save</strong>.</li>
</ul>

<li>Configure Certificates for HTTPS<br/>
You can leave the form in the "Disable" state or "Enable" it.
<img src="images/cert-enable-disable.png">

To enable, click "Enable" and then click "Generate RSA Certificate".

<img src="images/cert-enable1.png">

Enter the MinIO BOSH-DNS Alias (ex. <i>minio-internal-blobstore.system.example.com</i>) and IP addresses of minio servers that was configured in the "Configure Static IPs" form. The list needs to be comma-separated. (The IP addresses are not visible in the below screenshot)
<img src="images/cert-enable2.png">
<img src="images/cert-enable3.png">

<ul>
<li>Click <strong>Save</strong>.</li>
</ul>

<li>TAS Tile<br/>
<img src="images/tas-tile.png">

  <ul>
  <li>Choose if TAS Tile for VMs is already installed or not. If "Yes" is chosen, routes to MinIO will be published to the Gorouter for external access (ex. <i>cf curl</i>).</li>
  <li>Click <strong>Save</strong>.</li>
  </ul>

<li>Review errands.<br/>
<img src="images/errands.png">

  <ul>
  <li>There are two post-deploy errands: one to create the default buckets, the other to do the smoke tests.</li>
  <li>There is one pre-delete errand which ensures that all the buckets have been deleted before removal of the tile.</li>
  </ul>

<li>Configure resources.<br/>
<img src="images/resource-config.png">

  <ul>
  <li><strong>minio-server:</strong> For distributed mode, the number of instances should be an even number (at least 4 and at most 16).
You can select the disk size based on the requirements. Usable space of the Minio cluster is calculated as <i>(n/2)*d</i>.
where <i>n</i> is the number of instances and <i>d</i> is the disk size on each instance.
Half the instances store the data and the other half of the instances store the parity.
The cluster can sustain <i>n/2</i> number of instance failures and still be able to serve read requests.
For writes, at least <i>(n/2)+1</i> number of instances should be available.
For example if 6 instances are configured with each instance having 200G, total usable space will be 600G <i>(6/2 * 200)</i>
  </li>
  <li>Click <strong>Save</strong>.</li>
  </ul>

<li>Return to the Ops Manager Installation Dashboard and click <strong>Review Pending Changes</strong> and then <strong>Apply Changes</strong> to install the Minio Internal Blobstore tile.</li>
<img src="images/applying-changes.png">

<li>Note down the MinIO Internal Blobstore access details<br/>
  <ul>
  <li>Note down the BOSH DNS alias ("minio-internal-blobstore" + SystemDomain). For example if you configured SystemDomain as <i>system.example.com</i> , then MinIO BOSH DNS alias will be <i>minio-internal-blobstore.system.example.com</i></li>
  <li>Note down the AccessKey and SecretKey that was configured in step 4.</li>
  <li>Note down the bucket names configured in step 5.</li>
  <li>The above values should be configured in the TAS for VMs Tile's File Storage configuration in the “External S3 Compatible blobstore” section.</li>
  <img src="images/tas-tile-s3-blobstore.png">
  <li>When you save this S3 configuration in the TAS tile for VMs, it will show the following warning which can be ignored. This is because the BOSH DNS alias of MinIO will not be reachable from the Ops Manager. You can choose <strong>Apply anyway</strong> option. Once the VMs for the TAS tile for VMs are deployed, the BOSH DNS alias for MinIO will be resolvable in all the VMs of the TAS tile.</li>
  <img src="images/warning.png">
  </ul>

</ol>

##<a id='inspect'></a> Inspect Minio Blobstore

Minio Client can be installed on the Ops Manager.

To inspect Minio Blobstore, do the following:

1. To download the latest version of Minio Client, run the following commands:

    ```
    wget -O mc http://dl.minio.io/client/mc/release/linux-amd64/mc
    chmod +x mc
    ./mc --help
    ```

2. To configure the Minio Client, run the following command:

    ```
    ./mc config host add myminio http://MINIO-SERVER-IP ACCESS-KEY SECRET-KEY
    ```

   `MINIO-SERVER-IP` can be one of the MinIO server's IP address.

3. To list buckets in Minio blobstore, run the following command:

    ```
    ./mc ls myminio
    ```

##<a id='version'></a> Enable Versioning on the buckets

MinIO's S3 compatible bucket versioning support can be used for efficient BOSH Backup and Restore.

```
$ mc version enable myminio/buildpacks
$ mc version enable myminio/droplets
$ mc version enable myminio/packages
```

Apply lifecycle policy to the three buckets:

```
$ mc ilm  import myminio/test < lifecycle.json
$ mc ilm  import myminio/test < lifecycle.json
$ mc ilm  import myminio/test < lifecycle.json
```

`lifecycle.json` specifies the lifecycle policy:

```
{
  "Rules": [
    {
      "ID": "expire-non-current",
      "Status": "Enabled",
      "Expiration": {
        "ExpiredObjectDeleteMarker": true
      },
      "NoncurrentVersionExpiration": {
        "NoncurrentDays": 30
      }
    }
  ]
}
```

i.e the policy ensures that the deleted objects get purged from the system after 30 days.

NOTE: Please note that this tile creates a deployment with the name minio-internal-blobstore. Make sure that you do not have any other custom BOSH deployment that starts with the string "minio-internal-blobstore" as it causes issues with MinIO's BOSH DNS name resolution.
