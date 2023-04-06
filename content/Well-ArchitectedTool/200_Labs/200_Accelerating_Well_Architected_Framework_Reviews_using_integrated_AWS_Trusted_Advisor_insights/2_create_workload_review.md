---
title: "Prepare Well-Architected Framework Review Workload"
date: 2020-12-17T11:16:09-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---
 
With the sample workload deployed in the workload account, you can now conduct an AWS Well-Architected Framework Review on it.
The purpose of the AWS Well-Architected Framework Review Exercise is to measure the alignment of your workload with the AWS Well-Architected Framework Best Practices. The review will identify areas for improvement that can be implemented in the workload to achieve better alignment.
To assist with the review process, AWS Well-Architected provides a tool to access information about best practices that can be used as a guide during conversations with workload stakeholders. The tool provides insights into the configuration of AWS resources used in the workload by integrating with AWS Trusted Advisor checks. It also provides the capability to capture alignments and improvements over time.

![Section2 Architecture](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section2_architecture.png)

In this section of the lab, you will prepare for an AWS Well-Architected Framework Review of the sample workload by creating a workload resource in the AWS Well-Architected tool and enabling Trusted Advisor check capabilities.
Please follow the steps below to proceed with the lab.

### 1.0. Provision IAM Role for Trusted Advisor in Workload Account.
The AWS Well-Architected Tool is designed to help you review the state of your applications and workloads against architectural best practices, identify opportunities for improvement, and track progress over time.

![Section2 WATool](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section2_watool.png)

The AWS WA Tool periodically gets data from Trusted Advisor using the roles created in IAM. The IAM role is automatically created for the workload owner. However, to view Trusted Advisor information, the owners of any associated accounts on the workload must go to IAM and create a role, see [Activating Trusted Advisor for a workload in IAM](https://docs.aws.amazon.com/wellarchitected/latest/userguide/activate-ta-in-iam.html) for more details. If this role does not exist, AWS WA Tool cannot obtain Trusted Advisor information for that account and displays an error. 

We've created a CloudFormation template to facilate the process of creating IAM role in the workload account. YOu can follow the steps below to deploy the IAM roles into associated accounts for workload

You will provision a [CloudFormation](https://aws.amazon.com/cloudformation/) stackset that will deploy IAM Role with necessary permission policies for AWS WA Tool in Management Account to collect data in associated accounts for the workload

1. Download the sample workload CloudFormation Template [here](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Code/TrustedAdvisor_IAM_Role.yml).

2. Navigate to the AWS CloudFormation console.

3. Click on "StackSets" in the navigation pane and then click on "Create StackSet".

4. Under Specify template, select **Upload a template file** and upload the file you downloaded in step 1. Then Click on **Next**.

5. Specify `walab-wata-iam-role` as the **StackSet Name**.
   Under **ManagementAccount** specify the **Management Account ID**

6. Leave all settings as default and click **Next**.

7. Leave Execution configuration as **Inactive** then click **Next**.

8. In the **Deployment locations** section, select **Deploy stacks in organizational units** 

9. Under **AWS OU ID** enter in the Organizational Unit ID you captured in section 1 previously.

    ![Section3_9](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_9.png)

10. Specify the region you wish to deploy the workload to, Click **Next**, Click **Submit**

11. Wait until deployment is complete, and your Stack Operation status is **SUCCEEDED**

## 2.0 Create AWS Well-Architected Tool Workload.

In this section of the lab, you will create a workload in the AWS Well-Architected tool  

The Well-Architected Framework Reviews are conducted per workload. A workload is a collection of resources and code that delivers business value, such as a customer-facing application or a backend process. 
 
1. We will start with creating a workload in the Well-Architected Tool. Click **Define workload** associated with the necessary AWS tags.

![Section2WATool](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section2_tool.png)
 
2. Now you can [define a workload](https://docs.aws.amazon.com/wellarchitected/latest/userguide/define-workload.html):
 
![Section2 DefiningAWorkload](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section2_DefiningAWorkload.png)
 
The following are the required workload properties:
 
* workload-name - This is a unique identifier for the workload. Must be between 3 and 100 characters.
* description - A brief description of the workload. Must be between 3 and 250 characters.
* review-owner - The name, email address, or identifier for the primary individual or group that owns the review process. Must be between 3 and 255 characters.
* environment - The environment in which your workload runs. This must either be PRODUCTION or PREPRODUCTION
* aws-regions - The aws-regions in which your workload runs (us-east-1, etc).
* lenses - The list of lenses associated with the workload. All workloads must include the "wellarchitected" lens as a base, but can include additional lenses. 

3. Specify **workload account ID** created in Section 1 in the Account IDs field. This field is required to activate Trusted Advisor. 

4. To enable the integration with Trusted Advisor, after the necessary workload information has been entered, within the <b>AWS Trusted Advisor” section</b>, tick on <b>Activate Trusted Advisor</b>

![Enable Trusted Advisor](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/Enabling-the-Trusted-Advisor-feature.png)

5. Choose the lenses that apply to this workload. **AWS Well-Architected Framework** has been selected by default.

![Lens](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/WAF_Lens.png)

## Congratulations! 

You have defined a workload and enable Trusted Advisor to review.

Click on **Next Step** to continue to the next section.

{{< prev_next_button link_prev_url="../1_deploy_infrastructure/" link_next_url="../3_perform_review/" />}}
 
