---
title: "(Optional) Manage Improvement Items with change management system"
menutitle: "(Optional) Manage Improvement Items with change management system"
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 4
pre: "<b>4. </b>"
---

By now, you should have completed the simulated AWS Well-Architected Framework review (WAFR) for your sample workload. This review provides you with insights and actionable items that you need to take towards improving your workload's architecture.

To ensure accountability towards these improvement action items, you need to incorporate them into your organizational process. One way to achieve this is to manage these items using a change management system.

In this section of the lab, we will walk you through a quick example of how you can take the insights and actionable items from the AWS Well-Architected Framework review and manage them in a popular change management system, Jira. You will streamline the creation and management of these actionable improvement items in Jira, using integrations made possible by AWS Well-Architected Tool APIs and AWS serverless services.

![section4_Arch](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_Arch.png)


{{% notice note %}}
**NOTE**: The steps and integration pattern in this lab section are intended to provide guidance and showcase what is possible towards activities that should be performed on improvement action items produced at the back of the AWS Well-Architected review. The code provided through this example implementation is not intended for production. Please contact aws-wa-geo-sa@amazon.com for any question.
{{% /notice %}}

### 1. Creating a Jira Software account and related resources

In this first step, we are going to create a Jira account, a new Jira Project and a Jira API Token. 

