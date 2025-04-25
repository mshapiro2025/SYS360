# AWS CloudTrail

## Lecture Notes: CloudTrail

* an AWS service that helps you enable governance, compliance, and operational and risk auditing of your AWS account
  * actions taken by a user, rule, or an AWS service are recorded as events in CloudTrail
  * events include actions taken in the AWS Management Console, AWS CLI, and AWS SDKs and APIs
  * logging for AWS console actions, not for the AWS instances
* CloudTrail is enabled on your AWS account when you create it
  * when activity occurs in your AWS account, that activity is recorded in a CloudTrail event
  * you can easily view recent events in the CloudTrail console by going to Event History
  * for an ongoing record of activity and events in your AWS account, create a trail

### Why Use CloudTrail?

* use CloudTrail to view, search, download, archive, analyze, and respond to account activity across your AWS infrastructure
* can identify:
  * who took which action
  * what resources were acted upon
  * when the event occurred
* helps you analyze and respond to activity in your AWS account
* optionally, you can enable AWS CloudTrail Insights on a trail to help you identify and respond to unusual activity
  * insights detect anomalous actions

### Use Cases

* compliance aid
  * AWS CloudTrail makes it easier to ensure compliance with internal policies and regulatory standards by providing a history of activity in your AWS account
* operational issue troubleshooting
  * ex. can quickly identify the most recent changes made to resources in your environment, including creation, modification, and deletion of AWS resources (ex. EC2 instances, VPC security groups, and EBS volumes
* security analysis
  * can detect user behavior patterns by ingesting AWS CloudTrail events in to your log management and analytics solutions
* data exfiltration
  * detect data exfil by collecting activity data on S3 objects through API events recorded in CloudTrail
  * after the activity data is collected, other AWS services like CloudWatch Events and AWS Lambda can trigger response procedures
* unusual activity detection
  * detect unusual activity in AWS accounts with CloudTrail Insights
  * ex. can quickly alert and act on operational issues such as erroneous spikes in resource provisioning or services hitting rate limits

### Configuring CloudTrail

* can be configured through the AWS CloudTrail console
  * can also use the S3 console to access buckets containing logs
  * can also use the CloudWatch console if integrated
