# AWS-LOAD-BALANCER
### REG NUMBER: 212224110027
### NAME: KABELAN G K
## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM
### Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

### Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

### Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

### Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

### Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

### Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## OUTPUT
<img width="1404" height="913" alt="Screenshot 2026-08-20 103737" src="https://github.com/user-attachments/assets/287c0c70-439a-4608-8a69-f17c95c896c5" />
<img width="1401" height="919" alt="Screenshot 2026-08-20 103714" src="https://github.com/user-attachments/assets/c0acee38-3441-481d-8b0c-a323911210da" />
<img width="1388" height="896" alt="Screenshot 2026-08-20 103829" src="https://github.com/user-attachments/assets/1f83af5d-2d27-4f74-8ba5-604bf626d11a" />
<img width="1392" height="917" alt="Screenshot 2026-08-20 104213" src="https://github.com/user-attachments/assets/953788b1-9139-4456-beb4-da8d5c21e986" />
<img width="1417" height="901" alt="Screenshot 2026-08-20 104232" src="https://github.com/user-attachments/assets/1196321f-cb80-402e-9715-37c85aa960bc" />
<img width="1405" height="909" alt="Screenshot 2026-08-20 104839" src="https://github.com/user-attachments/assets/2e84c224-78ad-482f-9cae-6db2714c94bf" />
<img width="1395" height="894" alt="Screenshot 2026-08-20 104915" src="https://github.com/user-attachments/assets/5a88044b-af68-4fcd-9361-ee5f85ba357e" />
<img width="1437" height="940" alt="Screenshot 2026-08-18 094600" src="https://github.com/user-attachments/assets/178a9274-5f46-44e5-824c-55a4b17315c3" />
<img width="1388" height="897" alt="Screenshot 2026-08-20 111123" src="https://github.com/user-attachments/assets/3bf92670-bc17-4a02-8583-13af3562a789" />
<img width="1915" height="928" alt="Screenshot 2026-08-18 095310" src="https://github.com/user-attachments/assets/12445bd5-3bc7-4649-845c-ed365fb60a1f" />
<img width="1180" height="659" alt="Screenshot 2026-08-20 111617" src="https://github.com/user-attachments/assets/54418953-3f57-45e2-94c8-21a8924f3fe4" />




## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
