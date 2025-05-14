# Implementing AWS WAF with ALB to Safeguard Against SQL Injection, Geo Location, and Query String Threats.
![Untitled Diagram](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/6093f21f-8b6f-420b-b4e6-65c86a55fe2a)

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
![Screenshot 2023-11-28 040151](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/952012a5-0eb4-47af-bcc5-fe9f6a05f4b8)

## Create Target Groups, Register target (Instance)

![Screenshot 2023-11-28 040955](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/3d4a5602-4e06-4e8a-84f0-0bae581d3ec2)

## Load Balancer
### Create Application Load Balancer and add Target Group.

![Screenshot 2023-11-28 042104](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/fc7a44e0-bf9f-4713-9aef-bf50d38290d2)

## AWS WAF (Web Application Firewall)
### Define Web ACLs Rules.
### Select the Region in which Application Load Balancer is deployed.
![Screenshot 2023-11-28 042331](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/77688ed5-1421-486e-abcc-5af079f1ab31)

### Describe web ACL and associate it to AWS resources.
![Screenshot 2023-11-28 042721](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/c1aba7e5-aaa0-4fe2-8005-e7a5a0c1268d)

### Add rules and rule groups.
Select from Add Rules **Add my own rules and rule groups**
![Screenshot 2023-11-28 042924](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/87f6fb33-edb7-4702-a0dd-2ef6e83741d4)

Now select **Rule builder**.
![Screenshot 2023-11-28 043246](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/cde32046-a0da-40d8-b677-ab1030313d64)
### Web ACL Rule for Geo Location.
If a request doesn't match the statement then it will **Block** the request.
![Screenshot 2023-11-28 043336](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/0f2c30fe-5d99-4909-a6df-80153c4aa6a1)

### Web ACL Rule for Query String.
If a request matches the statement it will **Block** the request.
![Screenshot 2023-11-28 043451](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/9194aa17-80f9-4191-b19b-2264f9607421)
![Screenshot 2023-11-28 043540](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/d21d3ed6-dea0-4ca4-a875-be2aeeea0758)

### Web ACL Rule for SQL Injection.
Add the Web ACL from **AWS managed rule groups**.
Select **SQL database**.
![Screenshot 2023-11-28 043645](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/be48a196-0d40-4d2c-a140-4c4acd8c7ae3)
![Screenshot 2023-11-28 043740](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/d6dcec00-e5bb-4bab-8332-37b46ff8247c)

**Web ACl has been created.**
![Screenshot 2023-11-28 044252](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/6d91d84d-8b9f-4cfa-9387-6c4ce69dd7b2)
### Click in the Web ACL which is created, go to the **Rules** you can see all rules which you have created.

![Screenshot 2023-11-28 044821](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/616998e0-b26f-49d5-8b39-205c1537b4de)

### In the Associated AWS resources you can see Application Load Balancer.

![Screenshot 2023-11-28 044906](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/51deb496-b8de-4a0f-9e70-1ebcc022fe0d)

### In the Sampled requests you can see details about all metrics.
![Screenshot 2023-11-28 045602](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/7d330b65-0101-49d8-bfc9-221650fcd4cf)

## You can see all details in Sampled requests, navigate to bottem.

### Webserver-WAF-Web-ACL
![Screenshot 2023-11-28 051249](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/8c711f1e-2ddc-487b-b022-879ea66fbb53)
![Screenshot 2023-11-28 050653](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/e59d76a4-3af9-4780-82bc-0347a4e3ae52)

### Geo-location-rule
I have created Windows EC2 instance in Singapur Region and tested for geo location.
![Capture](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/02f9fa93-02eb-42a8-871b-1feb4b78cf60)
## Ip Address which i have highlighted is of my EC2 which i have created, other IPs are unknown IPs, it's looks like someone was trying to access ALB from another country.
![Screenshot 2023-11-28 053509](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/4f64bb5a-01eb-40ba-96dd-563a158b223a)

### Query-String
![Screenshot 2023-11-28 051507](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/6c6812ac-9c86-437d-b52e-7bdcc1ace779)
![Screenshot 2023-11-28 050731](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/fcba7d14-5959-4a16-89cd-3fb7f53e3516)

### SQL Injection
![Screenshot 2023-11-28 051715](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/e5000d4e-1a5e-4c29-8abd-47f96627a2c7)
![Screenshot 2023-11-28 050751](https://github.com/pradip2994/AWS_WAF_Implementation_with_ALB/assets/124191442/d237eab5-737d-4e09-8386-976e3a9d98e8)

Thank you!
