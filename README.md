# CyberArk PAS AWS STS INTEGRATION 2021
This is a tutorial share to you on how to provide a secure access to the AWS consoles using Cyberark AWS STS Integration.
For more detail about CyberArk AWS STS Integration, please visit below mentioned website.

- [CyberArk AWS STS Integration](https://docs.cyberark.com/Product-Doc/OnlineHelp/PAS/Latest/en/Content/PASIMP/PSM-AWS-CloudServicesManagement.htm?TocPath=Administration%7CComponents%7CPrivileged%20Session%20Manager%7CPSM%20Connectors%7CCloud%20Services%20Management%20Tools%7C_____1)

## Guide Version
- Version 1.0
- Release Date 10 June 2021

## Prerequisite
- You should have access to Cyberark PAM
- You should have access to the AWS IAM Service
 
## Lab Architecture
- EKS is used as platform to host the [demo app](https://github.com/jeepapichet/cityapp). The application will connect to a MySQL database to retreive data, and during authenication, [secrets](https://docs.cyberark.com/Product-Doc/OnlineHelp/AAM-DAP/Latest/en/Content/Get%20Started/key_concepts/secrets.html) will be used by the application
- The lab was based on Conjur Version 12.0.0

![Architecture](https://github.com/ivanckleecity/CyberArk-DAP-EKS-Lap-2021/blob/main/images/architecture_eks.JPG)

## Lab Guide
- Task 0 to 1 is to setup the AWS environment to enable the logon and 
- Task 2 to 4 is to create an EKS envirunment to run contrainer application to access an external Database. The External Database will be seating in your Jump Host
- Task 5 to 8 is to setup CyberArk Conjur Secrets Manager to protect containerized applications and DevOps tools secure access to resources. The lab will show case how to setup and use CyberArk Summon and Secretless Broker 


### [Task 0: Setup Jump Host](00-Setup_Jump_Host.md)

### [Task 1: Install Necessary Software in Jump Host](01-Install_Necessary_Software.md)

### [Task 2: Create EKS Cluster](02-Create_EKS_Cluster.md)

### [Task 3: Setup DataBase Server](03-Setup_DataBase_Server.md)

### [Task 4: Deploy App with Embedded Secret](04-Deploy_App_with_Embedded_Secret.md)

### [Task 5: Setup Conjur Master Server](05-Setup_Conjur_Master.md)

### [Task 6: Deploy Follower with Seed Fetcher](06-Deploy_Follower_with_Seed_Fetcher.md)

### [Task 7: Deploy App to EKS Cluster with CyberArk Summon Secrets Injection](07-Deploy_App_with_Summon_Secrets_Injects.md)

### [Task 8: Deploy App to EKS Cluster with CyberArk Secretless Broker](08-Deploy_App_with_Cyberark_Secretless_Broker.md)

### [Congratulation!!! Lab Completed](Task09/readme.md)  
