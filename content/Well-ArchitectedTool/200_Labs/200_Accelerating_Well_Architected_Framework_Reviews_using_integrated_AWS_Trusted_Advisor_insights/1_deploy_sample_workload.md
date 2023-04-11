---
title: "Deploy Sample Workload"
menutitle: "Deploy Sample Workload"
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---


In this section, you will deploy a sample workload resources that you will run the Well-Architected Framework Review against.
The workload will be deployed in a separate AWS account simulating a multi account environment.  Once you have completed this lab, you will have a workload deployed in your AWS account with the architecture shown below.

![SampleWorkload](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_sample_workload_architecture_before.png)


Follow below instructions to configure the workload:

### 1.0. Provision the Workload Account using AWS Organization.

In this first step you will provision an AWS Account that you will use to run the Sample Workload.

1. Sign in to the AWS Management Console using your Administrator credentials.
2. Navigate to the AWS Organizations console.

    ![Section1_1.2](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_1.2.png)

3. If this is the first time you are using AWS Organization, on the Introduction page, choose **Create an organization**. 
   Follow the prompts, and enter your email address to verify your email. 
   If you already have an AWS Organizations set up in your account, you can skip this step.

4. Once your organization is created, navigate to the "AWS accounts" page from the left menu. Confirm that AWS Organizations is created. 
   When your organization is fully created, you will be able to view your Root OU of your organizations as per screenshot below.

    ![Section1_1.4](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_1.4.png)

5. Select the **Root** OU, then click on **Actions**.
6. Under **Organizational Unit** click on **Create new**.

    ![Section1_1.6](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_1.6.png)

7. Enter `Workload` as the name of the OU and click **Create organizational unit**.

8. Click on the Organizational unit you just created, and take note of the Organization Unit ID as per screenshot.

    ![Section1_1.7a](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_1.7a.png)

9. Navigate back to the **AWS accounts** page and  tab and click on **Add an AWS Account**.

    ![Section1_1.8](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_1.8.png)

10. Enter `SampleWorkload` as the name of the account, type in your `email address` for the account.
   Wait for the email to arrive in your inbox and verify the temail.

11. Nagivate or referesh the "AWS accounts" page view.
12. Select the new account you just create, then click on **Actions** and **Move** under AWS account.
13. Select the **Wordload** OU you created before, then click **Move AWS Account**

    ![Section1_1.12](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_1.12.png)

14. You have now created the Sample Workload Account in the Workload Organization Unit.



### 2.0. Configure AWS CloudFormation StackSet for assume role.

1.  Navigate to the AWS Organizations console.
    
    ![Section1_2.1](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_2.1.png)

2.  Choose "StackSets" from the left-hand menu.

3.  Click **Enable trusted access** on the banner ofr "Enable trusted access with AWS Organizations to use service managed permissions".

    ![Section1_2.2](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_2.2.png)

### 3.0. Deploy Sample Workload Using Stackset.

In this first step you will provision a [CloudFormation](https://aws.amazon.com/cloudformation/) stackset that builds a sample workload along with the necessary underlying resource. 

1. Download the sample workload CloudFormation Template [here](https://raw.githubusercontent.com/sssalim-aws/aws-well-architected-labs/L200_WAFR_Acceleration/static/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Code/sample_workload_environment.yaml).

2. Navigate to the AWS CloudFormation console.

3. Click on "StackSets" in the navigation pane and then click on "Create StackSet".

4. Under Specify template, select **Upload a template file** and upload the file you downloaded in step 1. Then Click on **Next**.

5. Specify `walab-wata-sample-workload` as the **StackSet Name**.

6. Leave all settings as default and click **Next**.

7. In the **Configure StackSet options** page add a new tag named ``ApplicationId`` with value ``MySampleWorkload`` (this will allow for the proper identification of resources as part of the solution described in Section 4 of this lab). Leave Execution configuration as **Inactive**, then click **Next**.

    ![Section3_9](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_9.png)

8. In the **Deployment locations** section, select **Deploy stacks in organizational units** 

9. Under **AWS OU ID** enter in the Organizational Unit ID you captured in step 1 previously.

    ![Section3_10](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section3_10.png)

10. Specify the region you wish to deploy the workload to, Click **Next**, Click **Submit**

11. Wait until deployment is complete, and your Stack Operation status is **SUCCEEDED**



## Congratulations! 

You have now completed the first section of the Lab.

You should have a sample workload architecture which we will use for the remainder of the lab.

{{< prev_next_button link_prev_url="../" link_next_url="../2_create_workload_review/" />}}
