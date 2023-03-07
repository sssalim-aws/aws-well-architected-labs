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
8. Navigate back to the **AWS accounts** page and  tab and click on **Add an AWS Account**.

    ![Section1_1.8](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_1.8.png)

9. Enter `SampleWorkload` as the name of the account, type in your `email address` for the account.
   Wait for the email to arrive in your inbox and verify the temail.

10. Nagivate or referesh the "AWS accounts" page view.
11. Select the new account you just create, then click on **Actions** and **Move** under AWS account.
12. Select the **Wordload** OU you created before, then click **Move AWS Account**

    ![Section1_1.12](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_1.12.png)

13. You have now created the Sample Workload Account in the Workload Organization Unit.

### 2.0. Configure AWS CloudFormation StackSet.

1.  Navigate to the AWS Organizations console.
    
    ![Section1_2.1](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_2.1.png)

2.  Choose "StackSets" from the left-hand menu.

3.  Click **Enable trusted access** on the banner ofr "Enable trusted access with AWS Organizations to use service managed permissions".

    ![Section1_2.2](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_2.2.png)

4.  Click on "Create StackSet".
5.  In the "StackSet Details" section, give your StackSet a name, description, and choose a template source.
6.  In the "Deployment options" section, select "AWS Organizations" as the deployment target.
7.  In the "Permissions" section, specify the permissions required to deploy your StackSet.
8.  Click on "Next" to proceed to the "StackSet Settings" section.
9.  In the "StackSet Settings" section, select "Enable AWS Organizations" and choose the AWS Organizations entity to deploy your StackSet to.
10.  Click on "Next" to proceed to the "Review" section.
11. Review your StackSet configuration and click on "Create StackSet".
12. Once your StackSet is created, you can deploy it to the AWS accounts in your organization by creating a StackSet instance.


### 3.0. Deploy Sample Workload.

In this first step you will provision a [CloudFormation](https://aws.amazon.com/cloudformation/) stack that builds a sample workload along with the necessary underlying resource. You can choose the to deploy stack in one of the regions below. 

1. Click on the link below to deploy the stack. This will take you to the CloudFormation console in your account. Use `walab-wata-sample-workload` as the stack name, take the default values for all options, and create stack.

    * **us-west-2** : [here](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacksets/create/review?stackName=walab-wata-sample-workload&templateURL=https://aws-well-architected-labs-singapore.s3.ap-southeast-1.amazonaws.com/watools/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/sample_workload_environment.yaml)
    

    * **ap-southeast-2** : [here](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacksets/create/review?stackName=walab-wata-sample-workload&templateURL=https://aws-well-architected-labs-singapore.s3.ap-southeast-1.amazonaws.com/watools/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/sample_workload_environment.yaml)
    

    * **ap-southeast-1** : [here](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacksets/create/review?stackName=walab-wata-sample-workload&templateURL=https://aws-well-architected-labs-singapore.s3.ap-southeast-1.amazonaws.com/watools/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/sample_workload_environment.yaml)



## Congratulations! 

You have now completed the first section of the Lab.

You should have a sample workload architecture which we will use for the remainder of the lab.

 
<!-- ### 1.1. Confirm the Deployment status.

Once the application is successfully deployed, go to your [CloudFormation console](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2) and locate the stack named `walab-ops-sample-application`.

  1. Confirm that the stack is in a **'CREATE_COMPLETE'** state. 
  2. Record the following output details as it will be required later:
  3. Take note of the DNS value specified under **OutputApplicationEndpoint**  of the Outputs.

      The screenshot below shows the output from the CloudFormation stack:

      ![Section2 DNS Output](/Operations/200_Automating_operations_with_playbooks_and_runbooks/Images/section2-dns-outputs.png)

  4. Check for an email sent to the system operator and owner addresses you've specified in the build_application.sh script. This email should also be visible in the CloudFormation parameter under in the **SystemOpsNotificationEmail** and **SystemOwnerNotificationEmail**.

  5. Click `confirm subscription` on the email links to subscribe.

      ![Section2 DNS Output](/Operations/200_Automating_operations_with_playbooks_and_runbooks/Images/section2-email-confirm.png)

  {{% notice note %}}
  There will be 2 emails sent to your address, please ensure to subscribe to **both** of them.
  {{% /notice %}} 

-->

<!-- 
### 1.2. Test Workload. -->

<!-- In this section, you will be testing the encrypt API action from the deployed application. 

The application will take a JSON payload with `Name` as the identifier and `Text` key as the value of the secret message.

The application will encrypt the value under `Text` key with a designated KMS key and store the encrypted text in the RDS database with `Name` as the primary key. -->


{{< prev_next_button link_prev_url="../" link_next_url="../2_create_workload_review/" />}}
