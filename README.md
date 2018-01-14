# Data-Science-Toolkit

The below will explain how to create an AWS instance to run on a virtual machine versus the local machine and using docker to run programs such as jupyter. The advanages of this method are ease of scaling memory and processing on the virtual machine and automatically managed and up to date software by using docker.

![AWS vs. local](https://github.com/cleonadja/Data-Science-Toolkit/blob/master/Machine.png)


## How to configure a SSH key

 1. Generate a SSH key locally by entering `ssh-keygen` in the bash shell (Git Bash)
 2. The key will be saved in a file locally - the generic file path would be `~/.ssh/id_rsa`
 3. Verify the ssh key created by entering less `~/.ssh/id-rsa.pub`
   - Sample result:
    
    ssh-rsa            AAAAB3NzaC1yc2EAAAADAQABAAABAQCrZmvU0XFx8sVt+Z+g+eKmYCzIp2/1dRgM7Mc/UHD4H2Hz61PAaKM3uksBTNDw8NOzojsKQesURXUj2OiJ5/0qFvnA4vMsFgk0xtiLdOYst+MgGQOHzhMo8+5/j6ASQxFBfZlKPV0qgw7NxYFLC0j0FMlQmumy0wIeUcmVoAgJwm/bFUbKwuYwgXV+dTXN+p8Ox2AAig+JSJprPIlCpjooXgzssNSQUSt5DzriTWQahdtiWIdehRApDyOeKGac8iTS5bdD1/7lL6mUPaXH778A77zerP/OoUmmqKMr6NZE63MhcukRFw/40Xvb9wScuZ8AVjcau7RNqzHoTeEsTiql ELSHN002@W7-PC0ED7Y8
    
 4. Import SSH key to AWS instance following these steps:
    - Launch AWS Services --> EC2
    - At the top of the screen under Resources select "Key Pairs" (or on the left panel under Network & Security)
    - From the Key Pairs page select "Import Key Pair"
    - Copy/paste SSH key from bash shell into public key contents and give the key a name

--> All set to connect AWS to your local machine once you set up an instance.  
    
## How to create security groups in AWS

 1. In AWS EC2 dashboard select "Security Groups" from the Resources module at the top of the page or the Network & Security module on the left panel
 2. Select "Create Security Group", name it and give it a description
 3. On the Inbound tab configure rules for:
    - SSH - TPC - 22 - Anywhere
    - HTPPS - TPC - 443 - Anywhere
    - HTTP - TPC - 80 - Anywhere
    - Custom TPC Rule (Jupyter) - 8888 - Anywhere
    - Custom TPC Rule (Docker Hub) - 2376 - Anywhere
    - Custom TPC Rule (open port) - 80 - Anywhere

--> All set to use this security group with an AWS instance.

## How to set up Amazon EC2

 1. Select "Launch Instance" from the EC2 dashboard in AWS
 2. Select an Amazon Machine Image (AMI) - for example Unbuntu Server
 3. Choose and instance type - for example t2.micro
 4. Configure instance details - use the preset information
 5. Add storage - in the chosen example up to 30 GB are provided for free
 6. Add tags - can be ignored
 7. Configure security group - choose "Select an existing security group", then select the previously created security group
 8. Review and launch the instance
 9. In the final confirmation step choose and existing key pair and select the previously set key pair

--> You should get a notification that the instance is running and you can check the state in the EC 2 dashboard under instances

## How to install Docker 

 1. In Git Bash connect to the AWS instance that was created by entering `ssh ubuntu@35.165.48.162` (your public IP address)
     - The public IP address for the created instance can be obtained by selecting the instance on the EC2 dashboard instances tab
 2. Install Docker by entering `curl -sSL https://get.docker.com|sh`
 3. The command line Docker client will require sudo access in order to issue commands. Add Ubuntu user to the Docker group by entering `sudo usermod -aG docker ubuntu`
 4. A reboot is required for the changes to take effect. Enter `sudo reboot`
 5. Once the system has rebooted reconnect to the AWS instance by entering `ssh ubuntu@35.165.48.162` (your public IP address)
 6. Check if Docker is installed by entering `docker -v`
 7. Check what Docker container is running by entering `docker ps`
 
--> Step 6. should show you the Docker version installed and step 7. should return the container running

Summary:

![](https://github.com/cleonadja/Data-Science-Toolkit/blob/master/AWS%20Set%20up%20Process.png)

## How to access Jupyter

 1. Download the Jupyter Data Science Notebook on the EC2 instance by entering `docker pull jupyter/datascience-notebook` 
    - for ease of use it can be tagged dsnb `docker tag jupyter/datascience-notebook dsnb`
 2. Run the image by creating a container `docker run -v/home/ubuntu:/home/jovyan -p 80:8888 -d dsnb`
    - `-v` saves everything on the server
    - `-p` connects Docker port to AWS port
    - `-d` runs it detached
    
 3. Confirm Jupyter is running `docker ps` will show all running containers
 4. Access Jupyter in the browser [http://35.165.48.162] (your public IP address)
 5. Retrieve access token `docker exec 576a jupyter notebook list` (first four digits of you container ID)
 6. Copy/Paste the into the access key request in the browser.
    - Example: token=67f4314e4acb8b1160343dcc8b5deb629badaf5288b71ec2 

## Budget of the costs of running Jupyter Data Science Notebook Server for three months using 3 different kinds of EC2 instances

The costs of running the Jupyter Data Science Notebook on t2.micro, t2.small, and t2.medium for 3 months are $199,50.

![Cost Analysis](https://github.com/cleonadja/Data-Science-Toolkit/blob/master/Cost%20Analysis.png)
