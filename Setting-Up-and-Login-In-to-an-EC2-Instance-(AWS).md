The instructions here follow the ones outlined by Dennis Tenen [here](https://github.com/xpmethod/dhnotes/wiki/Launching-an-AWS-instance) and assume you've already signed-up for AWS and have access to the EC2 console. They also assume the instance you've launched is a Linux instance.

### Setting Up the EC2 Instance
* Make sure the region is set to the nearest in your area. For New York City, the right region is `US East (N. Virginia)`.
* When you launch a new instance, make sure you create a key pair and download it. This key pair will allow you access to your instance.
* In your AWS console, under Instances, make sure you see your new instance `running` and in the right region.
* (Optional) Set up an `Elastic IP` and associate it with your current instance. Once you've done this, your Public DNS will change.
* Note your Public DNS, it will be something like this: `ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com`.
* Modify your security group in the AWS console to allow SSH access: In the Security Groups section (I'm not sure if you already have a group or if you need to create a new one) select the group and in Actions select Edit Inbound Rules. There select Add Rule and set type to `SSH`, protocol to `TCP`, port range to `22` and source to `Anywhere` and `0.0.0.0/0`.

### Accessing Your Instance
The instructions here are divided between "Local", "AWS Console" and "Remote". "Local" means from your local user (usually in a Terminal window); and "remote" means once you've successfully logged into your instance, as a remote user.
* (Local) To log in to your AWS instance use `ssh -vi path/to/key.pem ec2-user@ec2-xx-xx-xxx-xxx.compute-1.amazonaws.com`.

### Creating New Users
* (Remote) Once you're logged into your instance, you can create new users and groups. To add a user do `sudo adduser username`.
* (Remote) Change to the new user with `sudo su - username`. Create a `.ssh` directory to place the `authorized_keys` file: use `mkdir .ssh`.
* (Remote) Change the permissions of the `.ssh` directory to `700`: `chmod 700 .ssh`. And create a file named `authorized_keys` in the `.ssh` directory: `touch .ssh/authorized_keys`.
* (Remote) Edit the `authorized_key` file with a text editor (ie. Nano) and paste the _public_ key for your key pair. You can find your public key by running the following local command (local means on your computer, not on the instance): `ssh-keygen -y`. This command should return your _public_ key. Copy this and paste it on your remote `authorized_key` file.
* More detailed instructions about these two last steps can be found [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/managing-users.html) and [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#retrieving-the-public-key).
* To remove a user do `sudo userdel -r username`. The `r` flag deletes the home directory and mail spool.