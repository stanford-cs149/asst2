# AWS Setup Instructions #

For performance testing, you will need to run this assignment on a VM instance on Amazon Web Services (AWS). We'll be providing (or have already sent) you student coupons that you can use for billing purposes. Here are the steps for how to get setup for running on AWS.

> [!NOTE]
> Please don't forget to SHUT DOWN your instances when you're done for the day to avoid burning through credits overnight!

### Creating a VM ###

1. Now you're ready to create a VM instance. Log in to the [AWS EC2 dashboard](https://us-west-2.console.aws.amazon.com/ec2/home?region=us-west-2#Home) for the `us-west-2` region and click on the button that says `Launch instance`.
![Launch instance](figs/launch_instance.png?raw=true)

> [!TIP]
> It is recommended to do most of your development locally / on myth, and only use your AWS machine for performance tuning.

2. Choose the `Ubuntu Server 24.04 LTS (HVM), SSD Volume Type` AMI:
![AMI](https://github.com/user-attachments/assets/34501c4a-a0d8-47d9-a622-f0dc6ffdaa4e)

3. Choose the `c7g.4xlarge` instance type.
![Instance type](https://github.com/user-attachments/assets/ecbe5840-4751-4dc8-b348-0620005679e7)

> [!TIP]
> If you find that you really need to experiment on an AWS machine after developing most of your code on myth or locally, use a `c7g.xlarge` instance (which offers 4 CPU cores and is more cost-effective).

> [!IMPORTANT]
> `c7g.4xlarge` instances cost $0.58 / hour, so leaving one running for a whole day will consume $13.92 worth of your AWS coupon. Remember to shut off the instance when you're not using it!

4. Change the size of the volume to 64 GB to accomodate the packages we will need to install to make the instance functional for the assignment:
![Storage](https://github.com/user-attachments/assets/4d736f35-a0bd-4e59-8b3e-329289105a11)

5. You will need a key pair to access your instance. In `Key pair (login)` section, click `Create a new key pair` and give it whatever name you'd like. This will download a keyfile to your computer called `<key_name>.pem` which you will use to login to the VM instance you are about to create. Finally, you can launch your instance.
![Key Pair Step 1](figs/keypair_step1.png)
![Key Pair Step 2](https://github.com/user-attachments/assets/6fd9f6f7-668a-4842-b196-30176c962e5a)

6. Confirm all details and lunch instance  
![Lunch instance](https://github.com/user-attachments/assets/7e6deb82-65fb-4ed9-a372-f56a2a437506)

7. Now that you've created your VM, you should be able to __SSH__ into it. You need the public IPv4 DNS name to SSH into it, which you can find by navigating to your instance's page and then clicking the `Connect` button, followed by selecting the SSH tab (note, it may take a moment for the instance to startup and be assigned an IP address):
![Connect](figs/connect.png?raw=true)

Make sure you follow the instructions to change the permissions of your key file by running `chmod 400 path/to/key_name.pem`.
Once you have the IP address, you can login to the instance by running this command:
~~~~
ssh -i path/to/key_name.pem ubuntu@<public_dns_name>
~~~~

> [!WARNING]
> If you need to step away during setup after creating your instance, be sure to shut it down. Leaving it running could deplete your credits, and you may incur additional costs.


### Setting up the VM environment ###

8. Once you SSH into your VM instance, you'll want to install whatever software you need to make the machine a useful development environment for you.  For example we recommend:
~~~~
sudo apt update
sudo apt install make g++ python3 # Required
sudo apt install vim
~~~~


9. Download [starter code](https://github.com/stanford-cs149/asst2/archive/refs/heads/master.zip) to your local computer, [initiate your Git](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository) (or another VCS of your choice) repo and **be sure to keep it in private**, then clone your repo on the VM.

### Fetching your code from AWS ###

You can retrieve files on your VM by running the following if needed:
~~~~
scp -i path/to/key_name.pem ubuntu@<public_dns_name>:/path/to/file /path/to/local_file
~~~~

You are highly encouraged to keep your code version controlled and accessible through VSC on your local computer. It's not a good practice to use `scp` for code transferring.

### Stopping the VM ###

10. You can stop the VM by navigating to the instance page, clicking "Instance state", and then selecting "Stop instance".
![Stop instance](figs/stop_instance.png?raw=true)

Note that terminating the instance will delete the instance and all associated files. Instances can be stopped in the AWS web console or by running `sudo shutdown -P now` while logged in.

If you're confused about any of the steps, having problems with setting up your account or have any additional questions, reach out to us on Ed!

> [!CAUTION]
> For one last time, please **DO NOT FORGET TO SHUT OFF THE INSTANCE WHEN UNUSED.**
> 
> We may not be able to provide additional AWS credits / reimburse any cost if you go over allocated credits for any reason.


### Performance leaderboard ###

We may release a leaderboard for you to submit your code to which will compare the top-performing solutions. For assignment 2 this will just be for fun, but stay tuned for more updates on Ed!
