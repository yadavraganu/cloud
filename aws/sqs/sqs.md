# Amazon SQS queue types
Amazon SQS supports two types of queues.  
- Standard queues
  - __Unlimited Throughput__ – Standard queues support a nearly unlimited number of API calls per second, per API action (SendMessage, ReceiveMessage, or DeleteMessage).
  - __At-Least-Once Delivery__ – A message is delivered at least once, but occasionally more than one copy of a message is delivered.
  - __Best-Effort Ordering__ – Occasionally, messages are delivered in an order different from which they were sent.
- FIFO queues
  - __High Throughput__ – If you use batching, FIFO queues support up to 3,000 messages per second, per API method (SendMessageBatch, ReceiveMessage, or DeleteMessageBatch).
      The 3,000 messages per second represent 300 API calls, each with a batch of 10 messages. To request a quota increase, submit a support request. Without batching, FIFO queues support up to 300 API calls per second, per API method (SendMessage, ReceiveMessage, or DeleteMessage).
  - __Exactly-Once Processing__ – A message is delivered once and remains available until a consumer processes and deletes it. Duplicates aren't introduced into the queue.
  - __First-In-First-Out Delivery__ – The order in which messages are sent and received is strictly preserved.

# SQS Configs
- __Visibility timeout__ - Enter the duration and units. The range is from 0 seconds to 12 hours. The default value is 30 seconds.It is the duration for which message gets hidden from other consumers when a consumer consumes message.  
- __Message retention period__ - Enter the duration and units. The range is from 1 minute to 14 days. The default value is 4 days.It is the amount of time or duration till which message will be available starting from when the message entered queue
- __Delivery delay__ - Enter the duration and units. The range is from 0 seconds to 15 minutes. The default value is 0 seconds.It is the duration for which message remains hidden from all consumers after message is published.
- __Maximum message size__ - Enter a value. The range is from 1 KB to 256 KB. The default value is 256 KB.
- __Receive message wait time__ - Enter a value. The range is from 0 to 20 seconds. The default value is 0 seconds, which sets short polling. Any non-zero value sets long polling. When a consumer tries to poll the queue to get the message if the message is there is responds quickly but if the message is not there then it waits for a certain time called receive message wait time.

# Dead Letter Queue (DLQ)
It is secondary queue which is used to store the messages which got failed while processing in main queue.So that it can be later used.We can set a number of retries after which messages comes in DLQ using __Maximum receives__ parameter/

# Redrive Allow Policy
Use to set which queue can use current queue as DLQ.
![image](https://github.com/yadavraganu/cloud/assets/77580939/b8388ed3-7229-4d0b-aea3-52d6b1b2cf89)

#boto3
### Create Queue:
```
def create_queue():
    sqs_client = boto3.client("sqs", region_name="us-west-2")
    response = sqs_client.create_queue(
        QueueName="my-new-queue",
        Attributes={
            "DelaySeconds": "0",
            "VisibilityTimeout": "60",  # 60 seconds
        }
    )
```
### Get Queue Url
```
def get_queue_url():
    sqs_client = boto3.client("sqs", region_name="us-west-2")
    response = sqs_client.get_queue_url(
        QueueName="my-new-queue",
    )
    return response["QueueUrl"]
```
### Send Message 
```
def send_message():
    sqs_client = boto3.client("sqs", region_name="us-west-2")

    message = {"key": "value"}
    response = sqs_client.send_message(
        QueueUrl="https://us-west-2.queue.amazonaws.com/xxx/my-new-queue",
        MessageBody=json.dumps(message)
    )
```
### Receive Messages
```
def receive_message():
    sqs_client = boto3.client("sqs", region_name="us-west-2")
    response = sqs_client.receive_message(
        QueueUrl="https://us-west-2.queue.amazonaws.com/xxx/my-new-queue",
        MaxNumberOfMessages=1,
        WaitTimeSeconds=10,
    )

    print(f"Number of messages received: {len(response.get('Messages', []))}")

    for message in response.get("Messages", []):
        message_body = message["Body"]
        print(f"Message body: {json.loads(message_body)}")
        print(f"Receipt Handle: {message['ReceiptHandle']}")
```
### Delete Messages
```
def delete_message(receipt_handle):
    sqs_client = boto3.client("sqs", region_name="us-west-2")
    response = sqs_client.delete_message(
        QueueUrl="https://us-west-2.queue.amazonaws.com/xxx/my-new-queue",
        ReceiptHandle=receipt_handle,
    )
```
### Delete All Messages (Purge)
```
def purge_queue():
    sqs_client = boto3.client("sqs", region_name="us-west-2")
    response = sqs_client.purge_queue(
        QueueUrl="https://us-west-2.queue.amazonaws.com/xxx/my-new-queue",
    )
    print(response)
```
