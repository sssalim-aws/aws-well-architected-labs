---
title: "Level 200: Running Well-Architected Framework Review using AWS Trusted Advisor Integration"
menutitle: "Level 200: Running Well-Architected Framework Review using AWS Trusted Advisor Integration"
description: "Running Well-Architected Framework Review using AWS Trusted Advisor Integration"
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 3
tags:
  - trusted_advisor_integration
---
## Authors

* Phong Le, Geo Solutions Architect, AWS Well-Architected
* Stephen Salim, Geo Solutions Architect, AWS Well-Architected
* Carlos Peres, Geo Solutions Architect, AWS Well-Architected

## Contributors
* Jang Whan Han, Geo Solutions Architect, AWS Well-Architected

## Introduction


Cloud workload optimization is a continuous process that involves learning, measuring workload alignment against best practices, and taking necessary actions to improve alignment as needed. By reviewing the workload against best practices, areas for improvement can be identified and actions can be taken to fine-tune configurations or adjust processes. These action items should be managed to ensure accountability, ownership, and visibility towards the progress of workload optimization. AWS Well-Architected provides a tool to aid architecture review processes, which integrates with [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/) to provide better insights and understanding of workload resource configuration.

Leveraging this integration, data and insights can be provided into the Well-Architected Framework Review across accounts. Findings can then be turned into actionable items and tracked in change management systems to ensure accountability and visibility towards the improvement progress of workload optimization.

In this lab, you will learn how to use AWS Well-Architected Tool Integration with AWS Trusted Advisor to provide data and insights into your Well-Architected Framework Review across your accounts. You will also learn how to turn these findings from the review into actionable items in JIRA to ensure accountability and streamline visibility towards the progress of your improvements.

The skills you learn will help you to accelerate your cloud optimization by reducing the time required to measure workloads against the AWS best practices in the [AWS Well-Architected Framework.](https://aws.amazon.com/architecture/well-architected/)


![OverallArchitecture](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/overall_architecture_00.png)


## Goals:

* Enable AWS Well-Architected Tool integration with AWS Trusted Advisor across multiple accounts.
* Perform a Well-Architected Framework Review and use AWS Trusted Advisor integration to define the Improvement action item.
* Track and record Improvement action items in JIRA for accountability & visibility.

## Prerequisites:

* Business or Enterprise Support plan enabled in AWS Account.
  To access relevant Trusted Advisor checks used in this lab, If  Business Support plan is not enabled, only 6 Trusted Advisor checks referenced [here](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor-check-reference.html) are available.
* (Optional) Access to [Atlassian JIRA](https://www.atlassian.com/software/jira) is required to complete section 4.

{{% notice note %}}
**NOTE**: You will be billed for any applicable AWS resources used as part of this lab, that are not covered in the AWS Free Tier.
{{% /notice %}}

## Lab Duration:
Estimated time required to complete this lab is 1 hour.

{{< prev_next_button link_next_url="./1_deploy_sample_workload/" button_next_text="Start Lab" first_step="true" />}}

## Steps:
{{% children  %}}
