# Amazon S3: Allows IAM Users Access to Their S3 Home Directory, Programmatically and In the Console<a name="reference_policies_examples_s3_home-directory-console"></a>

This example shows how you might create a policy that allows IAM users to access their own home directory bucket object in S3\. The home directory is a bucket that includes a `home` folder and folders for individual users\. This policy also grants the permissions necessary to complete this action on the console\. To use this policy, replace the red italicized text in the example policy with your own information\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:GetBucketLocation"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::bucket-name",
            "Condition": {
                "StringLike": {
                    "s3:prefix": [
                        "",
                        "home/",
                        "home/${aws:username}/*"
                    ]
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::bucket-name/home/${aws:username}",
                "arn:aws:s3:::bucket-name/home/${aws:username}/*"
            ]
        }
    ]
}
```