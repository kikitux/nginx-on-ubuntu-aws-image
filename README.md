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
packer build --var region=<REGION_CODE> nginx-on-ubuntu.pkr.hc
```
