**Reading: Cloud Computing Solutions Architect: A Hands-On Approach, by Arshdeep Bahga**

**Pages: 79-80**

**Task: Build a Python program for launching an EC2 instance**

**Python Template: launch_ec2.py**

**Steps**
1. Create a valid security group for your EC2 instance. Set up the SG in the same region you will use in the launch_ec2.py template.
2. Open the template in Visual Studio Code and insert values for the following:
    -AWS_KEY
    -AWS_SECRET
    -EC2_KEY_HANDLE
    -SECGROUP_ID
    *Note: AMI Ids are unique to each region. If you want to change the region or AMI, read this for more information. https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html
3.  Save the template
4. Open a terminal and navigate to the directory your template is saved to.
5. Type: python3.13 launch_ec2.py
   *Note: use python3.12 or your specific version if needed.
6. The script should run and your EC2 should launch. Confirm in the AWS console.

Tear Down Instructions
1. Click "Instances" on the left hand menu
2. Click the selection box next to your instance.
3. Click the "Instance State" dropdown menu and select "Terminate Instance"
4. Delete the EC2 security group (optional)

# Note: The script in the book returns a KeyError in the "while status == 'pending' loop."
   ```python
while status == 'pending':
sleep(10)
response = ec2.describe_instance_status(InstanceIds=[Instance_ID])
status = response['Reservations'][0]['Instances'][0]['State']['Name']
```

**The KeyError came from using the wrong response syntax.**

- The code mixes up describe_instance_status with the indexing pattern for describe_instances.
- describe_instance_status returns 'InstanceStatuses' not 'Reservations'.
- describe_instances returns 'Reservations'.

**For more information, study the resources below**

- https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ec2/client/describe_instances.html
- https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ec2/client/describe_instance_status.html
