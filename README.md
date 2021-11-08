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


# step-9:
Install those package: boto3==1.19.12 and django-storages==1.12.3

```
pip install boto3==1.19.12

```
```
pip install django-storages==1.12.3
```
# step-10:
add code settings.py
```
INSTALLED_APPS = [
    #...
    'storages', # new
]
```
```

# ======================== S3 bucket setup start================
# STATIC_ROOT = ''
# STATIC_URL = '/static/'
# STATICFILES_DIRS = (os.path.join('static'), )


AWS_ACCESS_KEY_ID = 'AWS_ACCESS_KEY_ID_AFTER_CREATE_IAM_USER'
AWS_SECRET_ACCESS_KEY = 'AWS_SECRET_ACCESS_KEY_AFTER_CREATE_IAM_USER'
AWS_STORAGE_BUCKET_NAME = 'MyBucketName'
AWS_S3_CUSTOM_DOMAIN = '%s.s3.amazonaws.com' % AWS_STORAGE_BUCKET_NAME
AWS_S3_OBJECT_PARAMETERS = {'CacheControl': 'max-age=86400'}
AWS_DEFAULT_ACL = 'public-read'

AWS_LOCATION = 'static'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]

STATIC_URL = 'https://%s/%s/' % (AWS_S3_CUSTOM_DOMAIN, AWS_LOCATION)
STATICFILES_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
DEFAULT_FILE_STORAGE = 'core.storages.MediaStore'

# MEDIA_URL = '/media/'
# MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

# =========== S3 bucket setup end================

```
# step-11:
create ```storages.py``` as project level where setings.py exists and add this code:
```
from storages.backends.s3boto3 import S3Boto3Storage


class MediaStore(S3Boto3Storage):
    location = 'media'
    file_overwrite = False

```
# step-12:
your Bucket looks like:

```
MyBucketName
    |
    |-media
    |-static

```
[Note] If you want to use existing media and static files upload it in your bucket 
# step-13:
Now run your project.

If you fetch any issue contact me.

Have a good day.


