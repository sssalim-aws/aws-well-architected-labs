---
title: "Running AWS Well-Architected Framework Review using AWS Trusted Advisor."
menutitle: "Running AWS Well-Architected Framework Review using AWS Trusted Advisor."
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 3
pre: "<b>3. </b>"
---
In this section, you will simulate a shortened version of an AWS Well-Architected Framework Review on the Sample Workload, focusing on one of the pillars in the framework. These steps will guide you on how to use questions in the AWS Well-Architected Tool to compare the architecture in the Sample Workload against best practices. You will also learn how to leverage the Trusted Advisor Checks Integration to provide further guidance on what actions can be taken to make improvements.

![Diagram](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_architecture.png)

In this section, let's take the Reliability Pillar of the Well-Architected Framework as an example. 
The reliability pillar encompasses the ability of a workload to perform its intended function correctly and consistently when it’s expected to. This includes the ability to operate and test the workload through its total lifecycle.

Let’s explore an example question. In this case, we will use [Question 10 from the Reliability Pillar](https://wa.aws.amazon.com/wat.question.REL_10.en.html), as there are Trusted Advisor checks related to the best practices in it: How do you use fault isolation to protect your workload?

1. AWS Well-Architected Reliability Question 10 includes best practices that are related to how workload can be protected by using fault isolation. Fault isolated boundaries limit the effect of a failure within a workload to a limited number of components. Components outside of the boundary are unaffected by the failure. Using multiple fault isolated boundaries, you can limit the impact on your workload. 

2. Navigate to <b>REL 10. How do you use fault isolation to protect your workload?</b> in the Well-Architected Tool to review the question

![REL10](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_q10.png)


3. To access Trusted Advisor checks as insights, you can select a question in the Well-Architected Tool. If there are related Trusted Advisor checks available for a question, there will be a “View checks” button like the screenshot below. You can also select the “Trusted Advisor checks” tab. 

![Trusted Advisor Tab](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_access_ta.png)

4. Trusted Advisor checks are available, which provide insights related to the best practice in the question. You will also notice the state of resources recommendations and the count of resources. Trusted Advisor checks that relate to the best practice “Deploy the workload to multiple locations” are displayed. 

![Trusted Advisor](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_ta.png)

One of the Trusted Advisor checks identified with a x in a circle (denoting “Action recommended”) status is on the Amazon EC2 Availability Zone Balance.

![Trusted Advisor EC2 AZ](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_ec2_az.png)

The reason is because the Amazon EC2 instances used in the sample workload were not deployed across Availability Zones in a region. Availability Zones are distinct locations that are designed to be insulated from failures in other Availability Zones and to provide inexpensive, low-latency network connectivity to other Availability Zones in the same region. By launching instances in multiple Availability Zones in the same region, you can help protect your applications from a single point of failure.

One of the Trusted Advisor checks identified with a x in a circle (denoting “Action recommended”) status is on the Amazon RDS Multi-AZ. 

![Trusted Advisor RDS Multi-AZ](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_rds.png)

The reason is because the RDS instance in the sample workload was deployed in a single Availability Zone. 
Multi-AZ deployments enhance database availability by synchronously replicating to a standby instance in a different Availability Zone. During planned database maintenance or the failure of a DB instance or Availability Zone, Amazon RDS automatically fails over to the standby so that database operations can resume quickly without administrative intervention.

5. Exploring the Trusted Advisor Console in the workload account, you can identify the region has uneven EC2 distribution

![EC2 AZ](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_ta_ec2_az.png)

And you can also identify the DB instance that was deployed in a single Availability Zone

![RDS Multi-AZ](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_ta_rds.png)

{{< prev_next_button link_prev_url="../2_create_workload" link_next_url="../4_cleanup/" />}}
