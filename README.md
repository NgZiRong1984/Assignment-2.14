# Assignment-2.14

Answer the following:

- Does SNS guarantee exactly once delivery to subscribers?

No, Amazon SNS does not guarantee exactly-once delivery. SNS provides at-least-once delivery, which means that a message will be delivered to a subscriber at least one time, but it may be delivered multiple times. Duplicate deliveries can occur, especially in cases of retries or network disruptions. Subscribers should implement idempotency in their applications to handle duplicate messages effectively.

- What is the purpose of the Dead-letter Queue (DLQ)? This a feature available to SQS/SNS/EventBridge.

A Dead-letter Queue (DLQ) is a feature available in services like SQS, SNS, and EventBridge. It is used to capture and store messages that were unable to be successfully processed or delivered after multiple retries.
The main purposes of a DLQ are:
- To retain undeliverable messages for troubleshooting and debugging.
- To prevent data loss by storing unprocessed messages for later analysis or reprocessing.
- To decouple error handling from the main processing flow, ensuring smoother application performance.

- How would you enable a notification to your email when messages are added to the DLQ?

-Set up an SNS Topic for Notifications:
Create an SNS topic in the AWS Management Console.
Subscribe your email address to the SNS topic. AWS will send a confirmation email; make sure to confirm the subscription.

-Configure an Amazon CloudWatch Alarm for DLQ Monitoring:
Open the CloudWatch Console.
Create a metric filter for the DLQ. For SQS-based DLQs:
Go to Metrics > SQS > Dead Letter Queue Metrics.
Look for the ApproximateNumberOfMessagesVisible metric, which tracks the number of messages in the DLQ.
Create an alarm that triggers when this metric exceeds a certain threshold (e.g., 1 message in the DLQ).

-Set the Alarm to Trigger the SNS Topic:
Configure the CloudWatch alarm to send notifications to the SNS topic when the threshold condition is met.
The SNS topic will send an email notification to the subscribed email addresses.

