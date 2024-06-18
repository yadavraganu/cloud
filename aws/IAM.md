# Resource Based Access Control Policies
Resource-based policies are attached to a resource. For example, you can attach resource-based policies to Amazon S3 buckets, Amazon SQS queues, VPC endpoints, AWS Key Management Service encryption keys, and Amazon DynamoDB tables and streams.  
With resource-based policies, you can specify who has access to the resource and what actions they can perform on it. Resource-based policies are inline only, not managed.
```
{
  "Version": "2012-10-17",
  "Id": "default",
  "Statement": [
    {
      "Sid": "s3-event-cezary_for_lambda-s3",
      "Effect": "Allow",
      "Principal": {
        "Service": "s3.amazonaws.com"
      },
      "Action": "lambda:InvokeFunction",
      "Resource": "arn:aws:lambda:eu-west-1:1234567890:function:lambda-s3",
      "Condition": {
        "StringEquals": {
          "AWS:SourceAccount": "1234567890:"
        },
        "ArnLike": {
          "AWS:SourceArn": "arn:aws:s3:::test-bucket-cezary"
        }
      }
    }
  ]
}
```
# Identity Based Access Control Policies
Identity-based policies are attached to an IAM user, group, or role. These policies let you specify what that identity can do (its permissions). For example, you can attach the policy to the IAM user named John, stating that he is allowed to perform the Amazon EC2 RunInstances action.
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListObjectsInBucket",
            "Effect": "Allow",
            "Action": ["s3:ListBucket"],
            "Resource": ["arn:aws:s3:::bucket-name"]
        },
        {
            "Sid": "AllObjectActions",
            "Effect": "Allow",
            "Action": "s3:*Object",
            "Resource": ["arn:aws:s3:::bucket-name/*"]
        }
    ]
}
```
