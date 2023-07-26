
# Continuous Integration using Jenkins, Nexus ,Sonarqube.

The vprofile web application is continuously integrated using Jenkins, SonarQube, and Nexus using a declarative Jenkins pipeline and  stage of the continuous integration process is integrated through a Slack channel for each  stage outcome notification.

## Pre-requisite
- Jdk-1.8 or later
- Maven3 or later version 
- Aws Account
- Slack channel
## Project Architecture 
![Screenshot](https://drive.google.com/uc?export=view&id=1CPdf89M7r5lGw2ypX0zMWUFwpleerJkd)

## Project overview
- Whenever a developer commits and pushes their code changes to GitHub, Jenkins automatically fetches those changes and triggers a build, followed by testing.
- Once all testing stages are passed, Maven generates a .war file of the code.
- The generated code is accessed by SonarQube for code analysis using quality gates, which generates a quality report of the code.
- When the quality check for the code is passed, Nexus Sonatype comes into play, downloading all required dependencies and storing the deployable artifacts of their updated version.

## Project Execution Steps
### 1.Create key-pair 
- create key pair on aws for login into instances.
### 2.Create Security group
- create security group for jenkins,Nexus,and Sonarqube
- Enable Jenkins to connect to Nexus and Sonatype instances, set inbound rules for each security group and open the corresponding ports. 

#### jenkins Security group
![Screenshot](https://drive.google.com/uc?export=view&id=1KL2WtA8ZxkBmnB7Iz3CTtCqn5tMgHOyo)


#### Nexus security group
![Screenshot](https://drive.google.com/uc?export=view&id=1Sn-CMZabyDFd8Hy4gbDWVW4VE2el9DbM)


#### Sonarqube Security group
![Screenshot](https://drive.google.com/uc?export=view&id=12Er8oRAfJpp0QMfH0sx9Ic5mjITnG-82)

### 3.Create Ec2 instances 
- By utilizing the script listed in the userdata for each instance, create  instance for Nexus, Jenkins, and SonarQube. 
![Screenshot](https://drive.google.com/uc?export=view&id=1UD0NApDwG7rnONuZF24cP3Al45TK4fk0)

### 4.Jenkins setups and Plugins
1. Access the jenkins UI running on port 8080
2. create Account and login to jenkins
3. Install the suggetsed plugins used in project
####  plugins list
- Github Integration
- Maven Integration
- Nexus Artifact Uploader
- Sonarqube Scanner
- Slack notification
- Timestamp (Artifact-versioning)
4. Configure the tools used in pipeline 
#### Jdk
![Screenshot](https://drive.google.com/uc?export=view&id=1fsCnS0MWVXoJ3p0ojsw1rvd1ZFzEcQVQ)

#### Sonarqube
![Screenshot](https://drive.google.com/uc?export=view&id=1uENXXQA8FYwRQo3Fi7n31gGsHn2a26PW)

#### Maven
![Screenshot](https://drive.google.com/uc?export=view&id=1tM_Dz7BCVTSbhqhsnm6tjYM8q-mGY1-X)

### 5.Nexus repository setup
1. Access the nexus sonatype running on port: 8081
2. create account and login to nexus
3. Go to Setting and create required repositories
![Screenshot](https://drive.google.com/uc?export=view&id=1XkNwcdTxsy9QZ1MDlPEF3hyj39-IOefi)
![Screenshot](https://drive.google.com/uc?export=view&id=1tqVVjcB4VsNzBcvfsXQUs2Mf4ztiIlJt)

### 6.Github Webhook
- Integrate jenkins with github using private key used for ssh authentication of github.

### 7.Sonarqube server Integration
- login into SonarQube
- Genrate a tocken in SonarQube 
- Integrate SonarQube with jenkins using webhooks
![Screenshot](https://drive.google.com/uc?export=view&id=19HxLNbO1q2nXU0-BNfsmE7FyH_xbHmBv)

- set the qulaity gate condition for code Analysis.
- when quality gate condition passed upload the Artifact to nexus repository.

### 8.Slack Notification
- create slack workspace and channel
- integrate jenkins app to slack channel
- configure slack channel with jenkins by adding jenkins credential 
- test the connection ,status must be success.
![Screenshot](https://drive.google.com/uc?export=view&id=1jL1n34RK1cbwcSib9SWXz6mHvzK3JTU8)

- set slack notification as post Declarative action stage in pipeline 

## Project Result
### Successful pipeline of Project
![Screenshot](https://drive.google.com/uc?export=view&id=1iVwilISL6mg33ypDJzVjCD-lpDqlXSyY)

### Sonarqube report Result
![Screenshot](https://drive.google.com/uc?export=view&id=1R412Tn4bDPZQFWTgunS5aVkHONxXlToW)

### Artifact uploaded to nexus Successfuly 
![Screenshot](https://drive.google.com/uc?export=view&id=1be5ll83V6_iCqdwH8SG-vlQ3bn6S2kgb)

### notification on slack after successful build job
![Screenshot](https://drive.google.com/uc?export=view&id=1h3M5oO0rEf7xZRpt8wQ0GtiCteV5X5HH)


