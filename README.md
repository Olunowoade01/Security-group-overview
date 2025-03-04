
# Implementing Inbound Traffic Rules for HTTP and SSH Protocol.

> The first step taken was to create a VPC and configure 2 subnets (Public & private subnet) in it.

> In the public subnet, an instance was created to host our website.

![Ec2 instant](./img/1.%20EC2%20instance.png)

> I created a security group and nammed it *My-public-SG*, attaching the Vpc that was created at the start of the project.


> The security group for this instance was configured as *Inbound rules* - SSH - port 22, HTTP - port 80,  ICMP-IPv4 - All

![Sg inbound ](./img/2.%20Inbound%20rules.png)

> For the *outbound rules*, i have configured all IPv4 traffic with any protocol on any port number is allowed, meaning this insatnce has unrestricted access to anywhere on the internet.

![SG-outbound](./img/3.%20Outbound%20rules.png)

> TESTING

![Public IP](./img/4.%20public%20IPv4.png)

> Lets test accessibility to the website using the public IP address above.

> RESULT 

![Result](./img/5.%20rESULT.png)

> I entered the public address into a web browser, and through this rule we're able to access the website.

# Network ACLs

> Network ACL was created under the security option on the VPC page. NACLs is names *my-first-NACLs, and our VPC is attached to the netwrok ACL.

> By default all traffic from all ports have been denied. This will be the same for the outnound and inbound rule.

> To make chnages, edit inbound rule, add new rule, configure as *All traffic, source 0.0.0.0/0, Allow*. 

see image below.

![NACLs](./img/7.%20cteate%20NACLs.png)


> This NACL was also assocociated with the public subnet in the VPC.

![SUNNET-NACLs](./img/9.%20subnet%20associated.png)

> Although we have permitted all traffic in the inbound rule of our NACL, we still need to allow all traffic in the outbound rule. 

> This is because NACLs are stateless, they do not automatically allow return traffic. Hence we need to explicitly configure rules for both inbound and ourbound rule. 

![OUTBOUND-NACLs](./img/8.%20outband%20rule%20NACLs.png)

> RESULT

![Result](./img/5.%20rESULT.png)

> Project Reflection 

- I successfully configured Security Groups and NACLs to manage inbound and outbound traffic in AWS

- I learned valuable troubleshooting techniques for diagnosing and resolving network connectivity issues in AWS.

- Overall, I gained practical experience and confidence in managing network security within AWS environments.