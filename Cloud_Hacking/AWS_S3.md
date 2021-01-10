## Introduction

- AWS S3 bucket is a commonly used Cloud Service to host website. Poorly misconfigured Cloud creates serious security issues to websites.

## What is S3 Bucket

- AWS S3 bucket has its unique URL and normally look like ```https://bucket-name.s3.Region.amazonaws.com/```. An example is like ```https://my-bucket.s3.us-west-2.amazonaws.com/puppy.png```;

## Check for data-leakage of S3 Bucket

- Some AWS S3 bucket might be publicly assessable due to poorly configured. To acccess S3 bucket, you can download a aws CLI python script by:

```
pip install aws-cli
aws configure
```

- In configuration, it would ask you for your own aws key. You can make one by registering in aws.

- Then can try some command:

```
aws s3 ls s3://whateverbucketname #list what is inside the bucket

aws s3 cp s3://whateverbucketname/secret.txt # Download file from bucket

aws s3 mv Exploit.txt s3://whateverbucketname/ # Upload file to bucket
```



