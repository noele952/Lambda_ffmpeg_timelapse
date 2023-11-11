# Time Lapse Lambda Function

This Lambda function creates a time-lapse video from a series of images stored in an Amazon S3 bucket. It requires ffmpeg installed as an executable in an attached Lambda layer. The images should be named with a Unix timestamp at the end of the filename.

## Configuration

Before deploying the Lambda function, make sure to set the following configuration values at the top of the script:

```python
S3_BUCKET = 'your-s3-bucket-name'
INPUT_PREFIX = 'input-folder/'
OUTPUT_PREFIX = 'output-folder/'
FRAMES_PER_SECOND = 5
FILE_EXTENSION = 'jpg'  # Compatible extensions: jpg, jpeg, png, gif, bmp, tiff, tif, webp
```

**Configuration:**

- _S3_BUCKET:_ The name of your Amazon S3 bucket containing the time-lapse images.
- _INPUT_PREFIX:_ The prefix of the folder within the bucket where the images are stored.
- _OUTPUT_PREFIX:_ The prefix for the folder where the output time-lapse video will be stored.
- _FRAMES_PER_SECOND:_ The desired frames per second for the time-lapse video.
- _FILE_EXTENSION:_ Compatible image file extension

**Deploying the Lambda Function:**

1. Create a new Lambda function in the AWS Management Console.
2. Upload your deployment package, which includes the script with the configuration values.
3. Configure the Lambda function with an appropriate IAM role and runtime (Python 3.8 or later).
4. Set environment variables for any sensitive information or additional configuration.

## Usage

Once deployed, the Lambda function can be triggered automatically based on various events in the S3 bucket.

### Trigger Options

#### Time Interval

You can set up an AWS CloudWatch Events rule to trigger the Lambda function at a specific time interval. For example, you might want to create a rule that triggers the Lambda function every hour or once a day.

#### Image Count Threshold

Alternatively, you can configure the Lambda function to be triggered when a certain number of images are added to the S3 bucket. Set up an S3 event trigger that activates the Lambda function when new images are uploaded, and define a threshold for the number of images required to trigger the function.

### How to Set Up Triggering

1. **AWS CloudWatch Events Rule:**

   - Go to the AWS Management Console and navigate to CloudWatch.
   - Create a new rule with a schedule expression to define the time interval.
   - Add the Lambda function as the target for the rule.

2. **S3 Event Trigger:**
   - Navigate to the S3 bucket in the AWS Management Console.
   - Configure an event for object creation.
   - Set the Lambda function as the destination for the event.
   - Optionally, configure the event to trigger based on a specific prefix or file extension.

By leveraging these triggering options, the time-lapse video will be created automatically based on your specified conditions.

## License

This DynamoDB Picture Assembly System is licensed under the [MIT License](LICENSE).
