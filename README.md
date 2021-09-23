# Appcues S3 Data Exports

Utility files and instructions for creating and managing S3 resources related to Appcues data exporting

## Using the Cloudformation template

1. Download the `cloudformation-s3-data-exports.yaml` file
1. Head over to [AWS CloudFormation](https://aws.amazon.com/cloudformation/) and click `Create Stack`.
3. Choose `Upload a template file` in the `Specify Template` section and upload the `cloudformation-s3-data-exports.yaml` file downloaded earlier and click `Next`
4. On step 2 enter a Stack Name to help you identify this CloudFormation Stack later.
5. Also on step 2, enter a BucketName.  This is where your data exports will be uploaded to. This must be unique across all AWS so something clear like `companyname-appcues-s3-data-exports` is a good starting point
6. Click `Next` past the Configure Stack Options step (no need to change anything)
7. Click `Create stack` at the bottom of the Review step (no need to change anything here either) and CloudFormation will take a bit to run, and once you see `CREATE_COMPLETE` in the status column, everything is done :+1:.
8. After everything is done, head over to [AWS S3](https://aws.amazon.com/s3/) and note the AWS Region your bucket is in.

Once the above steps are done, just let us know the BucketName you chose, AWS Region, and if you would like a custom path. For example, by default files are uploaded with date paths: `customer-bucket/YYYY/MM/DD/export-file` but you can add an additional path: `customer-bucket/**some/path/here**/YYYY/MM/DD/export-file`. A custom path is *not* necessary.
