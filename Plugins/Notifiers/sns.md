# *SNS*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; SNS can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>

This is a provides the ability for FlexGet to send notifications via [Amazon SNS](https://aws.amazon.com/sns/).

SNS is a notification delivery system that can be connected to email, SMS, or other programmatic message delivery methods.

## Installation Requirements
In addition to FlexGet, you must install the boto3 AWS SDK using pip:

```bash
pip install boto3
```

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**sns_topic_arn**|text|SNS Topic ARN. **Required**
|**aws_region**|text|AWS Region. **Required**
|aws_access_key_id|text|AWS access key ID. Will be taken from AWS_ACCESS_KEY_ID environment if not provided|
|aws_secret_access_key|text|AWS secret access key
|profile_name|text|If provided, use this profile name instead of the default


The AWS access credentials can be configured in the same way as is used by the [Boto3](https://aws.amazon.com/sdk-for-python/) connection library. Either provide the configuration in the config file (risky, but it works) or set it in the environment using the documented environment variables.

The SNS topic ARN can be found on the AWS console or via the AWS SDK. For more details, read the [AWS SNS documentation](http://aws.amazon.com/documentation/sns/)