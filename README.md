# Data-Science-Toolkit
How to configure a SSH key

 1) Generate a ssh key locally by entering ssh-keygen in the bash shell (Git Bash)
 2) The key will be saved in a file locally - the generic file path would be ~/.ssh/id_rsa
 3) Verify the ssh key created by entering less ~/.ssh/id-rsa.pub
    Sample result:
    
    ssh-rsa            AAAAB3NzaC1yc2EAAAADAQABAAABAQCrZmvU0XFx8sVt+Z+g+eKmYCzIp2/1dRgM7Mc/UHD4H2Hz61PAaKM3uksBTNDw8NOzojsKQesURXUj2OiJ5/0qFvnA4vMsFgk0xtiLdOYst+MgGQOHzhMo8+5/j6ASQxFBfZlKPV0qgw7NxYFLC0j0FMlQmumy0wIeUcmVoAgJwm/bFUbKwuYwgXV+dTXN+p8Ox2AAig+JSJprPIlCpjooXgzssNSQUSt5DzriTWQahdtiWIdehRApDyOeKGac8iTS5bdD1/7lL6mUPaXH778A77zerP/OoUmmqKMr6NZE63MhcukRFw/40Xvb9wScuZ8AVjcau7RNqzHoTeEsTiql ELSHN002@W7-PC0ED7Y8
    
 4) Import ssh key to AWS instance following these steps:
    - Launch AWS Services --> EC2
    - At the top of the screen under Resources select "Key Pairs" (or on the left panel under Network & Security)
    - From the Key Pairs page select "Import Key Pair"
    - Copy/paste SSH key from bash shell into public key contents and give the key a name

--> all set to connect AWS to your local machine once you set up an instance.  
    
How to create  security groups in AWS
 1) In AWS EC2 dashboard select "Security Groups" from the Resources module at the top of the page or the Network & Security module on the       left panel
 2) Select "Create Security Group", name it and give it a description
 3) on the Inbound tab confgire rules for:
    - SSH - TPC - 22 - Anywhere
    - HTPPS - TPC - 443 - Anywhere
    - HTTP - TPC - 80 - Anywhere
    - Custom TPC Rule (Jupyter) - 8888 - Anywhere
    - Custom TPC Rule (Docker Hub) - 2376 - Anywhere

--> all set to use this security group with an AWS instance.

How to set up Amazon EC2
 1) Select "Launch Instance" from the EC2 dashboard in AWS
 2) Select an Amazon Machine Image (AMI) - for example Unbuntu Server
 3) Choose and insatnce type - for example t2.micro
 4) Configure insatcne details - use the preset information
 5) Add storage - in the chosen example up to 30 GB are provided for free
 6) Add tags - can be ignored
 7) Configure security group - choose "Select an existing security group", then select the previously createdd security group
 8) Review and launch the instance
 9) In the final confirmation step choose and exisiting key pair and select the previously set key pair

--> You should get a notification that the instance is running and you can check the state in the EC 2 dashboard under instances

How to install Docker 
 1) In Git Bash connect to the AWS instance that was created by entering ssh ubuntu@35.165.48.162 (your public IP address)
     - the public IP address for the created instance can be obtained by selecting the instance on the EC2 dashboard instances tab
 2) Check if docker is already installed by enetring docker -v
 3) Install Docker by enetering curl -sSL https://get.docker.com|sh
 4) The commmand line docker client will require sudo access in order to issue commands. Add ubuntu user to the doscker group by             entering suod usermod -aG docker ubuntu

How to obtain the correct Docker image

How to confirm the correct Docker image is running as a container

Jupyter notebook security concerns
Anything else I may have forgotten ...
Create at least one diagram of your overall system.
A detailed budget of the costs of running a Jupyter Data Science Notebook Server for three months using at least three different kinds of EC 2 instances.
