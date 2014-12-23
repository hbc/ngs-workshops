## Setup Galaxy for courses

We try to use the latest [Galaxy Cloudman](https://wiki.galaxyproject.org/CloudMan) version where possible. While Cloudman offers in-place updates through it's user interface we found it better to roll out a new instance with major releases, if only to prevent compatibility issues and to wipe user data from previous students.

To spin up an instance you need your access key and secret key from the AWS account information page. Ideally you'd spin up the instance via [BioCloudCentral](https://biocloudcentral.herokuapp.com/launch); alternatively this can be done through the [AWS Interface](https://aws.amazon.com/).

1. Go the `AWS Management Console`
2. Select `EC2`
3. Select `Instances`
4. Select `Launch Instances`, `Community AIMs`
5. Search for the current Cloudman AMI, v2.3. , AMI ID `ami-a7dbf6ce`
6. Select the AMI and pick an instance type (medium or above recommended; for classes I go with the m3.2xlarge)
7. Go with `configure instance details`
8. In the next screen leave everything at default but the availability zone (usually `us-east-1d`); it must be the same zone used for previous spin ups or Cloudman won't find the stored user data. If spinning up a new instance pick whatever zone you like but note it for future use
9. Under `Advanced Details` cut and paste the following configuration:

    cluster_name: YOUR_CLUSTER_NAME
    password: YOUR_CLOUDMAN_PASSWORD
    access_key: AWS_ACCESS_KEY
    secret_key: AWS_SECRET KEY
    admin_users:
     - shosui@hsph.harvard.edu
     - rkhetani@hsph.harvard.edu

Replace the name with something new if spinning up a clean instance, but keep track of it to restart the same instance at a later time. Replace the keys with your account, replace admin users with whoever should have full access to the _Galaxy_ admin interface; this is independent of the Cloudman admin backend. All that is needed for the Cloudman console access is the password. 

10. Go through `Add Storage`, `Tag Instance`, to `Configure Security Group`. Select an existing security group, ideally one that was previously defined through BioCloudCentral or define your own following the Cloudman manual. I am using a security group called `Galaxy_Cloudman`. 
11. Use the Galaxy keypair and the Galaxy_Cloudman security groups. Use the default admin user, cloud@galaxyproject.org. Use m1.large instance types for now, deployed in us-east-1d.
12. Click 'Review and Launch`; click `Launch`. This will ask for a keypair which you will either have to generate yourself and upload, _or_ you can re-use an existing one. 

The instance will now spin up. I strongly recommend reserving a dedicated IP address for the server (AWS Console, `EC2`, `Elastic IPs`) and assigning it to the instance that is starting up. Navigate to the IP and wait till the Cloudman placeholder comes up, then log into the Cloudman backend using any username (`foo` will do) and the password provided above. If this is a new instance Cloudman will ask how much disk space to set aside; for most courses 100-200GB will be more than sufficient. For a course deployment I'd suggest to switch to one of the larger instances with 8+ cores and in particular good networking performance; the biggest stumbling block seem to stem from jobs that get dropped due to the network falling over when 25+ students submit a BWA job at the same time.

Wait `till Galaxy itself becomes available (follow the progress in the log, the status LEDs will switch from yellow to green). In the Cloudman `Admin` interface (link in the top bar) validate that all services are running and that the admin users have been configured correctly. Access Galaxy itself and you are done.

## Populating a new Galaxy instance

In theory the Galaxy [BioBlend]() module can spin up instances, tear them down, add tools, etc.; in practice I found lots of bugs and irritations that make working with it a bit tricky. For the time being all I use the API for is to populate the shared data library _after_ I've spun up a Cloudman instance via AWS or BioCloudCentral.

Start an [Python Notebook](http://ipython.org/ipython-doc/dev/notebook/notebook.html#starting-the-notebook-server) with `ipython notebook` and navigate to the GitHub repo to find the 'Cloudman' folder alongside the `Cloudman_Upload.ipynb` notebook and open it. 

The explanatory text in the notebook should guide you through the process. Fair to say that the only part reliably working at this point consists of the data upload, and I'd stick to these cells (ignoring the others).

The notebook does _not_ contain the actual data files. That archive is stored in a [public Dropbox folder]() that you will need to download and extract into `~/cloudman/data`. You want to end up with something close to:

```
oho-2:ngs-workshops oho$ ls -l cloudman/data
total 0
drwxr-xr-x@ 5 oho  staff  170 Dec 23 10:38 ChIP-Seq
drwxr-xr-x@ 7 oho  staff  238 Dec 23 10:38 Galaxy Introduction
drwxr-xr-x@ 5 oho  staff  170 Dec 23 10:38 RNA-Seq
```

Make sure to add the `cloudman/data/*` to your `.gitignore` file as some of the data files are rather large.



