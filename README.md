
# Implementing security Groups Overview and NACLs 


> exploring the core concept of the Amazon web service  which focuses on Security Group Network Access control list (NACL) I will be using the fundamental component of AWS infrascrture including security group to control the inbound and outboud traffic to EC2 instance also using NACL AS SUBNET LEVEL firewall to requlate the traffic entering and exiting the subnet.



# creating an EC2 instant (public and private) to host my website.



![EC2 instant](./img/3%20instant.png)


## After launching an EC2 instance, I decided to test it in my web browser by copying the IP address (18.134.151.126). However, when I entered the IP address into my Chrome browser, I received an error message stating that the site couldn't be reached.


![error facing](./img/EC2%20error.png)

> This is due to the security settings not allowing the HTTP protocol in the security group. As a result, when external requests attempt to access the instance and retrieve data, the security settings block the connection.



# To resolve this issue  i created 2 Security Group that allows HTTP (PORT 80) and named it *MyWebaccessSGPublic* and *PrivateSG* attached my VPC that was created at the start of the project to both.


![Public SG](./img/4%20SGP.png)

![Private SG](./img/05%20private%20sg.png)



# In the public security group, the instance was configured with the following inbound rules: HTTP (port 80), SSH (port 22), and ICMP (IPv4 - all).

![SG PUBLIC INBOUND](./img/05%20public%20Sg%20rule.png)



## In the private security group, the instance was configured with the following inbound rules: HTTP (port 80), ICMP (IPv4 - all), and it was associated with the security group I previously created as the source.



> After successfully creating my public and private security groups, the next step is to attach the public security group to my instance.

# I navigate to the "Instances" section, select the instance I previously created, click on "Security" in the "Actions" section, and then proceed to choose "Change Security Group."



![instance attached](./img/instance%20attached%20.png)



# After selecting the security group I created, it was automatically attached to my instance.


![SG added](./img/added%20sg.png)




# The next step is to test the website's accessibility using the public IP address mentioned above.

![public ip](./img/8%20public%20IPv4.png)



# I entered the public IP address into a web browser, and through this route, I was able to access the website.

> Result 

![Ip result](./img/9%20RESULT.png)



# Network ACLs 

> The next step is to create NACLs to add an extra layer of security to my security groups, allowing or blocking traffic.

## I go to the search bar in AWS and select my VPC. Inside the VPC, I navigate to "Network ACLs" in the left sidebar and click on it to create a new Network ACL.

![NACLs creation](./img/%2010%20NACLs%20creation.png)



# I provided a name for my NACL, *My-first-NACL*, and selected the VPC I created in the previous session.

![NACLs name](./img/NACL%20NAME.png)


#  I associated my public subnet with the NACL in the VPC. NACLs are designed to control traffic at the subnet level, and without this attachment, the NACL would have no traffic to protect.

![subnet](./img/12%20subnet.png)



# Although I have allowed all traffic in the inbound rule of my NACL, I still need to permit all traffic in the outbound rule as well. 

> This is because NACLs are stateless, meaning they do not automatically allow return traffic. Therefore, I must explicitly configure rules for both inbound and outbound traffic.

![inbound rule](./img/13%20inbound%20rule.png)


![outbound rule](./img/13%20inbound%20rule.png)


# I Successfully configured Security Groups and NACLs to control inbound and outbound traffic in AWS.

# I Learned valuable troubleshooting techniques for diagnosing and resolving network connectivity issues in AWS.

# Overall, gained practical experience and confidence in managing network security within AWS environments.












