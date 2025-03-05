
# Implementing security Groups Overview and NACLs 



> The first step taken was to located my Vpc on AWS amazon.


![VPC](./img/01%20located%20VPC.png)



> I created a VPC by selecting "VPC and more," and named it *My-VPC-1*. I configured it with two subnets (public and private), two route tables (public and private), and one NAT gateway.

![VPC config](./img/02%20VPC%20AND%20MORE%20CREATION%20.png)



> In the subnet, two instant was created (public and private) to host my website.


![instant](./img/3%20instant.png)



> The next step i created 2 Security Group and named it *MyWebaccessSGPublic* and *PrivateSG* attached my VPC that was created at the start of the project to both.


![Public SG](./img/4%20SGP.png)

![Private SG](./img/05%20private%20sg.png)




> In public security group an instant was configure as *inboubnd rule* HTTP-port 80, SSH-port 22 Icmp-IPv4-all.

![SG PUBLIC INBOUND](./img/05%20public%20Sg%20rule.png)



> For the private security group an instant was configure as *inbound rule* HTTP-port 80 , ICMP-IPv4- All and attached with my security that i created priviously for source.


> The next stage is too test the accessibility to the website using the public ip address above.


![public ip](./img/8%20public%20IPv4.png)



> I entered the public IP address into a web browser and through this rute i was a able to access the website 

> Result 

![Ip result](./img/9%20RESULT.png)



# Network ACLs 

> The next stage is create NACLs in other to provide an extra security layer on my security groups, to block or allow traffic.

> I navigate to my search bar on AWS and choose my vpc, inside the VPC i Navigate to the network ACLs in the left bar and click on it create Network ACL


![NACLs creation](./img/%2010%20NACLs%20creation.png)



> i provided a name for my NACLs *My-first-NACL* and choose the VPC i created in the previously session.

![NACLs name](./img/NACL%20NAME.png)


> I associated my public subnet with my NACL in the VPC, NACL are designed to control traffic at the subnet level. wihtout this attachement, the NACL has nothing to protect.

![subnet](./img/12%20subnet.png)



> Although i have permitted all traffic in the inbound rule of our NACL, wi still need to allow all traffic in the outbound rule. 

This is because NACLs are stateless, they do not automatically allow return traffic. Hence i need to explicitly configure rules for both inbound and ourbound rule

![inbound rule](./img/13%20inbound%20rule.png)


![outbound rule](./img/13%20inbound%20rule.png)


> I Successfully configured Security Groups and NACLs to control inbound and outbound traffic in AWS.

> I Learned valuable troubleshooting techniques for diagnosing and resolving network connectivity issues in AWS.

> Overall, gained practical experience and confidence in managing network security within AWS environments.












