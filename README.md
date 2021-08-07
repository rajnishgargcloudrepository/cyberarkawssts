Cyberark STS Plugin Integration with AWS

In this short step by step guide, we will see how Cyberark STS Plugin can be used to provide secure AWS console access to different group of privilege users.

I believe STS plugin is one of the best approaches what all the customer should leverage upon due to following reasons-
1.	No need to create multiple user identity on AWS IAM
2.	No credentials involved (Cyberark STS plugin involves the use of logon account)
3.	Provide JIT access to any of the given privilege users which will be tied to the granular roles or have specific set of permissions

We have divided the entire configuration into 3 main stages.

1.	Creation and On-Boarding of the STS logon account
  
 a.	Go to AWS IAM Service and then click on to add new user
 
 ![STSLogonAccount](https://user-images.githubusercontent.com/60601287/128140479-56d1fcd3-9410-411e-afb9-99a5f864588b.png)
 
 b.	Proceed without assigning any policy or permissions
 ![Permissions](https://user-images.githubusercontent.com/60601287/128140664-ab0a0168-d1a0-4eee-9e9a-1a0a9f93d97b.png)

c.	Click on create user and note down the User, Access key ID and Secret Access Key.
![awsstslogonaccouncreation](https://user-images.githubusercontent.com/60601287/128140817-bfc7c1d6-b9d9-4429-a43e-295a33218e13.png)

d.	We will create new policy where we will assign enough permission to the AWSSTSLogonAccount to verify and rotate the access keys as per the Organization security policy.

e.	Go to IAM policies and click create Policy. Note down the 4 permissions what we require and also on the resource section, we are restricting this policy to be able to perform all these 4 actions against the AWSTSLogonAccount only.

![Permissions4](https://user-images.githubusercontent.com/60601287/128141077-d3c8a336-1d99-47de-b718-f8d4ed58908c.png)

f.	Assign a policy name and in my case, it is named as AWSTSLogonPolicy

![stslogonpolicy](https://user-images.githubusercontent.com/60601287/128141167-2ac8325d-d8ee-4030-a800-a51b3bb9a7f5.png)

g.	Assign the policy created in previous step to AWSSTSLogonAccount

![StsInline](https://user-images.githubusercontent.com/60601287/128141302-8d20a35c-2ac9-4197-be0c-39d1522e551a.PNG)

h.	All steps have been completed on the AWS side and now we will on-board the AWSSTSLogonAccount on Cyberark. We shall be on-boarding this account manually, but it can be on-boarded using automated manner.

i.	Login into Cyberark using the appropriate credentials who shall be authorized to on-board new accounts

j.	Go to Platform Management and enable the Amazon Web Services-AWS-Access keys platform under Cloud Service.

k.	In my case, we will duplicate the AWS-Access Keys platform and name it as an AWS-STS-Access-Logon Account.

![STSPLatform](https://user-images.githubusercontent.com/60601287/128141418-60ceb69a-b4c1-4f12-9868-30ac3e224a76.png)

l.	Create one additional safe and in my case, I have created additional safe named AWSCloud Console STS account and assigned appropriate members.

j.  Add new account. And then select few parameters as mentioned below.

![AWSKeysTable](https://user-images.githubusercontent.com/60601287/128141528-242c04ae-b58c-4f4d-8903-1bf912c11e56.PNG)

k. Once the new account has been added, we will perform 2 steps. i.e. verify and change. Once it’s completed, then we will move to the next step.

![LogonAccountPicture](https://user-images.githubusercontent.com/60601287/128141621-b485f41e-4f29-4524-90e6-9a6ec3f6e323.png)

2.	Creation of  roles in AWS and assigning of those roles within Cyberark 

a.	Create 2 different roles. One is for EC2Administrator access and second one is for S3Full access. 

b.	Here are the steps on how to setup access for EC2Administrator access. Trust that any entity within your account can use this role.

![EC2Adminrole](https://user-images.githubusercontent.com/60601287/128141820-a8a54d71-d53c-4346-8939-a4d0efdae898.PNG)

![Ec2FullAccess](https://user-images.githubusercontent.com/60601287/128141916-5c3a33f9-a2f9-489c-ab20-aee54abbe691.png)

![Ec2Rolepicture](https://user-images.githubusercontent.com/60601287/128142061-4b66e003-e276-44c9-a6be-9608057c547c.PNG)

c.	Below mentioned is how the role should look like for S3Fullaccess

![S3Fullaccess](https://user-images.githubusercontent.com/60601287/128142264-1dde07a1-0235-4535-b628-6d4e6c61c208.PNG)

d.	Once the role assignment has been done, then we will configure the policy so that AWSSTSLogonAccount should be able to assume these 2 roles.

e.	Below mentioned is some of the permissions required and we have to make sure that these permissions being restricted to assume the role defined at earlier steps.

![Capture11](https://user-images.githubusercontent.com/60601287/128142420-f98c92aa-9348-4de3-955c-fdd9a4bcecdf.PNG)

f.	Configuration has been completed on AWS side. Now it’s the time to setup the appropriate configuration on Cyberark.

g.	Logon to the Cyberark again and make sure that Amazon Web Services-AWS platform has been enabled

h.	We can create another safe from best practices perspective and to have better role-based access control. But in my case, I shall leverage upon the same safe as we used before to store AWS STS Logon Account keys.

i.  Add new account. And then select few parameters as mentioned below.

![table1](https://user-images.githubusercontent.com/60601287/128582071-a9d33b9c-3347-43cb-9a55-78d74ffa8d3e.PNG)

j. Similarly add one more account. And then select few parameters as mentioned below.

![table2](https://user-images.githubusercontent.com/60601287/128582107-0844de9f-0ae3-4e4a-9cd9-36a912a38331.PNG)

3.	As a last step, authorized user can simply click on the connect button for the given configured EC2FullAccess or S3FullAccess account.
I.	You will see that there is no password configured or required for the STS access.

![picturecyberark](https://user-images.githubusercontent.com/60601287/128582143-19db19be-8c9d-444a-9cf2-68355563681e.png)

ii. Once you click on connect button then RDP file going to get downloaded. From there, user will be able to access to the AWS Console via Cyberark jumphost. Below mentioned is the screenshot from my setup

![awsconsolepicture2](https://user-images.githubusercontent.com/60601287/128582174-1a3b1ebe-9878-4341-aa50-f4b90dbc9459.png)











