# Appcues S3 Data Exports

Utility files and instructions for creating and managing S3 resources related to Appcues data exporting

## Using the Cloudformation template

1. Download the `cloudformation-s3-data-exports.yaml` file
1. Head over to [AWS CloudFormation](https://aws.amazon.com/cloudformation/) and click `Create Stack`.
1. Choose `Upload a template file` in the `Specify Template` section and upload the `cloudformation-s3-data-exports.yaml` file downloaded earlier and click `Next`
1. On step 2 enter a Stack Name to help you identify this CloudFormation Stack later.
1. Also on step 2, enter a BucketName. This is where your data exports will be uploaded to. This must be unique across all AWS so something clear like `companyname-appcues-s3-data-exports` is a good starting point
1. Click `Next` past the Configure Stack Options step (no need to change anything)
1. Click `Create stack` at the bottom of the Review step (no need to change anything here either) and CloudFormation will take a bit to run, and once you see `CREATE_COMPLETE` in the status column, everything is done :+1:.
1. After everything is done, head over to [AWS S3](https://aws.amazon.com/s3/) and note the AWS Region your bucket is in.

Once the above steps are done, just let us know the BucketName you chose, AWS Region, and if you would like a custom path. For example, by default files are uploaded with date paths: `customer-bucket/YYYY/MM/DD/export-file` but you can add an additional path: `customer-bucket/**some/path/here**/YYYY/MM/DD/export-file`. A custom path is _not_ necessary.

## I already have a bucket that I wish to use or I am unable to create one

If you are unwilling/unable to create a new bucket and/or wish to use an existing bucket, please ensure the following bucket-policy has been applied to that bucket:

```json
{
  "Version": "2008-10-17",
  "Statement": [
    {
      "Sid": "GrantPutObjectToAppcues",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::121185820226:root"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME-GOES-HERE/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "bucket-owner-full-control"
        }
      }
    }
  ]
}
```

As shown, you will retain all ownership of objects placed in this bucket via this policy. Appcues cannot delete objects we place there.
