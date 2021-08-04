Cyberark STS Plugin Integration with AWS
In this short step by step guide, we will see how Cyberark STS Plugin can be used to provide secure AWS console access to different group of privilege users.
I believe STS plugin is one of the best approaches what all the customer should leverage upon due to following reasons-
1.	No need to create multiple user identity on AWS IAM
2.	No credentials involved (Cyberark STS plugin involves the use of logon account)
3.	Provide JIT access to any of the given privilege users which will be tied to the granular roles or have specific set of permissions
We have divided the entire configuration into 3 main stages.



