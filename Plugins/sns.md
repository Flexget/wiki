---
title: sns
description: 
published: true
date: 2022-09-18T05:13:19.637Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:13:17.013Z
---

# SNS
## Overview
This is a provides the ability for FlexGet to send notifications via [Amazon SNS](https://aws.amazon.com/sns/).

SNS is a notification delivery system that can be connected to email, SMS, or other programmatic message delivery methods.

## Installation Requirements
In addition to FlexGet, you must install the boto3 AWS SDK using pip:

```
pip install boto3
```

## Configuration Options
```
notify_sns:
  [aws_access_key_id: <AWS ACCESS KEY ID>] (will be taken from AWS_ACCESS_KEY_ID environment if not provided)
  [aws_secret_access_key: <AWS SECRET ACCESS KEY>] (will be taken from AWS_SECRET_ACCESS_KEY environment if not provided)
  [profile_name: <AWS PROFILE NAME>] (If provided, use this profile name instead of the default.)
  aws_region: <REGION>
  sns_topic_arn: <SNS ARN>
  [sns_notification_template: <TEMPLATE] (defaults to DEFAULT_TEMPLATE_VALUE)
```

The AWS access credentials can be configured in the same way as is used by the [Boto3](https://aws.amazon.com/sdk-for-python/) connection library. Either provide the configuration in the config file (risky, but it works) or set it in the environment using the documented environment variables.

The SNS topic ARN can be found on the AWS console or via the AWS SDK. For more details, read the [AWS SNS documentation](http://aws.amazon.com/documentation/sns/)