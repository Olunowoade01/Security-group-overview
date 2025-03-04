
 ##  Establishing Inbound Traffic Rules for HTTP and SSH Protocols.

The initial step involved creating a VPC and setting up two subnets (public and private) within it.

In the public subnet, an instance was created to host our website.

![EC2](./img/1.%20EC2%20instance.png)

# I created a security group named My-public-SG and associated it with the VPC that was set up at the beginning of the project.


# The security group for this instance was configured as *Inbound rules* - SSH - port 22, HTTP - port 80,  ICMP-IPv4 - All

![SG-inbound](./img/2.%20Inbound%20rules.png)

> The security group for this instance was configured with the following inbound rules: SSH on port 22, HTTP on port 80, and ICMP-IPv4 set to allow all.

![SG-outbound](./img/3.%20Outbound%20rules.png)

> TESTING

![Public IP](./img/4.%20public%20IPv4.png)

> Let's test the accessibility of the website using the public IP address provided above.

> RESULT 

![Result](./img/5.%20rESULT.png)

I entered the public IP address into a web browser, and through this method, we were able to access the website.

# Network ACLs

> A Network ACL was created under the security section on the VPC page. The NACL is named my-first-NACL, and our VPC is associated with this network ACL.


>By default, all traffic from all ports is denied, including both inbound and outbound rules.

To make changes, edit the inbound rule, add a new rule, and configure it as All traffic, source 0.0.0.0/0, Allow.

see image below.

![NACLs](./img/7.%20cteate%20NACLs.png)


## This NACL was also associated with the public subnet in the VPC.

![SUNNET-NACLs](./img/9.%20subnet%20associated.png)

> Although we have allowed all traffic in the inbound rule of our NACL, we also need to permit all traffic in the outbound rule. 

> TThis is because NACLs are stateless and do not automatically allow return traffic. Therefore, we need to explicitly configure rules for both inbound and outbound traffic. 

![OUTBOUND-NACLs](./img/8.%20outband%20rule%20NACLs.png)

> RESULT

![Result](./img/5.%20rESULT.png)

> Project Reflection 

