# Three-Tier-Architecture
Built an AWS Project on Three Tier Architecture Concept
---

Building a Resilient Three-Tier Architecture on AWS
Architectural Diagram :

---

AWS offers extensive assets to fabricate and keep up with your cloud applications. These assets can be arranged to cooperate to make profoundly accessible, exceptionally solid cloud structures. The situation we will utilize is that you have been approached to plan and make a profoundly accessible 3 level design for your organisation's new web application.
What is a Three Tier Architecture
A Three Tier Architecture consists of :-
Presentation Tier, Application Tier, Data Tier.
The Presentation Tier is the user Interface, such as the website that a user or client navigates to. It can also be thought of as the "Front End."
The Application Tier is where data is processed and is often called the "Back End."
The Data Tier is where data is Stored and Managed.
Benefits of a Three Tier Architecture
Decreased development time - It allows different teams to work simultaneously on different Tiers, resulting in a Faster Deployment Process.
Increased scalability - A Tier can have an Auto-Scaling Group independent of other Tiers, meaning for each Tier, you only use what you need.
Increased reliability - Each Tier can have multiple resources in multiple availability zones and the success and availability of one tier is independent of the other tiers.
Increased security - Each Tier can have its own security group, allowing for custom Permissions depending on the needs of that Tier.

---

Created a VPC
After looking at the architecture diagram, I see that we need to create 1 VPC, 2 public subnets, and 4 private subnets. After successfully logged into the AWS console, I navigated to the VPC resource. Clicked "Create VPC" and I got two options: "VPC only" or "VPC and more."
Because I am creating a VPC with Multiple subnets, Availability zones, and more, I choosed "VPC and more."
When creating the VPC, I used the following input:
IPv4 CIDR block: 10.0.0.0/16
Tenancy: Default
Availability zones: 2
Number of public subnets: 2
Number of private subnets: 4
NAT gateways: In 1 AZ
(there is a fee for this, so delete it when I am done)
VPC endpoints: None
Enable DNS hostnames: check
Enable DNS resolutions: check
The first item to build is a VPC. It will house all the other components therefore choosing which location hosts your VPC will be quite important with regards to:
Costs
Availability of services
Proximity to the end users

On the dashboard, I navigated to VPC and followed the prompts as below:
In the AWS Console Panel, I simply Searched for VPC and opened VPC service (I have selected "N.California" Region).

2. Then I clicked on "Create VPC" option on the top left corner and started with the configuration of my VPC.
3. I have given a name to VPC as "Three-Tier-Application-VPC" and selected the given radio button as "IPv4 CIDR manual input" by allocating it IP as "10.0.0.0/16".
4. I have kept "Tenance" as "Default" and Clicked on "Create VPC" and I have successfully created VPC.
Creating Subnets
5. In the left panel, I clicked on "Subnets" then "Create Subnet".
6. I have selected VPC, I have created names as "Three-Tier-Application-VPC".
7. First Subnet as "Web-Server-Subnet-1" allocated AZ as "us-west-1a" with IPV4 CIDR block "10.0.0.0/20".
8. Second Subnet as "Web-Server-Subnet-2" allocated AZ as "us-west-1c" with IPV4 CIDR block "10.0.16.0/20".
9. Third Subnet as "Application-Server-Private-Subnet-1" allocated AZ as "us-west-1a" with IPV4 CIDR block "10.0.128.0/20".
10. Fourth Subnet as "Application-Server-Private-Subnet-2" allocated AZ as "us-west-1c" with IPV4 CIDR block "10.0.144.0/20".
11. Fifth Subnet as "Database-Server-Private-Subnet-1" allocated AZ as "us-west-1a" with IPV4 CIDR block "10.0.160.0/20".
12. Sixth Subnet as "Database-Server-Private-Subnet-2" allocated AZ as "us-west-1c" with IPV4 CIDR block "10.0.176.0/20".
13. Then I clicked on Create Subnets & I have successfully Created Subnets.
Creating Internet Gateway
14. On the left side I clicked on "Internet Gateways" and clicked on "Create Internet Gateway" & I have given IG name as "Three-Tier-IG" and Attached to the VPC.
Created NAT Gateway
15. On the left side I clicked on "NAT Gateways" then "Create NAT Gateway".
16. I have given name as "Web-Server-NG" and set connectivity type as Public and clicked on Create NAT gateway & this way I have successfully created NAT gateway.
Created Route Tables
17. On the left side I clicked on "Route Tables" then "Create Route Table".
18. First Route Table, I have given name as "Public-Route Table" and selected the VPC and Clicked on "Create Route Table" & Now, I have Successfully Created "Public-Route-Table".
19. Again, I created Second Route Table, I have given name as "Private-Route Table" and selected the VPC and Clicked on "Create Route Table" & Now, I have Successfully Created "Private-Route-Table".
20. Now, to associate Subnets according to the Private and Public Subnets, I select "Public-Route-Table" then "Subnet Association".
21. In the "Explicit Subnet Associations" I clicked on "Edit Subnet Associations" to associate "Public Subnets".
22. I have selected "Web-Server-Public-Subnet-2" and Clicked on "Save Associations".
23. I select "Private-Route-Table" then "Subnet Association".
24. In the "Explicit Subnet Associations" I clicked on "Edit Subnet Associations" to associate "Private Subnets" then I have selected all the subnets, except "Web-Server-Public-Subnet-2" and Clicked on "Save Associations".
25. Now, In the Subnets Section, I select one Subnet then I clicked on "Actions" & "Edit Subnet Settings".
26. And I Checked in for the option as "Auto-Assign".
27. I did this for all 6 Subnets.
Created a Web Server Tier -Presentation Tier
Launched An Instance
28. To enable the Auto scaling group, and to create similar instances, I need to create a launch template that it will use as a blue print.
29. I have searched for EC-2 and below is how I created my "EC-2 Launch Template".
30. This is how, I have created Launch Template for an Application Tier.
Launching An Auto Scaling Group
Created an Application Layer - App Tier
31. AutoScaling Group
32. Used Cloud Watch To Enable Monitoring (It's not in the Diagram).
33. Enabled SNS alerts for custom warnings (It's not in the Diagram).
34. This was the Final Template Looked alike.
35. After successfully launched the Auto scaling group , after a few minutes it created the desired resources as shown:
36. I followed a similar process to create the Launch template for the Application tier:
37. I finished off via a similar process to create the Autoscaling group for the Application tier:
38. Finally I have finished off with the Database tier.
Data Layer - Database Tier
A good database choice affects data availability, read/write speed, the amount of load the database can endure in peak conditions, and most importantly, a good database choice gives you great value for your money.
39. Eureka, Implementation of Three Tier Application Layer successful!
As a final step, it is advisable to connect to web, application and database servers to confirm that their access is as per your requirements.
Conclusion :
As shown in the Architectural Diagram, I have created a highly available, resilient, reliable, and secure architecture. The remaining steps will transform this project from a learning environment to a production application.
![image](https://github.com/girhs/Three-Tier-Architecture/assets/93239323/59dc0759-5191-476c-854b-59f423b9ee38)
