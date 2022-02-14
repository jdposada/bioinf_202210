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

