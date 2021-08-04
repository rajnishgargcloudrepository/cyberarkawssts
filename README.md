Cyberark STS Plugin Integration with AWS
In this short step by step guide, we will see how Cyberark STS Plugin can be used to provide secure AWS console access to different group of privilege users.
I believe STS plugin is one of the best approaches what all the customer should leverage upon due to following reasons-
1.	No need to create multiple user identity on AWS IAM
2.	No credentials involved (Cyberark STS plugin involves the use of logon account)
3.	Provide JIT access to any of the given privilege users which will be tied to the granular roles or have specific set of permissions
We have divided the entire configuration into 3 main stages.
1.	Creation and On-Boarding of the STS logon account
a.	Go to AWS IAM Service and then click on to add new user
 

b.	Proceed without assigning any policy or permissions.
 
c.	Click on create user and note down the User, Access key ID and Secret Access Key.
 
d.	We will create new policy where we will assign enough permission to the AWSSTSLogonAccount to verify and rotate the access keys as per the Organization security policy.
e.	Go to IAM policies and click create Policy. Note down the 4 permissions what we require and also on the resource section, we are restricting this policy to be able to perform all these 4 actions against the AWSTSLogonAccount only.

 

f.	Assign a policy name and in my case, it is named as AWSTSLogonPolicy
 
g.	Assign the policy created in previous step to AWSSTSLogonAccount
  

h.	All steps have been completed on the AWS side and now we will on-board the AWSSTSLogonAccount on Cyberark. We shall be on-boarding this account manually, but it can be on-boarded using automated manner.
i.	Login into Cyberark using the appropriate credentials who shall be authorized to on-board new accounts
j.	Go to Platform Management and enable the Amazon Web Services-AWS-Access keys platform under Cloud Service.
k.	In my case, we will duplicate the AWS-Access Keys platform and name it as an AWS-STS-Access-Logon Account.
 

l.	Create one additional safe and in my case, I have created additional safe named AWSCloud Console STS account and assigned appropriate members.
j.  Add new account. And then select few parameters as mentioned below.
S.No.		
1.		System Type	Cloud
2.		Select Platform 	AWS-STS-Access-Logon
3.		Select Safe	AWS Cloud Console STS Account
4.		IAM Username 	AWSSTSLogonAccount
5.		AWS Access Key Secret	XXXX (You have noted down this while configuring new user on AWS)
6.		AWS Access Key ID	XXXX (You have noted down this while configuring new user on AWS)
7.		AWS Account Number	Key in your AWS Account number
8.		AWS Account Alias	AWS STS Logon Account (You can choose anything)
 
k. Once the new account has been added, we will perform 2 steps. i.e. verify and change. Once it’s completed, then we will move to the next step.
 

2.	Creation of  roles in AWS and assigning of those roles within Cyberark 
a.	Create 2 different roles. One is for EC2Administrator access and second one is for S3Full access. 
b.	Here are the steps on how to setup access for EC2Administrator access. Trust that any entity within your account can use this role.
 

 

 


c.	Below mentioned is how the role should look like for S3Fullaccess
 

d.	Once the role assignment has been done, then we will configure the policy so that AWSSTSLogonAccount should be able to assume these 2 roles.
e.	Below mentioned is some of the permissions required and we have to make sure that these permissions being restricted to assume the role defined at earlier steps.
 
f.	Configuration has been completed on AWS side. Now it’s the time to setup the appropriate configuration on Cyberark.
g.	Logon to the Cyberark again and make sure that Amazon Web Services-AWS platform has been enabled
h.	We can create another safe from best practices perspective and to have better role-based access control. But in my case, I shall leverage upon the same safe as we used before to store AWS STS Logon Account keys.
i.  Add new account. And then select few parameters as mentioned below.
S.No.	Parameters	Settings
1.		System Type	Cloud
2.		Select Platform 	Amazon Web Services-AWS
3.		Select Safe	AWS Cloud Console STS Account
4.		IAM Username 	EC2Fullaccess (Can be anything)
5.		AWS Role	arn:aws:iam::19XXXX:role/AWSEC2fullaccessSTS (This is how it should look like)
6.		AWS Account Number	Key in your AWS Account number
7.		AWS Account Alias	EC2 FullAccess (You can choose anything)
8.		Associate Logon Account	AWS STS Logon Account (Created in Step 1)

j. Similarly add one more account. And then select few parameters as mentioned below.
S.No.	Parameters	Settings
1.		System Type	Cloud
2.		Select Platform 	Amazon Web Services-AWS
3.		Select Safe	AWS Cloud Console STS Account
4.		IAM Username 	S3Fullaccess (Can be anything)
5.		AWS Role	arn:aws:iam::19XXXX:role/AWSS3fullaccessSTS (This is how it should look like)
6.		AWS Account Number	Key in your AWS Account number
7.		AWS Account Alias	S3 FullAccess (You can choose anything)
8.		Associate Logon Account	AWS STS Logon Account (Created in Step 1)

3.	As a last step, authorized user can simply click on the connect button for the given configured EC2FullAccess or S3FullAccess account.
I.	You will see that there is no password configured or required for the STS access.
 

ii. Once you click on connect button then RDP file going to get downloaded. From there, user will be able to access to the AWS Console via Cyberark jumphost. Below mentioned is the screenshot from my setup
 

