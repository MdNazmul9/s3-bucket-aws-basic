# s3-bucket-aws-basic

# step-1:
create asw s3 bucket
# step-2:
create IAM user group
# step-3:
create IAM user
# step-4:
Add user to the group
# step-5:
Download (new_user_credentials.csv) the user credentails for connecting s3 bucket with your project:
# step-6: (optional)
add policy and attach it with the group

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::myAWSBucketName",
                "arn:aws:s3:::myAWSBucketName/*"
            ]
        }
    ]
}

```
# step-7:
Attach policy with the group
# step-8: Create bucket policy (Very very Important)
Goto
```
Buckets --> myAWSBucketName --> Permissions --> Bucket policy
```
add this JSON code

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicRead",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectVersion"
            ],
            "Resource": "arn:aws:s3:::emawsbucket/*"
        }
    ]
}
```


# step-7:
Install those package: boto3==1.19.12 and django-storages==1.12.3

```
pip install boto3==1.19.12

```
```
pip install django-storages==1.12.3
```
# step-9:


