
Implementing security Groups Overview and NACLs


exploring the core concept of the Amazon web service which focuses on Security Group Network Access control list (NACL) I will be using the fundamental component of AWS infrascrture including security group to control the inbound and outboud traffic to EC2 instance also using NACL AS SUBNET LEVEL firewall to requlate the traffic entering and exiting the subnet.


# In the public subnet, we've created an EC2 instance that is running hosting our website.


![1](./img/01.%20previous%20EC2%20instant.png)


> Now let's take a moment to see if we can access the website using the public IP address





#  After entering the IP address into your Chrome browser and hitting enter, I noticed that the page doesn't load. It keeps attempting to connect and eventually shows a message saying that the site can't be reached.

![2](./img/02%20Error%20.png)

> This issue is likely due to the security group configuration. Since the HTTP protocol hasn't been defined in the security group, it is blocking incoming traffic from the outside world. As a result, when trying to access the instance to retrieve the website data, the security group restricts the connection, preventing me from seeing the website content.




# To resolve this issue, we can create a new security group that allows HTTP (Port 80) traffic.


> First, I navigate to the Security Groups section in AWS and click on Create Security Group. This will allow us to set up a new security group with the necessary rules to allow HTTP traffic.

![sg](./img/3.%20create%20new%20SG.png)



# In the next stage i provided a name for my security group, added a discription and ensure to select my VPC during the creation.


![sg name and vpc](./img/04%20sg%20name%20and%20d.png)




# I procced creating my Security group by adding rule to the *inbound rule*
# SSH-port 22,  HTTP port-80 and used 0.0.0.0.0/0 as the CIDR.

![SG INBOUND RULE](./img/5%20inbound%20rule%20for%20SG.png)


# I ensure sure to leave the outband rule as it is, All traffc

![SG outband rule](./img/6%20sg%20outband%20rule.png)


# The security group as been created succesfully and the next stage is to attached it with my instance


![SG successfuly](./img/07%20sg%20successfully.png)


# The next stage is too attached my sucurity group with my instance,

> I navigated to my instance, selected it, then proceeded to the "Actions" menu. From there, I chose "Security Groups" and clicked on "Change Security Groups."

![instance attached](./img/08%20instant%20attached.png)



# Next stage i choose the security group that i have already been created and click on add security group after chosing my security group, and it was added i procced to click on save 


![instance details](./img/9%20instance%20details.png)




# Now that my instance is properly attached to the security group, the next step is to copy the public IP address and paste it into my Chrome browser to check if the website data is being served

![IP address](./img/10%20public%20IP%20.png)



# The IP address is successfully working, and my website is now accessible through the public IP.

![ip address](./img/11%20ip%20working.png)


> This means the security group is configured correctly, and the inbound rules (HTTP and SSH) are allowing the necessary traffic to reach the instance. 




# After confirming that your IP address is working successfully, i have proceeded to the next step of checking how the inbound and outbound rules are configured.


> With these rules, my instance is accessible over the web via HTTP, and i can also connect to it remotely using SSH.

![inbound rule](./img/12%20inbound%20rule%20.png)



# The outband rule set up permits all traffic to exit the inatnce


![outband rule](./img/outband%20rule.png)


# Through this rule, we're able to access the website 


![Ip address](./img/11%20ip%20working.png)



# Even when the outbound rule is removed, the website is still accessible because security groups in AWS are stateful. This means they automatically allow the return traffic to reach the instance, regardless of the outbound rule. As a result, once the inbound traffic is allowed, the response can flow back to the requester without any issues.

![edit outbound](./img/edit%20outbound.png)



# Since AWS security groups are stateful, even with no outbound rules, the response traffic (like the data returned to an HTTP request) will be allowed automatically.

![edit outbound](./img/outbound%20removed.png)




# Even though we've removed the outbound rule that allows all traffic from the instance to the outside world, we can still access the website successfully. This behavior is due to the stateful nature of AWS security groups.


![testing](./img/11%20ip%20working.png)

> So, it confirms that the stateful nature of security groups allows the website to remain accessible


# When the inbound rule is removed, you're essentially closing all access to and from the instance, which blocks any incoming traffic to the website. This means that no external IP address or user will be able to access the website hosted on the instance anymore.

![inbound edit](./img/inbound%20delete.png)




# As shown in the screenshot, after removing the inbound rule, the IP address can no longer reach the website. This is because there are no rules allowing the traffic to reach the instance, effectively making the instance unreachable from the outside world.


![ip address](./img/Ip%20not%20working.png)



# NACL


# I navigate to the VPC section on AWS and click on it.


![vpc](./img/vpc.png)




# Next, I proceed to create a Network ACL within the VPC to manage the network traffic more effectively.


![network acl](./img/create%20network%20acl.png)




# I provided a name for my Network ACL and made sure to select the VPC I created in the previous session.


![NACL details](./img/Create%20Nacl.png)



# After creating the Network ACL, I navigated to the Inbound section and noticed that it's currently denying all traffic, including traffic from port 80.



![ACL traffic](./img/NACL%20profile%20deny.png)





# Similarly, in the Outbound section, I noticed that the traffic is also being denied. This means that the instance cannot send any traffic out of the VPC, which could affect the response to external requests, such as returning data for the website.


![NACL outbound](./img/acl%20outband%20deny.png)


> This means that the Network ACL is blocking incoming traffic, which is why the website isn't accessible. To resolve this, we need to update the inbound rules to allow the necessary traffic, such as HTTP (Port 80), so the website can be reached successfully.




# After noticing that the traffic is being denied in both the Inbound and Outbound sections, we need to make changes in both and allow all traffic.

> # I navigate to the Inbound section and click on Edit Inbound to modify the rules.

![edit ACL INBOUND](./img/ACL%20edit%20inbound.png)


 > I click on Add Rule, then set the following configuration:

> Rule number: 1
> Type: All traffic
> Source: 0.0.0.0/0 (this allows traffic from all IP addresses)


![inbound rule](./img/Acl%20ALLOW%20TRAFFIC.png)

> This setup will allow all inbound traffic to reach the instance, including HTTP traffic on port 80, which is necessary for the website to be accessible.



# After allowing traffic with the Network ACL (NACL), I noticed that the NACL is not yet associated with any of the subnets.

![subnet](./img/associate%20with%20subnet.png)



# To associate the NACL with the subnet, I select my NACL, click on Actions, and then choose Edit Subnet Association.

> This will allow me to associate the NACL with the appropriate subnet(s), ensuring that the rules apply to the traffic in those subnets and allowing the website to be properly accessible.


![edit subnet](./img/edit%20subnet%20acl.png)


# After selecting my public subnet and clicking on Save, the NACL is successfully associated with the subnet.



![subnet](./img/subnet%20associate.png)


# I followed the same process to edit my Outbound rule by allowing traffic.

![nacl outbound](./img/acl%20edit%20outbound%20.png)


> I navigate to the Outbound section and click on Edit Outbound to modify the rules.

> I add the following configuration:

Rule number: 1
Type: All traffic
Destination: 0.0.0.0/0 (this allows traffic to any destination)

![outbound](./img/outbound%20edit%20traffic.png)

> This ensures that outbound traffic is allowed, and the instance can send traffic back out, including HTTP responses, which is necessary for the website to function properly.







# Project reflection 

> overall gained pratical exprience and confidence in nmanaging network security within AWS environments

> explored various scenarios to undestand how security Groups and NACLs interact



















