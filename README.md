# AWS AMI: nginx on ubuntu using packer

# Description
Create an nginx web server on ubuntu image to deploy static pages.\
The image is build on AWS by default in "eu-central-1" region.
This image contains a default instalation of nginx. If you need to change the nginx confiration please refer to [nginx docs](http://nginx.org/en/docs/)

# How to use

If you don't have AWS credentials you can create them on [this page](https://console.aws.amazon.com/iam/home?#security_credential).

Add your AWS credentials as two environment variables:
```
export AWS_ACCESS_KEY_ID=<YOUR_ACCESS_KEY>
export AWS_SECRET_ACCESS_KEY=<YOUR_SECRET_KEY>
```

Clone the repository on your computer
```bash
git clone git@github.com:ionhashicorp/nginx-on-ubuntu-aws-image.git
```

drive into the directory named nginx-on-ubuntu-aws-image
```bash
cd nginx-on-ubuntu-aws-image
```

build the image with the following command:
```
packer build nginx-on-ubuntu.pkr.hcl
```

# Change the region of the AMI
You can specify a different region where you want to deploy the image by specifying the [region](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html) code:

```
packer build --var region=<REGION_CODE> nginx-on-ubuntu.pkr.hcl
```


Sample output:
```
$ cd nginx-on-ubuntu-aws-image
$ packer build --var region=eu-west-1 nginx-on-ubuntu.pkr.hcl
nginx-on-ubuntu.amazon-ebs.ubuntu: output will be in this color.

==> nginx-on-ubuntu.amazon-ebs.ubuntu: Prevalidating any provided VPC information
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Prevalidating AMI Name: nginx-on-ubuntu-aws-20210916082457
    nginx-on-ubuntu.amazon-ebs.ubuntu: Found Image ID: ami-016ee74f2cf016914
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Creating temporary keypair: packer_6142ff59-2325-d50f-c8b4-787f77af28bf
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Creating temporary security group for this instance: packer_6142ff5b-587a-3f5e-625d-031863649390
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Authorizing access to port 22 from [0.0.0.0/0] in the temporary security groups...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Launching a source AWS instance...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Adding tags to source instance
    nginx-on-ubuntu.amazon-ebs.ubuntu: Adding tag: "Name": "Packer Builder"
    nginx-on-ubuntu.amazon-ebs.ubuntu: Instance ID: i-08deb517313655f27
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Waiting for instance (i-08deb517313655f27) to become ready...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Using SSH communicator to connect: 3.249.164.251
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Waiting for SSH to become available...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Connected to SSH!
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Provisioning with shell script: /var/folders/k2/jxw8lbzx3k91ml2q8w02zfv00000gq/T/packer-shell529205201
==> nginx-on-ubuntu.amazon-ebs.ubuntu:
==> nginx-on-ubuntu.amazon-ebs.ubuntu: WARNING: apt does not have a stable CLI interface. Use with caution in scripts.
==> nginx-on-ubuntu.amazon-ebs.ubuntu:
 
                <<< some output was omitted for brevity >>>


    nginx-on-ubuntu.amazon-ebs.ubuntu: Setting up nginx-core (1.10.3-0ubuntu0.16.04.5) ...
    nginx-on-ubuntu.amazon-ebs.ubuntu: Setting up nginx (1.10.3-0ubuntu0.16.04.5) ...

                <<< some output was omitted for brevity >>>


==> nginx-on-ubuntu.amazon-ebs.ubuntu: Stopping the source instance...
    nginx-on-ubuntu.amazon-ebs.ubuntu: Stopping instance
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Waiting for the instance to stop...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Creating AMI nginx-on-ubuntu-aws-20210916082457 from instance i-08deb517313655f27
    nginx-on-ubuntu.amazon-ebs.ubuntu: AMI: ami-07059453584c9b47e
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Waiting for AMI to become ready...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Skipping Enable AMI deprecation...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Terminating the source AWS instance...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Cleaning up any extra volumes...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: No volumes to clean up, skipping
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Deleting temporary security group...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Deleting temporary keypair...
Build 'nginx-on-ubuntu.amazon-ebs.ubuntu' finished after 3 minutes 31 seconds.

==> Wait completed after 3 minutes 31 seconds

==> Builds finished. The artifacts of successful builds are:
--> nginx-on-ubuntu.amazon-ebs.ubuntu: AMIs were created:
eu-west-1: ami-07059453584c9b47e

$
```
