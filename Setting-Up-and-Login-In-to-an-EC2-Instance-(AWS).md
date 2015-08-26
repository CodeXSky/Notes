The instructions here follow the ones outlined by Dennis Tenen [here](https://github.com/xpmethod/dhnotes/wiki/Launching-an-AWS-instance) and assume you've already signed-up for AWS and have access to the EC2 console. They also assume the instance you've launched is a Linux instance.

### Setting Up the EC2 Instance
* Make sure the region is set to the nearest in your area. For New York City, the right region is `US East (N. Virginia)`.
* When you launch a new instance, make sure you create a key pair and download it. This key pair will allow you access to your instance.
* In your AWS console, under Instances, make sure you see your new instance `running` and in the right region.
* Note your Public DNS, it will be something like this: `ec2-xx-x-xx-xxx.compute-1.amazonaws.com`.

### Accessing Your Instance
The instructions here are divided between "Local", "AWS Console" and "Remote". "Local" means from your local user (usually in a Terminal window); and "remote" means once you've successfully logged into your instance, as a remote user.