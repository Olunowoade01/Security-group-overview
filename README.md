
Implementing security Groups Overview and NACLs


exploring the core concept of the Amazon web service which focuses on Security Group Network Access control list (NACL) I will be using the fundamental component of AWS infrascrture including security group to control the inbound and outboud traffic to EC2 instance also using NACL AS SUBNET LEVEL firewall to requlate the traffic entering and exiting the subnet.


# in my previous project i configure a VPC and in the public subnet an Ec2 instance was lunched and running to host our website.


![EC2 instant](./img/01.%20previous%20EC2%20instant.png)


# The next step is to test accessiblity to the website using the public ip address that was assigned to the instance.


> After entering the ip adress to my chrome browser i recieve error message indicating the page can't be reached.
this is because of the security group that we haven't defined HTTP protocol in the security group so whenever the outside world is trying to go inside our instance and trying to get the data, security group is restricting.

![Error](./img/02%20Error%20.png)




# To resolve this issue i csn create a new security group that alllows ahttp (port 80) traffi.


> I navigate to security group section and click on create security group.

![sg](./img/3.%20create%20new%20SG.png)



> in the next stage i provided a name for my security group, added a discription and ensure to select my VPC during the creation and add rule


![sg name and vpc](./img/04%20sg%20name%20and%20d.png)




> I procced creating my Security group by adding rule to the *inbound rule*
SSH-port 22,  HTTP port-80 and used 0.0.0.0.0/0 as the CIDR.

![SG INBOUND RULE](./img/5%20inbound%20rule%20for%20SG.png)


> I make sure to leave the outband rule as it is, All traffc

![SG outband rule](./img/6%20sg%20outband%20rule.png)


> The security group as been created succesfully and the next stage is to attached it with my instance


![SG successfuly](./img/07%20sg%20successfully.png)


# The next stage is too attached my sucurity group with my instance,

> i navigate to my instance and select the instance then procced to action where i choose security and click on change security groups

![instance attached](./img/08%20instant%20attached.png)



> Next stage i choose the security group i created and click on add security group after chosing my security group, after it was added i procced to click on save 


![instance details](./img/9%20instance%20details.png)




# My instance as been attached successfully with my security group the next stage is to copy my IP address and paste it on my chrome to see if i will able to see data of our website

![IP address](./img/10%20public%20IP%20.png)



>  The ip address  is successfully working 
![ip address](./img/11%20ip%20working.png)




# The next stage is too take a look at how my inbound and outboubd rules are configured


> The inbound rule setup allow the HTTP and SSH protocols to access the instnce.

![inbound rule](./img/12%20inbound%20rule%20.png)



> The outband rule set up permits all traffic to exit the inatnce


![outband rule](./img/outband%20rule.png)


> Through this rule, we're able to access the website 


![Ip address](./img/11%20ip%20working.png)




>  when the outbound rule is removed the website is still accessable because the security group is stateful meaning they automatically allow traffic to return to the instance which they are attached to


![edit outbound](./img/edit%20outbound.png)



> Now that outbound has been removed lets take a look at how it appear in the configuration


![edit outbound](./img/outbound%20removed.png)




# After making this change lets whether we can still access the website succesfully.


![testing](./img/11%20ip%20working.png)

> even though i have removed the outbound rule that allow all traffic from the instance to the outside world, i can still access the website.


> when the inbound rule is removed, enssentially we're closing all access to and from the instance

![inbound edit](./img/inbound%20delete.png)




> The ip address can't acess the website any longer 


![ip address](./img/Ip%20not%20working.png)



# NACL


# Navigate to VPC on aws and click on it


![vpc](./img/vpc.png)




> I procced to create network ACL ON VPC


![network acl](./img/create%20network%20acl.png)




> I provided a name for my network ACL and ensure to choose my VPC that i created in the previous session


![NACL details](./img/Create%20Nacl.png)



# After creating my Networl ACl i navigate to the inbound section and notice that it's denying all traffic fron port.



![ACL traffic](./img/NACL%20profile%20deny.png)





> similarly on outbound section the traffic was denying


![NACL outbound](./img/acl%20outband%20deny.png)




> After noticing that the traffic as been denying on both section we need to maken changes on both and allow all traffic

> first i navigate to my inbound section and click on edit inbound.

![edit ACL INBOUND](./img/ACL%20edit%20inbound.png)


> The next stage is to click on add rule, i choose (1)for the rule number, All traffic was allow and 0.0.0.0/0 for the source 


![inbound rule](./img/Acl%20ALLOW%20TRAFFIC.png)



# After allowing traffic with NACL, Currently, the NACL is not associated with any of the subnet.

![subnet](./img/associate%20with%20subnet.png)



> Next step is too associate the NACL with the subnet, by selecting my NACL  click on action to edit the subnet association


![edit subnet](./img/edit%20subnet%20acl.png)


> After selecting my public subnet and and click on save 
> NACL is succefully associated with the  subnet.


![subnet](./img/subnet%20associate.png)


> I followed the same procces to edit my outband rule by allowing traffi

![nacl outbound](./img/acl%20edit%20outbound%20.png)


> On outbound traffic i choose (1)for the rule number, All traffic was allow and 0.0.0.0/0 for the source

![outbound](./img/outbound%20edit%20traffic.png)







# Project reflection 

> overall gained pratical exprience and confidence in nmanaging network security within AWS environments

> explored various scenarios to undestand how security Groups and NACLs interact



