1. Create a Jira account by following this [link.](https://www.atlassian.com/try/cloud/signup?bundle=jira-software&edition=free) In the creation process, feel free to skip all the optional steps.
    
    **Important:** Take note of your Jira Site (e.g. ``https://my-site.atlassian.net/``)

2. When prompted, create a Jira project (use any name for it). If not prompted, you can always create a project from your Jira site. Just use the top navigation bar, from the "Projects" dropdown, select "Create project".

3. Once the project is created, go to the projects list page by using the top navigation bar, from the "Projects" dropdown, select "View all projects".
    
    **Important:** Take note of the Jira Project Key.

![section4_1_1_jiraprojectkey](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_1_1_jiraprojectkey.png)

4. Create a Jira API Token. Go to the [Jira Manage Profile page](https://id.atlassian.com/manage-profile/security/api-tokens) and create an API token (use any label for it).
    
    **Important:** Take note of the Jira API token.

### 2. Provision the AWS resources needed for the Well-Architected Tool and Jira integration

In this step, we will provision a [CloudFormation](https://aws.amazon.com/cloudformation/) stack that builds a Cloud9 workspace. This Cloud9 workspace will be used to build and deploy the AWS Serverless Application Model (AWS SAM) stack with the resources needed for the Well-Architected Tool and Jira integration.

1. Download the sample workload CloudFormation Template [here](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Code/walab-ta-jira-cloud9.yml).

2. Go to the CloudFormation console in the same AWS Region where you created the Well-Architect Tool Workload from [Section 2](../2_create_workload_review/#20-create-aws-well-architected-tool-workload) of this lab.
    
    Create a new stack and use the downloaded template **walab-ta-jira-cloud9.yml** as the template source.
    
    For the stack name, use ``well-architected-tool-ta-jira-lab-cloud9``.
    
    Leave any other parameters as default and create the stack.

3. Once the CloudFormation stacks completes, go to the **Outputs** tab and open the **Cloud9DevEnvUrl** link to log in to the Cloud9 workspace IDE we just created:

![section4_2_1_cfncloud9](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_1_cfncloud9.png)

4. Your environment will bootstrap the lab repository when you connect to it. Wait until it finishes, you should see a terminal output similar to this:

![section4_2_2_cloud9bootstrap](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_2_cloud9bootstrap.png)

5. In the IDE terminal console, change directory to the working folder where the script for building and deploying the SAM stack is located:

```
cd ~/environment/aws-well-architected-labs/static/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Code/scripts/
```

6. Run the **build_deploy_sam.sh** script as below. Make sure to replace the script input variables as follow:

    **JiraSiteURL** with your Jira Site (from Step 1.1 above). For example, ``https://my-site.atlassian.net/``

    **JiraUsername** with the email address you use for creating the Jira account. For example, ``myemail@example.com``

    **JiraProjectKey** with your Jira Project Key (from Step 1.3 above). For example, ``WAL``

    **EmailAddress** with your preferred email address for receiving notification about WAFR improvement action items completed. For example, ``myemail@example.com``

    Also, when prompted by the script, paste your Jira API Token (from Step 1.4 above).

```
bash build_deploy_sam.sh JiraSiteURL JiraUsername JiraProjectKey EmailAddress
```

As the SAM deployment progresses, you should have received a "Subscription Confirmation" email from SNS to confirm your subscription for getting the WAFR improvement action notifications. Click on the "Confirm subscription" link from that email to confirm the subscription.

Once the SAM deployment completes, you should see a "Successfully created/updated stack" message like below:

**Important:** From the Output section, take note of the SNS Topic ARN for Jira Automation.

![section4_2_3_cloud9scriptsuccess](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_3_cloud9scriptsuccess.png)

7. Use the SNS Topic ARN to create a Jira Automation. Go back to your Jira Site, open your Project, select "Project Settings" from the left panel and then click on "Automation":

    7.1. Click on "Create Rule" (skip the tour if prompted):

    ![section4_2_4_jiraautomationrule](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_4_jiraautomationrule.png)

    7.2. Use the trigger search box to look for the ``Issue transitioned`` trigger, and select it. Set the condition as per below image, by changing the **"To status"** value to **"DONE"** (The **"From status"** value should remain blank). Click on **Save**:

    ![section4_2_5_jiraautomationrule](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_5_jiraautomationrule.png)

    7.3. In the **"Add component"** view, select **"New condition"** and then **"Advanced compare condition"**:
    
    As **"First value"** add ``{{issue.summary}}``.

    The **"Condition"** should be set as ``starts with``.

    And **"Second value"** should be ``[WALAB]``.

    ![section4_2_6_jiraautomationrule](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_6_jiraautomationrule.png)

    7.4. In the **"Add component"** view, select **"New action"** and use the action search box to look for ``Send message to Amazon SNS``, select it. In the **"Send message to Amazon SNS topic"** configuration view, click on the **"Connect"** button and paste the **SNS Topic ARN for Jira Automation** copied from Step 2.6.

    ![section4_2_7_jiraautomationrule](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_7_jiraautomationrule.png)

    7.5. In the same **"Send message to Amazon SNS topic"** configuration view, for the **"Key-value pairs"** definition, add ``ticketId`` as the **"Key"** and ``{{issue.key}}`` as the **"Value"** (leave the value type as a **"String"**). Click on **"Save"**:

    ![section4_2_8_jiraautomationrule](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_8_jiraautomationrule.png)

    7.6. Finally, click on **"Rule details"**, then on **"Publish rule"**. Add a name to the rule and click on **"Turn it on"**:

    ![section4_2_9_jiraautomationrule](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_2_9_jiraautomationrule.png)

### 3. Managing Improvements Items with Jira as the Change Management System:

In the previous [Section 3](../3_perform_review/) of the lab, we simulated a shortened version of an AWS Well-Architected Framework Review for our sample workload by reviewing the [REL 10 question](https://wa.aws.amazon.com/wat.question.REL_10.en.html) of the Reliability pillar. Using the Well-Architected Tool, we then reviewed the Best Practices for that question as well as the Trusted Advisor checks related to them (by taking advantage of the integration between the [Well-Architected Tool and AWS Trusted Advisor](https://docs.aws.amazon.com/wellarchitected/latest/userguide/activate-ta-for-workload.html)).

For the final part of this lab, we will continue the review of those questions from the Well-Architected Tool. But this time, we will leverage the deployed SAM stack to automatically get actionable improvement items or tickets in our Jira project based on recommendation from the Well-Architected Framework and Trusted Advisor checks.

1. First, lets open again our sample workload from the Well-Architected Tool. Go to the Well-Architected Tool console page. From the **Workloads** section open your sample workload and click on **"Continue reviewing"**.

![section4_3_1_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_1_watooljiraworkflow.png)

2. Navigate again to the **Reliability** pillar on the left panel and click on the **REL 10 question**:

![section4_3_2_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_2_watooljiraworkflow.png)

3. For this example, lets assume that after conducting the review for this **REL 10** question, it was agreed (or even, was not clear) whether the first two best practices listed are followed for this sample workload. In such case, we leave those two best practices unchecked and proceed with the next question to continue with the review:

    ![section4_3_3_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_3_watooljiraworkflow.png)

    At this point, by clicking on the **"Next"** or **"Save and exit"** buttons, the SAM stack will automatically detect the updates to this question's answer. Such action will trigger the SAM stack workflow to automatically create a Jira ticket for us with more context.

4. Go to your Jira site. In your Jira project, you should now see new Jira tickets/issues that were automatically created and that are related to Trusted Advisor checks and its associated Well-Architected best practices. Notice that in this case, the SAM stack workflow detected two Trusted Advisor checks with flagged resources related to our sample workload in the workload account:

    One in relation to the Trusted Advisor check: **"Amazon EC2 Availability Zone Balance"**

    And another on for the Trusted Advisor check: **"Amazon RDS Multi-AZ"**

    Both checks are related to the [REL 10 question](https://wa.aws.amazon.com/wat.question.REL_10.en.html) best practice **"Deploy the workload to multiple locations"** (as we discussed in previous [Section 3](../3_perform_review/) of this lab)

    ![section4_3_4_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_4_watooljiraworkflow.png)

5. Open any of the issues in Jira. You will see that, as part of the description, useful information was included by the SAM stack workflow. You can see details such as resource Ids or even useful links with recommendation on how to remediate the issue. For example, for the **"Amazon RDS Multi-AZ"** ticket:

![section4_3_5_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_5_watooljiraworkflow.png)

6. Now lets open the other ticket related to **"Amazon EC2 Availability Zone Balance"**.

    If we first check the information within the **"Resources affected"** section, it is telling us that there is an Availability Zone imbalance of EC2 instances in the AWS Region where our sample workload is deployed (for this example "ap-northeast-1"). It is showing that there is only 1 instance deployed in a single Availability Zone ("ap-northeast-1a" in this case):

    ![section4_3_6_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_6_watooljiraworkflow.png)

    If we further scroll down in the ticket description, within the **"Useful link for resolution"** section, we will see a link where we can find more information about recommendation to solve this issue:

    ![section4_3_7_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_7_watooljiraworkflow.png)

    If we then open that [link](https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_fault_isolation_multiaz_region_system.html#implementation-guidance), it will take use to the **Implementation guidance** documentation for the Well-Architected Best Practice **Deploy the workload to multiple locations**. From there, we can find useful information about next actions to take:

    ![section4_3_8_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_8_watooljiraworkflow.png)

 7. Now, one of the components of [our sample workload](../1_deploy_sample_workload/) is an EC2 Auto Scaling Group. Following the recommendations from the [Distribute instances across Availability Zones](https://docs.aws.amazon.com/autoscaling/ec2/userguide/auto-scaling-benefits.html#arch-AutoScalingMultiAZ) documentation we got from the Jira ticket, we can proceed and modify our Auto Scaling Group so it is properly distributed across Availability Zones:

    ![section4_3_9_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_9_watooljiraworkflow.png)

    Go to the EC2 Auto Scaling console, select the Auto Scaling Group related to our workload and edit the **Network** settings. Make sure than more than one Availability Zone is selected:

    ![section4_3_10_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_10_watooljiraworkflow.png)

    ![section4_3_11_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_11_watooljiraworkflow.png)

    Also, we need to change the desire capacity of the Auto Scaling Group from 1 to at least 2. By doing this, the Auto Scaling Group will deploy another instance across Availability Zones, which resolves our EC2 Availability Zone imbalance issue:

    ![section4_3_12_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_12_watooljiraworkflow.png)

8. Now that we have resolved the EC2 Availability Zone imbalance problem, we can go back to the Jira ticket, add a summary of the actions taken and then we proceed to change the ticket status to **"DONE"**:

![section4_3_13_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_13_watooljiraworkflow.png)

9. Once the Jira ticket is marked as **"DONE"**, the Jira automation rule will be triggered and report back to our SAM stack. This initiates a new workflow by the SAM stack to keep track of the change and to inform us of the updates (via a SNS message email):

![section4_3_14_watooljiraworkflow](/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Images/section4_3_14_watooljiraworkflow.png)

### 4. Congratulations!

You have now completed the last section of the **Accelerating Well-Architected Framework reviews using AWS Trusted Advisor & JIRA** lab. In this section we took advantage of the integration between the AWS Well-Architected Tool and AWS Trusted Advisor in order to:

- Get insights from Trusted Advisor about what specific resources of your workload are not aligned to the best practices and;
- Use those insights, together with Well-Architected implementation guidances, to automatically create actionable items in Jira (as the change management system used in this example).

Click on the **Next Step** button below and follow the steps to cleanup the lab resources.

{{< prev_next_button link_prev_url="../3_perform_review" link_next_url="../5_cleanup/" />}}
