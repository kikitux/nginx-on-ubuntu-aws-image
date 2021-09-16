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

AMI image located at:
[AWS AMI management page](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=eu-central-1#Images:visibility=owned-by-me;search=learn-packer-linux-aws;sort=tag:Name)

# Change the region of the AMI
You can specify a different region where you want to deploy the image by specifying the [region](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html) code:

```
packer build --var region=<REGION_CODE> nginx-on-ubuntu.pkr.hcl
```


# Sample output
```
$ packer build nginx-on-ubuntu.pkr.hcl
nginx-on-ubuntu.amazon-ebs.ubuntu: output will be in this color.

==> nginx-on-ubuntu.amazon-ebs.ubuntu: Prevalidating any provided VPC information
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Prevalidating AMI Name: nginx-on-ubuntu-aws-20210916121300
    nginx-on-ubuntu.amazon-ebs.ubuntu: Found Image ID: ami-01299931803ce83f6
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Creating temporary keypair: packer_614334cc-5ddf-5e3e-ea8e-b812147e7326
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Creating temporary security group for this instance: packer_614334cd-bf4b-6996-efa1-82a57dbf97c2
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Authorizing access to port 22 from [0.0.0.0/0] in the temporary security groups...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Launching a source AWS instance...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Adding tags to source instance
    nginx-on-ubuntu.amazon-ebs.ubuntu: Adding tag: "Name": "Packer Builder"
    nginx-on-ubuntu.amazon-ebs.ubuntu: Instance ID: i-025b85d57f55090b9
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Waiting for instance (i-025b85d57f55090b9) to become ready...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Using SSH communicator to connect: 3.64.125.148
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Waiting for SSH to become available...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Connected to SSH!
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Provisioning with shell script: /var/folders/k2/jxw8lbzx3k91ml2q8w02zfv00000gq/T/packer-shell769877108
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Stopping the source instance...
    nginx-on-ubuntu.amazon-ebs.ubuntu: Stopping instance
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Waiting for the instance to stop...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Creating AMI nginx-on-ubuntu-aws-20210916121300 from instance i-025b85d57f55090b9
    nginx-on-ubuntu.amazon-ebs.ubuntu: AMI: ami-0636dab9b4d96888d
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Waiting for AMI to become ready...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Skipping Enable AMI deprecation...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Terminating the source AWS instance...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Cleaning up any extra volumes...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: No volumes to clean up, skipping
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Deleting temporary security group...
==> nginx-on-ubuntu.amazon-ebs.ubuntu: Deleting temporary keypair...
Build 'nginx-on-ubuntu.amazon-ebs.ubuntu' finished after 3 minutes 52 seconds.

==> Wait completed after 3 minutes 52 seconds

==> Builds finished. The artifacts of successful builds are:
--> nginx-on-ubuntu.amazon-ebs.ubuntu: AMIs were created:
eu-central-1: ami-0636dab9b4d96888d
$
```
