# Say_It_AI

### Project Description:

This project leverages various AWS services to convert written text into lifelike speech. Utilizing Amazon Polly, a powerful text-to-speech service, the application transforms text into natural-sounding audio in multiple languages and voices. The project employs AWS Lambda for serverless computing, ensuring scalability and efficiency without the need for server management.

### Key Features:

* Real-time Conversion: Provides fast and responsive text-to-speech conversion.
* Offline Playback: Stores audio files in formats like MP3 for offline use.
* Scalable and Serverless: Utilizes AWS Lambda for seamless scalability and reduced operational overhead.

### Use Cases:

* Accessibility: Converts written content into audio for visually impaired users. \
* Learning: Allows users to listen to educational material, enhancing the learning experience. \
* Content Distribution: Provides an additional format for consuming content, boosting audience engagement. \
* Convenience: Lets users listen to articles or books while multitasking, such as during commutes or workouts.

### Steps to Build the Project:

* Step 1: Set Up an AWS Account 
* Step 2: Create two S3 Buckets (Source S3 Bucket Name: aws-polly-source-bucket, Destination S3 Bucket Name: aws-polly-destination-bucket) 
* Step 3: Create an IAM Policy (IAM Policy Name: aws-polly-lambda-policy) \
  Policy Defination:

  ```bash
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": [
                "arn:aws:s3:::aws-polly-source-bucket/*",
                "arn:aws:s3:::aws-polly-destination-bucket/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "polly:SynthesizeSpeech"
            ],
            "Resource": "*"
        }
    ]
  }

* Step 4: Create an IAM Role (IAM Role Name: aws-polly-lambda-role) and attach aws-polly-lambda-policy and AWSLambdaBasicExecutionRole Policies
* Step 5: Create and Configure the Lambda Function (Lambda Function Name: TextToSpeechFunction)
  - Set the runtime to Python 3.8.
  - Set the execution role with necessary permissions for S3 and Polly. (Step 4)
  - Add Environment Variables (`SOURCE_BUCKET`: Name of your source S3 bucket and `DESTINATION_BUCKET`: Name of your destination S3 bucket.
* Step 6: Configure S3 Event Notification
  - Set up an event notification in the source S3 bucket to trigger the Lambda function on new object creation events with the `.txt` suffix.
* Step 7: Write Lambda Function Code 
* Step 8: Test the System
