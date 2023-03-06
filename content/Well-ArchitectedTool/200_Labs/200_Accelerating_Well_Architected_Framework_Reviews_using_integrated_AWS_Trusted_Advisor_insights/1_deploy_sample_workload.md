---
title: "Deploy Sample Workload"
menutitle: "Deploy Sample Workload"
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---


In this section, you will deploy the sample workload and AWS infrastructure resources that you will run the AWS Well-Architected Framework Review against. Once you have completed this lab, you will have a workload deployed in your AWS account with the architecture shown below.

![SampleWorkload](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/section1_sample_workload_architecture_before.png)


Follow below instructions to deploy the workload:

### 1.0. Deploy Sample Workload & Lab resources.

In this first step you will provision a [CloudFormation](https://aws.amazon.com/cloudformation/) stack that builds a sample workload along with the necessary underlying resource. You can choose the to deploy stack in one of the regions below. 

1. Click on the link below to deploy the stack. This will take you to the CloudFormation console in your account. Use `walab-wata-sample-workload` as the stack name, take the default values for all options, and create stack.

    * **us-west-2** : [here](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?stackName=walab-wata-sample-workload&templateURL=https://aws-well-architected-labs-singapore.s3.ap-southeast-1.amazonaws.com/watools/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/sample_workload_environment.yaml)
    

    * **ap-southeast-2** : [here](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/create/review?stackName=walab-wata-sample-workload&templateURL=https://aws-well-architected-labs-singapore.s3.ap-southeast-1.amazonaws.com/watools/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/sample_workload_environment.yaml)
    

    * **ap-southeast-1** : [here](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/review?stackName=walab-wata-sample-workload&templateURL=https://aws-well-architected-labs-singapore.s3.ap-southeast-1.amazonaws.com/watools/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/sample_workload_environment.yaml)



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
