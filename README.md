# Monitoring and Alert Management

![EC2 CLOUDWATCH](https://user-images.githubusercontent.com/110179866/186394768-4924d159-75ef-427e-8c28-634e61a1ff11.jpeg)



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

To ensure that your support team is notified when your application experiences high latencies, you create the following alerting policy:

```
 If the HTTP response latency is higher than two seconds for at least five
  minutes, then open an incident and send an email to your support team.
  ```



## AWS SNS & SQS

- SNS - Amazon Simple Notification Service (Amazon SNS) is a web service that makes it easy to set up, operate, and send notifications from the cloud.

- SQS - Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.



### How do they differ?

Amazon Simple Queue Service (SQS) and Amazon SNS are both messaging services within AWS, which provide different benefits for developers. Amazon SNS allows applications to send time-critical messages to multiple subscribers through a “push” mechanism, eliminating the need to periodically check or “poll” for updates.

