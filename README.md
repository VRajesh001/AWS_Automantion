# AWS Automation
----------
 Task 1
----------

**Ansible role for the below code challenge**

**Task 1**: Automate the EC2 instance creation under load balancer.

1. Create a VPC with should have a public and private subnet

2. Create a role with s3 access.

3. Launch an ec2 instance with the role created in step 1, inside the private subnet of VPC, and install apache through bootstrapping. ( You need to have your NAT gateway attached to your private subnet )

4. Create a load balancer in public subnet.

5. Add the ec2 instance, under the load balancer

# Note

Add variable in the file inside vars folder as per requirement.

----------
 Task 2
----------

**Task 2**

 - Automate the process of stop (For cost saving)

Automate the process of stop to a group of EC2 instances (based on tags). Ensure that there is no user logged into the servers, and CPU usage is idle ( less than 10% ) for the particular period of time before stopping. The idle period and tag will be passed as arguments.

    usage: autostop <Tag name> < idle period>

For example:

    autostop <development> 60

If the current time is 6 PM, the script needs to check the idle development instances in the last 60 minutes ( 5 PM to 6 PM ) and make sure no users are logged into those instances before stopping them. Don’t set up permanent cloudwatch alarm to stop the instances. The script needs to run on-demand for stopping the instances.

----------
 Task 3
----------

**Task 3**

1. Create an auto scaling group with minimum size of 1 and maximum size of 3 with load balancer created in step 3 of Task 1.

2. Add the created instances under the auto scaling group. ( You need to have an AMI created out of previously created instance in Task 1 which has apache installed in it)

3. Write a life cycle policy with the following parameters:

scale in : CPU utilization > 80%

scale out : CPU Utilization < 60%

----------
 Task 4
----------

**Task 4**

Automate the process of granting / revoking SSH access to a group of servers instances to a new developer. Please provide your solution by uploading your code in any of the code repository.

# To add a new user and grant user SSH access
ansible-playbook -i inv -e "action=grant" ssh.yml

# To grant SSH access to an existing user (skip adding the user part)
ansible-playbook -i inv -e "action=grant" ssh.yml --skip-tags=add

# To revoke SSH access from an existing user (skip removing the user part)
ansible-playbook -i inv -e "action=revoke" ssh.yml --skip-tags=remove

# To remove user, and thereby revoking the SSH access as well
ansible-playbook -i inv -e "action=revoke" ssh.yml

# Note

1. Please make sure to add IPs or DNS of target servers in inv file.
2. Update the variable "user_name" and "user_des" in inv file.
3. Create a directory under "keys" directory having the same name as "user_name" and put its SSH public key in it.