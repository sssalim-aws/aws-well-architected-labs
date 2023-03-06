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

1. Sign in to the AWS Management Console using your root account credentials.
2. Navigate to the AWS Organizations console.
3. Click on the "Get started" button to enable AWS Organizations.
4. Select "Enable all features" and click on "Next".
5. Review the information on the next screen and click on "Create organization".
6. Once your organization is created, navigate to the "Organize accounts" page.
7. Click on "Create Organizational Unit".
8. Enter "Workload" as the name of the OU and click on "Create".
9. Navigate to the "Accounts" tab and click on "Create account".
10. Enter the email address "hula@hula.com" and other required details for the new account.
11. Choose a password for the new account and click on "Create account".
12. AWS will send an email to the email address specified in step 10.
13. Follow the instructions in the email to complete the account setup.
14. Once the account setup is complete, the new account will appear under the "Accounts" tab.
15. Select the account and click on "Move account".
16. Choose the "Workload" OU as the destination and click on "Move".
17. The account is now in the "Workload" OU.

### 2.0. Configure AWS CloudFormation StackSet.

1.  Open the AWS CloudFormation console.
2.  Choose "StackSets" from the left-hand menu.
3.  Click on "Create StackSet".
4.  In the "StackSet Details" section, give your StackSet a name, description, and choose a template source.
5.  In the "Deployment options" section, select "AWS Organizations" as the deployment target.
6.  In the "Permissions" section, specify the permissions required to deploy your StackSet.
7.  Click on "Next" to proceed to the "StackSet Settings" section.
8.  In the "StackSet Settings" section, select "Enable AWS Organizations" and choose the AWS Organizations entity to deploy your StackSet to.
9.  Click on "Next" to proceed to the "Review" section.
10. Review your StackSet configuration and click on "Create StackSet".
11. Once your StackSet is created, you can deploy it to the AWS accounts in your organization by creating a StackSet instance.


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
