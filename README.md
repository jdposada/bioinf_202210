# Fundamentals of Artificial Intelligence in Medicine

This repository will contain the code to be used as part of the 2022-10 class on Bioinformatics (yup different name..) at Universidad del Norte.

## How to use this repo

We are going to use mostly R but some Python code here and there. To ensure everyone has the same development environment we are going to use Docker. Docker is a virtualization technology that will allow us to run the same software even ensure dependencies at the OS level are the same. Below are the steps you need to follow in order to ensure the software will run on your machine.


- Install Docker on your machine. [link](https://docs.docker.com/get-docker/) 
    - Check a small [introduction](https://www.youtube.com/watch?v=_dfLOzuIg2o) to Docker so you are somewhat familiar to what it is. You do no need to worry about technical details of Docker at the moment since I am providing everything ready to go for you. 
- Please verify your installation by running `docker run hello-world` on command line / terminal. 
- Run the following command `docker run -d --name=rstudio-ohdsi -p 8787:8787 -e USER=ohdsi -e PASSWORD=ohdsi odysseusinc/rstudio-ohdsi:latest`.
- Open a Web browser and type on the bar `http://localhost:8787`. You will be promoted for a user and password. Both are **ohdsi**. The username and password can be changed if you change the values of the parameters `USER` and `PASSWORD` on the command run on the previous step
- After login you should see RStudio server on your browser. Type this command in the R terminal `library(PatientLevelPrediction)` The library should load with no issues.

## Remote Development Environment on Cloud

### Azure setup and VM

- Open an [Azure Student Account](https://azure.microsoft.com/en-us/free/students/) using your Uninorte email. This will give you 100 USD in credits
- Start a VM with 1 Core and 4GB of RAM.  We will use Ubuntu 20.04. Here some [instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal) for you.
- Connect to the VM using SSH. If you are in windows you will need to use a [compatible SSH client](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client). If you are in Ubuntu you are all set. the command you will need to run is something like this `ssh oopclass@10.1.1.1`. In this command oopclass is the user that was created during the VM creation and the IP is assigned automatically by Azure.
- Install Docker and Git **inside the VM**
    - [Docker instructions](https://docs.docker.com/engine/install/ubuntu/)
    - [Git Instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- Add current users to sudoers to use Docker as current user **inside the VM**
    - `sudo groupadd docker`
    - `sudo usermod -aG docker $USER`
    - `newgrp docker`
    - Check that you everything is ok by running `docker run hello-world`
    - **Turn off** the VM for the changes to have effect and **Turn on** again
- *Optional*
    - If you want to login on Github and you have two factor authentication enabled you need to first
        - [Generate a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
        - Run this command so your Git credentials are stored `git config --global credential.helper store`
- Clone our course repository on /home/$USER **inside the VM**. `git clone https://github.com/jdposada/bioinf_202210.git`
    - *Optional*
        - You could decide to [Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) the main repo so you have minor changes and other files in it. If that is the case you could keep it private. If you made this decision you should clone your fork instead of the class repo. Keep in mind you need to [keep your fork updated](https://stackoverflow.com/questions/39819441/keeping-a-fork-up-to-date)

### Locally

- Connect to the VM using an SSH tunnel
    - `ssh -L 8787:localhost:8787 investigacion@<Your IP Here>`
- Run the following command on the Azure VM 
    - `docker run -d --name=rstudio-ohdsi --network=host -v /home/$USER/bioinf_202210:/home/ohdsi/workdir -e USER=ohdsi -e PASSWORD=ohdsi odysseusinc/rstudio-ohdsi:latest`
- To check that the container is properly running by executing on the terminal `docker ps`. You should see a container with the name `rstudio-ohdsi`
- Open a Web browser and type on the bar `http://localhost:8787`. You will be prompted for a user and password. Both are **ohdsi**. The username and password can be changed if you change the values of the parameters `USER` and `PASSWORD` on the command run on the previous step. Be sure to check the box `Stay signed in when browser closes` if you want to RStudio server to run in the background without you actively being there. This is very useful for long runnings. 
- After login you should see RStudio server on your browser. Type this command in the R terminal `library(PatientLevelPrediction)` The library should load with no issues.

### IMPORTANT!! Please stop the VM if you are not actively using it. If you do not that it will eat your free credits. 
