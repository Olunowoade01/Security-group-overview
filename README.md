
#  The process is too understand the concepts of security group and NACLs in AWS

> The first step taken was to create a security group allowing HTTP for all traffic and i attached it to the instance.

> In the public subnet, an EC2 instance was created to the webiste.

![Ec2 instant](./img/1.%20EC2%20instance.png)

> After creating an Ec2 instant, I created a security group and attached with the Vpc that was created at the start of the project.


> The security group for this instance was configured as * Inbound rules and Allow - SSH - port 22, HTTP - port 80,  ICMP-IPv4 - All

![Sg inbound ](./img/2.%20Inbound%20rules.png)

> For the *outbound rules*, i configured all IPv4 traffic with any protocol on any port number to be  allowed, meaning this insatnce has unrestricted access to anywhere on the internet.

![SG-outbound](./img/3.%20Outbound%20rules.png)

> The next step i copy my  public ip to test on chrome browser to ensure it's working 

> TESTING

![Public IP](./img/4.%20public%20IPv4.png)

> Lets test accessibility to the website using the public IP address above.

> RESULT 

![Result](./img/5.%20rESULT.png)

> I entered the public address into a web browser, and through this public ip i'm able to access the website.

# Network ACLs

>  Network ACL was created under the security option on the VPC page. NACLs is names *my-first-NACLs, and our VPC is attached to the netwrok ACL.


>   the next step is to navigate to the inbound and outbound rules to check if all traffic has been denied.

> By default all traffic from all ports have been denied. This will be the same for the outnound and inbound rule.

> i make changes on both inbound rule and outbound rule and add new rule, configure as All traffic, source 0.0.0.0/0, Allow 

image bellow show the result after 

![NACLs](./img/7.%20cteate%20NACLs.png)


> This NACL was also assocociated with the public subnet in the VPC.


![SUNNET-NACLs](./img/9.%20subnet%20associated.png)

> Although i have permitted all traffic in the inbound rule of our NACL, we still need to allow all traffic in the outbound rule. 

> This is because NACLs are stateless, they do not automatically allow return traffic. Hence we need to explicitly configure rules for both inbound and ourbound rule. 

![OUTBOUND-NACLs](./img/8.%20outband%20rule%20NACLs.png)

> RESULT

![Result](./img/5.%20rESULT.png)

> Project Reflection 

- I successfully configured Security Groups and NACLs to manage inbound and outbound traffic in AWS


- Overall, I gained practical experience and confidence in managing network security within AWS environments.