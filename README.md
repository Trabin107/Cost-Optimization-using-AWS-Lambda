# Cost-Optimization-using-AWS-Lambda
COST OPTIMIZATION PROJECT:
## Why do this ?
Ans: There are some EBS volume snapshots which are attached to the EC2 instances. But after the work is done, the developer deleted the EC2 instances but forgot to delete the volume

For this, we will use the aws lambda which is serverless function. Here we write the python code using the boto3. Python boto3 will talk to the aws api for
1.	Accessing all the ebs snapshots
2.	Then filtering out the snapshots

So to begin with, we created a ec2 instance with the attached volume. Then we created a snapshots. Now what happened is that after few months of inactivity we might not need the snapshots so why not delete it for cost optimization. For this we have to write the python code in aws lambda using python boto3. After the code is written, from the configuration we need to adjust the default time to 10 sec from 3 seconds. 
In order to delete the snapshots, aws lambda needs to view and describe the snapshots at first. For this we need to provide it with the necessary permission. For this go to permission and under iam policies add the permission, the default snapshots permission is not available so we have to create a new policy. To create a policy, we have to select the services and search for snapshots, under snapshots we have to select the policy for describing and deleting the snapshots. Now we reload and then attach the snapshot policy. 
Then we also need to describe the volume and ec2 instance so we need to create the new policy.
 
Now if we terminate the ec2 instance manually, the attached volume will be terminated but the snapshots still remains but after we delete the ec2 instance and then go to lambda function to run the code it will delete the attached snapshots. 
In this code we can automate the task by writing the code to run the aws lambda everyday at 10 am and conduct a test that delete the snapshots only if they are more than 30 days old.
