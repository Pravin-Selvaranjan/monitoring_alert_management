# Monitoring and Alert Management

![EC2 CLOUDWATCH (1)](https://user-images.githubusercontent.com/110179866/186463374-47326c07-7919-4b5a-815a-6efbb7af066f.jpeg)




## Monitoring

Monitoring is a set of practices you can use to verify the security and performance of your AWS resources and data. These practices rely on various tools and services to collect, analyze, and present data insights. You can then use these insights to identify vulnerabilities and issues, predict performance, and optimize configurations.


## Why do we need to Monitor?
- To make sure that your website/cloud and app are always online.
- To make your application secure for your customers.
- It can help you monitor the resultant performance and cost of your application.
- Troubleshooting and recommendation for future and how to avoid the existing errors.


In AWS there are multiple ways to achieve Monitoring, some of these are 

- CloudWatch

- CloudTrail 

- Certificate Manager

- EC2 Dashboard


### CloudWatch

CloudWatch is a service you can use to aggregate, visualize, and respond to service metrics. CloudWatch has two main components: alarms, which create alerts according to thresholds for single metrics, and events, which can automate responses to metric values or system changes.


### CloudTrail 

CloudTrail is a service that you can use to track events across your account. The service automatically records event logs and activity logs for your services and stores the data in S3. Collected data includes user identities, traffic origin IPs, and timestamps. You can view all management events for free for the most recent 90 days. Data events and insights based on your data are also available for an additional fee.


### Certificate Manager

Certificate Manager is a tool you can use to provision, manage, and apply transport layer security (TLS) and secure sockets layer (SSL) certificates. These certificates are used to prove your services or devices' authenticity and enable you to secure network connections.

### EC2 Dashboard

EC2 Dashboard is a monitoring tool for the Amazon EC2 virtual machine service. You can use this dashboard to monitor and maintain your EC2 instances and infrastructure. The dashboard lets you view instance states and service health, manage alarms and status reports, view scheduled events, and assess volume and instance metrics


## 4 Golden Signals

- Latency - The time it takes to service a request. It’s important to distinguish between the latency of successful requests and the latency of failed requests.

- Traffic - A measure of how much demand is being placed on your system, measured in a high-level system-specific metric.

- Errors - The rate of requests that fail, either explicitly (e.g., HTTP 500s), implicitly (for example, an HTTP 200 success response, but coupled with the wrong content), or by policy (for example, "If you committed to one-second response times, any request over one second is an error").

- Saturation - How "full" your service is. A measure of your system fraction, emphasizing the resources that are most constrained (e.g., in a memory-constrained system, show memory; in an I/O-constrained system, show I/O). Note that many systems degrade in performance before they achieve 100% utilization, so having a utilization target is essential.


## Alert Management

Alerting gives timely awareness to problems in your cloud applications so you can resolve the problems quickly.
In Cloud Monitoring, an alerting policy describes the circumstances under which you want to be alerted and how you want to be notified.

#### Example 

You deploy a web application onto an EC2 instance that's running a web application. While you expect the HTTP response latency to fluctuate, you want your support team to respond when the application has high latency for a significant time period.

To ensure that your support team is notified when your application experiences high latencies, you would incorporate something along the lines of, If the HTTP response latency is higher than two seconds for at least five minutes, then send an email to the support team.



## AWS SNS & SQS

- SNS - Amazon Simple Notification Service (Amazon SNS) is a web service that makes it easy to set up, operate, and send notifications from the cloud.

- SQS - Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.



### How do they differ?

Amazon Simple Queue Service (SQS) and Amazon SNS are both messaging services within AWS, which provide different benefits for developers. Amazon SNS allows applications to send time-critical messages to multiple subscribers through a “push” mechanism, eliminating the need to periodically check or “poll” for updates.

Amazon SQS is a message queue service used by distributed applications to exchange messages through a polling model, and can be used to decouple sending and receiving components.

A common pattern is to use SNS to publish messages to Amazon SQS queues to reliably send messages to one or many system components asynchronously.



# Setting up an alarm with EC2 instances

- Select the instance and choose Actions, Monitor and troubleshoot, Manage CloudWatch alarms.

<img width="860" alt="alarm setup" src="https://user-images.githubusercontent.com/110179866/186426332-2f77ed72-67ee-4fc9-be53-dcd36303ffba.png">


- On the Manage CloudWatch alarms detail page, under Add or edit alarm, select Create an alarm.


- For Alarm notification, choose whether to turn the toggle on or off to configure Amazon Simple Notification Service (Amazon SNS) notifications. Enter an existing Amazon SNS topic or enter a name to create a new topic.


- For Alarm action, choose whether to turn the toggle on or off to specify an action to take when the alarm is triggered. Select an action from the dropdown.


- For Alarm thresholds, select the metric and criteria for the alarm. For example, you can leave the default settings for Group samples by (Average) and Type of data to sample (CPU utilization). For Alarm when, choose >= and enter 0.80. For Consecutive period, enter 1. For Period, select 5 minutes.


- Once you have completed the above steps you should receive an email asking you to confirm the endpoint from SNS, be sure to confirm this and receive the below notification.

<img width="340" alt="sns confirmed" src="https://user-images.githubusercontent.com/110179866/186426426-9ddb80ef-cf69-41ee-8548-7f1907c97d59.png">

- If your instance exceeds the given paramaters ( in this case the CPU over 20 percent)
you will receive the following notification in your email


<img width="635" alt="SNS email not" src="https://user-images.githubusercontent.com/110179866/186426448-1fee9d4e-67dc-4250-8806-4bfc2defdc14.png">


# Autoscaling and Load Balancing 

![load balancer](https://user-images.githubusercontent.com/110179866/186463396-855eb422-cf25-46e5-82d1-29cf28a05e7a.jpeg)


- Autoscaling automatincally adjusts the amount of computational resources based on the server load

- Load Balancing distributes traffic beetween ec2 instances so that no one instance gets overwhelmed

## Application Load Balancer
An Application Load Balancer makes routing decisions at the application layer (HTTP/HTTPS), supports path-based routing, and can route requests to one or more ports on each container instance in your cluster. Application Load Balancers support dynamic host port mapping. For example, if your task's container definition specifies port 80 for an NGINX container port, and port 0 for the host port, then the host port is dynamically chosen from the ephemeral port range of the container instance (such as 32768 to 61000 on the latest Amazon ECS-optimized AMI). 

## Network Load Balancer

A Network Load Balancer makes routing decisions at the transport layer (TCP/SSL). It can handle millions of requests per second. After the load balancer receives a connection, it selects a target from the target group for the default rule using a flow hash routing algorithm. It attempts to open a TCP connection to the selected target on the port specified in the listener configuration.


## Auto scaling policies 
- Simple - Simple scaling relies on a metric as a basis for scaling. For example, you can set a CloudWatch alarm to have a CPU Utilization threshold of 80%, and then set the scaling policy to add 20% more capacity to your Auto Scaling group by launching new instances. Accordingly, you can also set a CloudWatch alarm to have a CPU utilization threshold of 30%. When the threshold is met, the Auto Scaling group will remove 20% of its capacity by terminating EC2 instances. 


- Step - Step Scaling further improves the features of simple scaling. Step scaling applies “step adjustments” which means you can set multiple actions to vary the scaling depending on the size of the alarm breach. 


- Target tracking - Target tracking policy lets you specify a scaling metric and metric value that your auto scaling group should maintain at all times. Let’s say for example your scaling metric is the average CPU utilization of your EC2 auto scaling instances, and that their average should always be 80%. When CloudWatch detects that the average CPU utilization is beyond 80%, it will trigger your target tracking policy to scale out the auto scaling group to meet this target utilization.


## Target Groups

Target Group is a way of getting network traffic routed via specified protocols and ports to specified instances. It's basically load balancing on a port level. This is used mostly to allow accessing many applications running on different ports but the same instance.

A target group contains EC2 instances to which a load balancer distributes workload.

A load balancer paired with a target group does NOT yet have auto scaling capability.

This is where auto scaling comes in. An auto scaling group (ASG) can be attached to a load balancer.

We can attach auto scaling rules to an ASG. Then, when thresholds are met (e.g. CPU utilization), the number of instances will be adjusted programatically.


![Blank diagram (8)](https://user-images.githubusercontent.com/110179866/186672880-d7b1bdfe-f5e0-4eca-8ba4-27aed1ecdfcc.jpeg)


# Creating a service to automate running a service in Linux

- `cd /etc/systemd/system`
- Create a file named [servicename.service] and add the following
 ```
[Unit]
Description=<description_about_your_service>

[Service]
User=<user_such_as_root>
WorkingDirectory=<directory_of__your_script such as /home/unixcop>
ExecStart=<script_which_needs_to_be_executed>
Restart=always

[Install]
WantedBy=multi-user.target
```

- `sudo systemctl daemon-reload`
- `sudo systemctl start [your_new_service].service`
- `sudo systemctl status unixcop.service`
- To enable on every reboot
- `sudo systemctl enable unixcop.service`
- 
