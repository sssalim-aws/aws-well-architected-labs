---
title: "Teardown"
date: 2021-08-31T11:16:09-04:00
chapter: false
pre: "<b>5. </b>"
weight: 5
---

The following instructions will remove the resources that you have created in this lab.

#### Cleaning up Sample Workload Resources

1. Follow the instructions in these links to Delete the [StackSet Instances](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stackinstances-delete.html) and [StackSet]https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-delete.html) of your `walab-wata-sample-workload`

2. Follow the instructions [here](https://docs.aws.amazon.com/wellarchitected/latest/userguide/workloads-delete.html) to delete the Well-Architected Tool Workload.

#### Cleaning up SAM stack

1. Go back to the AWS Cloud9 console and connect again to the Cloud9 IDE terminal, change directory to the working folder where the script for building and deploying the SAM stack is located:

```
cd ~/environment/aws-well-architected-labs/static/watool/200_Running_WAFR_using_Trusted_Advisor_Integration/Code/scripts/
```

2. Run the **section4_cleanup_resources.sh** script as below:

```
bash section4_cleanup_resources.sh
```

#### Revoke the Jira API Token you have explicitly created for this workshop

**Important**: Only follow below step if you have explicitly created a Jira API Token to be used for this lab. If you have used one of your existing ones (e.g. if you already had a Jira account), there is no need to revoke it.

1. Open the [Jira API Tokens configuration page](https://id.atlassian.com/manage-profile/security/api-tokens).

2. Click on the **Revoke** button next to the token you created for this workshop.


### Thank you for using this lab.
