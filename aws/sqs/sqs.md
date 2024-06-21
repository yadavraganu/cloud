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
## SQS Configs
- __Visibility timeout__ - Enter the duration and units. The range is from 0 seconds to 12 hours. The default value is 30 seconds.
- __Message retention period__ - Enter the duration and units. The range is from 1 minute to 14 days. The default value is 4 days.
- __Delivery delay__ - Enter the duration and units. The range is from 0 seconds to 15 minutes. The default value is 0 seconds.
- __Maximum message size__ - Enter a value. The range is from 1 KB to 256 KB. The default value is 256 KB.
- __Receive message wait time__ - Enter a value. The range is from 0 to 20 seconds. The default value is 0 seconds, which sets short polling. Any non-zero value sets long polling.
