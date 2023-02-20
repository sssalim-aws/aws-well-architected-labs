---
title: "Level 300: Streamlining Workload Optimization using Change Management Tool"
#menutitle: "Lab #3"
chapter: false
weight: 1
---
## Authors
- Carlos Peres, AWS Well-Architected Geo SA
- Stephen Salim, AWS Well-Architected Geo SA

## Feedback
If you wish to provide feedback on this lab, there is an error, or you want to make a suggestion, please email: sssalim@amazon.com or clp@amazon.com

## Introduction

Cloud workload optimization is a continuous process that involves learning and measuring your workload against known best practices, and then taking the necessary actions to improve alignment as needed. By reviewing your workload against best practices, you can identify areas for improvement and take necessary actions to optimize, fine-tune architecture, or adjust your processes. These  action items will then need to be managed to ensure accountability, ownership, and visibility towards the progress of workload optimization. 

To review your workload, you can use Well-Architected Tool and measure your current architecture and practices against the AWS Well-Architected Best Practices. The tool offers a set of questions and best practice information to assist your conversations during the review, and it provides insights into resources configuration that can be improved using AWS Trusted Advisor. Once these improvements are identified, you will need to manage their lifecycle to ensure that they are being addressed accordingly. 

One of the most common ways to do this is by leveraging a change management system, such as JIRA.
JIRA allows you to create and manage tickets for each improvement item, assign them to specific team members or departments, track their progress, and ensure that they are properly prioritized and addressed. This helps to ensure accountability, ownership, and visibility into the progress of workload optimization. 

In this lab, we will guide you through an example on how to integrate your AWS Well-Architected Tool with JIRA, using various AWS services. 
The integration will allow you to manage the lifecycle of the improvement items identified in the Well-Architected Framework review. By following the steps in this lab, you will gain a better understanding of how you can use Well-Architected Tool API and other AWS services, to automate the process of managing improvement items of your cloud workload optimization process.

## Architecture overview

![OverallArchitecture](/Well-ArchitectedTool/300_Labs/300_Streamlining_Workload_Optimization_Using_Change_Management_Tool/Images/overall_architecture.png)

## Goals


## Prerequisites

## Permissions required

## Steps:
{{% children  /%}}

{{< prev_next_button link_next_url="./1_etl_wa_workload_data/" button_next_text="Start Lab" first_step="true" />}}
