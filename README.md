## Create an SNS Topic
        Open the AWS Management Console.
        Navigate to the SNS service.
        Click Create Topic and select Standard as the topic type.
        Name the topic (e.g., gd_topic) and note the ARN.
        Click Create Topic.
## Add Subscriptions to the SNS Topic
        After creating the topic, click on the topic name from the list.
        Navigate to the Subscriptions tab and click Create subscription.
        Select a Protocol:
                For Email:
                        Choose Email.
                        Enter a valid email address.
                For SMS (phone number):
                        Choose SMS.
                        Enter a valid phone number in international format (e.g., +1234567890).
## Create the SNS Publish Policy
        Open the IAM service in the AWS Management Console.
        Navigate to Policies → Create Policy.
        Click JSON and paste the JSON policy from gd_sns_policy.json file
        Replace REGION and ACCOUNT_ID with your AWS region and account ID.
        Click Next: Tags (you can skip adding tags).
        Click Next: Review.
        Enter a name for the policy (e.g., gd_sns_policy).
        Review and click Create Policy.
## Create an IAM Role for Lambda
        Open the IAM service in the AWS Management Console.
        Click Roles → Create Role.
        Select AWS Service and choose Lambda.
        Attach the following policies:
        SNS Publish Policy (gd_sns_policy) (created in the previous step).
        Lambda Basic Execution Role (AWSLambdaBasicExecutionRole) (an AWS managed policy).
        Click Next: Tags (you can skip adding tags).
        Click Next: Review.
        Enter a name for the role (e.g., gd_role).
        Review and click Create Role.
        Copy and save the ARN of the role for use in the Lambda function.
## Deploy the Lambda Function
        Open the AWS Management Console and navigate to the Lambda service.
        Click Create Function.
        Select Author from Scratch.
        Enter a function name (e.g., gd_notifications).
        Choose Python 3.x as the runtime.
        Assign the IAM role created earlier (gd_role) to the function.
        Under the Function Code section:
        Copy the content of the src/gd_notifications.py file from the repository.
        Paste it into the inline code editor.
        Under the Environment Variables section, add the following:
        NBA_API_KEY: your NBA API key.
        SNS_TOPIC_ARN: the ARN of the SNS topic created earlier.
        Click Create Function.
## Set Up Automation with Eventbridge
        Navigate to the Eventbridge service in the AWS Management Console.
        Go to Rules → Create Rule.
        Select Event Source: Schedule.
        Set the cron schedule for when you want updates (e.g., hourly).
        Under Targets, select the Lambda function (gd_notifications) and save the rule.
## Test the System
        Open the Lambda function in the AWS Management Console.
        Create a test event to simulate execution.
        Run the function and check CloudWatch Logs for errors.
        Verify that SMS notifications are sent to the subscribed users.