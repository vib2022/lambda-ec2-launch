# lambda-ec2-launch
-create the lambda function. (include the environment variable, like region and other parameters if necessary)
-in lambd fuction general config, increase the timeout time to about 8-10 seconds as 3 seconds might be small for the lambda fuction to trigger and launch the instance.
import boto3

def lambda_handler(event, context):
    ec2 = boto3.client('ec2', region_name='ca-central-1')  # Replace 'your_region' with your desired region

    # Launch EC2 Instance
    response = ec2.run_instances(
        ImageId='ami-0ff573f7b3cc516fc',  # Replace with the desired AMI ID
        InstanceType='t2.micro',  # Replace with the desired instance type
        MinCount=1,
        MaxCount=1,
       # KeyName='JC-key',  # Replace with your key pair name
       # SecurityGroup=['NGINX-sg']  # Replace with your security group name(s)
        #SubnetId='subnet-062e07f76cd51c947'  # Replace with your subnet ID
    )

    return {
        'statusCode': 200,
        'body': response
    }

-create and IAM role with run ec2 instances policy (ec2:Runinstance)
-create a scheduler (at a specific time fofr example ) to act as your trigger for the lambda function
-Test and deploy the lambda script
