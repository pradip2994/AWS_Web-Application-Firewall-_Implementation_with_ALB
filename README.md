# Implementing AWS WAF with ALB to Safeguard Against SQL Injection, Geo Location, and Query String Threats.
![image](https://github.com/user-attachments/assets/275d1961-fc1c-4c0f-871b-8d79584b58f4)


## Instance
### Create Two EC2 Instances in default VPC with Auto-assign public IP enabled, Security Group: allow HTTPS, HTTP, and SSH, Advanced details: Provide EC2 user data mention below.
```
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from Server-1</h1>" > /var/www/html/index.html
```
![image](https://github.com/user-attachments/assets/c091d9b0-b262-4d18-a806-79cc6c775c11)


## Create Target Groups, Register target (Instance)

![image](https://github.com/user-attachments/assets/011cf4ce-7ab6-47e8-aaee-31d82cc2aaa3)


## Load Balancer
### Create Application Load Balancer and add Target Group.

![image](https://github.com/user-attachments/assets/bb14352a-9c81-47b8-8de4-ed9a463ad62d)


## AWS WAF (Web Application Firewall)
### Define Web ACLs Rules.
### Select the Region in which Application Load Balancer is deployed.
![image](https://github.com/user-attachments/assets/01a600b3-a96e-423e-942b-0512ef5c9241)


### Describe web ACL and associate it to AWS resources.
![image](https://github.com/user-attachments/assets/907c9df8-70a1-4eac-9fd3-7bc63ea78fbe)


### Add rules and rule groups.
Select from Add Rules **Add my own rules and rule groups**
![image](https://github.com/user-attachments/assets/4b715cb1-f841-4370-a202-7202ed007af4)


Now select **Rule builder**.
![image](https://github.com/user-attachments/assets/b4ea6a7f-800a-44f3-b54b-405df93f3899)

### Web ACL Rule for Geo Location.
If a request doesn't match the statement then it will **Block** the request.
![image](https://github.com/user-attachments/assets/46448d88-37c0-4dd1-b0e7-63a51cfb6d3e)


### Web ACL Rule for Query String.
If a request matches the statement it will **Block** the request.
![image](https://github.com/user-attachments/assets/a1988f9a-0fb7-4a06-86d2-80333d1cd2a9)
![image](https://github.com/user-attachments/assets/af476311-aea4-4f98-93c4-d6ad984a5dcd)


### Web ACL Rule for SQL Injection.
Add the Web ACL from **AWS managed rule groups**.
Select **SQL database**.
![image](https://github.com/user-attachments/assets/47bb0a45-e2b6-4f89-a91d-2d9a1f461c88)
![image](https://github.com/user-attachments/assets/34193ba9-1b7f-42f7-a730-48f65d7d4b98)


**Web ACl has been created.**
![image](https://github.com/user-attachments/assets/d2e9f403-ed64-42c8-83f3-ac8475204695)

### Click in the Web ACL which is created, go to the **Rules** you can see all rules which you have created.

![image](https://github.com/user-attachments/assets/9afe8787-26fa-44f7-9352-a4ee495beba3)


### In the Associated AWS resources you can see Application Load Balancer.

![image](https://github.com/user-attachments/assets/c7bc05db-104f-4416-b6d7-b5e57b819e23)


### In the Sampled requests you can see details about all metrics.
![image](https://github.com/user-attachments/assets/97a049a1-b6f7-428f-9140-0800ecb8e54b)

## You can see all details in Sampled requests, navigate to bottem.

### Webserver-WAF-Web-ACL
![image](https://github.com/user-attachments/assets/ccb21d92-44a9-4d42-9b8d-2ebf7c166638)
![image](https://github.com/user-attachments/assets/c4fd9295-ddfb-4552-be80-6ae239680b9a)


### Geo-location-rule
I have created Windows EC2 instance in Singapur Region and tested for geo location.
![image](https://github.com/user-attachments/assets/b840049a-177d-4a58-b321-228761904d25)

## Ip Address which i have highlighted is of my EC2 which i have created, other IPs are unknown IPs, it's looks like someone was trying to access ALB from another country.

![1](https://github.com/user-attachments/assets/0d8faee2-4bd1-4b11-99c4-8adf89196452)


### Query-String
![2](https://github.com/user-attachments/assets/d151234f-7198-4962-a28e-5e678e0bd381)
![3](https://github.com/user-attachments/assets/4c83a223-640b-488c-bc53-69cda55dbb66)

### SQL Injection
![image](https://github.com/user-attachments/assets/3c522f8c-d7f9-490e-961f-d9c01645620c)
![image](https://github.com/user-attachments/assets/50841922-0570-4071-9518-85447203c889)


Thank you!
