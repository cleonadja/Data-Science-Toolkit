# Data-Science-Toolkit
How to configure a SSH keys

 1) generate a ssh key locally by entering ssh-keygen in the bash shell (Git Bash)
 2) the key will be saved in a file locally - the generic file path would be ~/.ssh/id_rsa
 3) verify the ssh key created by entering less ~/.ssh/id-rsa.pub
    sample results:
    ssh-rsa     AAAAB3NzaC1yc2EAAAADAQABAAABAQCrZmvU0XFx8sVt+Z+g+eKmYCzIp2/1dRgM7Mc/UHD4H2Hz61PAaKM3uksBTNDw8NOzojsKQesURXUj2OiJ5/0qFvnA4vMsFgk0xtiLdOYst+MgGQOHzhMo8+5/j6ASQxFBfZlKPV0qgw7NxYFLC0j0FMlQmumy0wIeUcmVoAgJwm/bFUbKwuYwgXV+dTXN+p8Ox2AAig+JSJprPIlCpjooXgzssNSQUSt5DzriTWQahdtiWIdehRApDyOeKGac8iTS5bdD1/7lL6mUPaXH778A77zerP/OoUmmqKMr6NZE63MhcukRFw/40Xvb9wScuZ8AVjcau7RNqzHoTeEsTiql ELSHN002@W7-PC0ED7Y8
 4) Import ssh key to AWS instance following these steps:
    - launch AWS Services --> EC2
    - at the top of the screen under Resources select Key pairs (or on the left panel under Network & Security)
    - From the Key Pairs page select Import Key Pair
    
 -   
 
Amazon EC 2
Security Groups
AWS Operating System
Docker Installation
Obtaining the correct Docker image
Running the correct Docker image as a container
Jupyter notebook security concerns
Anything else I may have forgotten ...
Create at least one diagram of your overall system.
A detailed budget of the costs of running a Jupyter Data Science Notebook Server for three months using at least three different kinds of EC 2 instances.
