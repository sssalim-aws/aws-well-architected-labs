---
title: "Running AWS Well-Architected Framework Review using AWS Trusted Advisor."
menutitle: "Running AWS Well-Architected Framework Review using AWS Trusted Advisor."
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 3
pre: "<b>3. </b>"
---
In this section, you will simulate a shortened version of an AWS Well-Architected Framework Review on the Sample Workload we deployed, focusing on one of the pillars in the framework. These steps will guide you on how to use questions in the AWS Well-Architected Tool to review the architecture in the Sample Workload against best practices. You will also learn how to leverage the Trusted Advisor Checks Integration to provide further guidance on what actions can be taken to make improvements.

![Diagram](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_architecture.png)

Let’s take the Reliability Pillar of the Well-Architected Framework as an example. The reliability pillar encompasses the ability of a workload to perform its intended function correctly and consistently when it’s expected to. This includes operating and testing the workload through its total lifecycle.

In this case, we will use [Question 10 from the Reliability Pillar](https://wa.aws.amazon.com/wat.question.REL_10.en.html), as there are Trusted Advisor checks related to the best practices in it.

1. AWS Well-Architected Reliability Question 10 includes best practices related to how workload can be protected by using fault isolation. Fault-isolated boundaries limit the effect of a failure within a workload to a limited number of components. Components outside of the boundary are unaffected by the failure. Using multiple fault-isolated boundaries, you can limit the impact on your workload. 

2. Click on **Start reviewing** and navigate to **REL 10. How do you use fault isolation to protect your workload?** in the Well-Architected Tool to review the question.

![REL10](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_q10.png)


3. You can select a question in the Well-Architected Tool to access Trusted Advisor checks as insights. If Trusted Advisor checks related to REL 10 question are available, there will be a **View checks** button as presented in the screenshot below.Alternatively you can also select the **Trusted Advisor checks** tab.

![Trusted Advisor Tab](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_access_ta.png)

4. The Trusted Advisor checks provides further insights around resource configurations and how it it aligned to the related best practice in thr question.

In this scenario, under Reliability Best Practice of ["**Deploy the workload to multiple locations**"](https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_fault_isolation_multiaz_region_system.html). 

You will see several Trusted Advisor checks including **Amazon EC2 Availability Zone Balance** and **Amazon RDS Multi-AZ**.Along with the total number of identified resources in each account. 

![Trusted Advisor](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_ta.png)

5. To find further information about the check, you can click on the **Info** link, to show details and context about the Trusted Advisor check behaviour.

![Trusted Advisor EC2 AZ](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_ec2_az.png)

Which in this example, indicates that the Amazon EC2 instances in the Sample Workload Account are at risk, as they are not deployed across Availability Zones in the region. 

![Trusted Advisor RDS Multi-AZ](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_rds.png)

Along with that, the Amazon RDS in the Sample Workload account, also does not have Multi-AZ enabled, which increases risk of service interuption when failure occurs.

6. To locate the  resources being checked, you can access the Sample Workload Account by following the instruction to **Switch to the role for member account** described [here](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_access.html#orgs_manage_accounts_access-cross-account-role). And use the **Sample Workload** Account Id you took note in the first section of this lab.

7. Once you are logged in, you can open the Trusted Advisor Console and identify AWS resources related to the check as per screenshots below.

![EC2 AZ](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_ta_ec2_az.png)

![RDS Multi-AZ](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_ta_rds.png)

## Congratulations! 

You have completed simulating an AWS Well-Architected Framework Review using Well-Architected Tool and Trusted Advisor. 

Click on **Next Step** to continue to the next section.

{{< prev_next_button link_prev_url="../2_create_workload" link_next_url="../4_streamline_jira/" />}}
