## SAM minimal template
The smallest python SAM template you can get away with, including IAM policy for API gateway & Lambda. You will run into permissions issues if you add more resource dependencies & events.

Substitutions:
* $YOUR_STACK_NAME - Stack name as defined in samconfig.toml
* $YOUR_DEPLOY_BUCKET - Deployment bucket as defined in samconfig.toml, must already exist and have versioning enabled.
* $ACCOUNT - Your AWS account ID
* MyFunction - Your function name; add more ARNs for more functions.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "SAMDeployPolicy",
            "Effect": "Allow",
            "Action": [
                "apigateway:DELETE",
                "apigateway:GET",
                "apigateway:PATCH",
                "apigateway:POST",
                "apigateway:PUT",
                "apigateway:UpdateRestApiPolicy",
                "cloudformation:CreateChangeSet",
                "cloudformation:DescribeChangeSet",
                "cloudformation:DescribeStackEvents",
                "cloudformation:DescribeStacks",
                "cloudformation:ExecuteChangeSet",
                "cloudformation:GetTemplate",
                "cloudformation:GetTemplateSummary",
                "iam:AttachRolePolicy",
                "iam:CreateRole",
                "iam:DeleteRole",
                "iam:DetachRolePolicy",
                "iam:GetRole",
                "iam:PassRole",
                "iam:TagRole",
                "iam:UntagRole",
                "lambda:AddPermission",
                "lambda:CreateFunction",
                "lambda:DeleteFunction",
                "lambda:GetFunction",
                "lambda:GetFunctionConfiguration",
                "lambda:ListTags",
                "lambda:UpdateFunctionCode",
                "lambda:UpdateFunctionConfiguration",
                "s3:GetObject",
                "s3:ListBucket",
                "s3:PutObject",
                "apigateway:SetWebACL"
            ],
            "Resource": [
                "arn:aws:apigateway:*::*",
                "arn:aws:s3:::$YOUR_DEPLOY_BUCKET/*",
                "arn:aws:s3:::$YOUR_DEPLOY_BUCKET",
                "arn:aws:lambda:*:$ACCOUNT:function:$YOUR_STACK_NAME-MyFunction*",
                "arn:aws:iam::$ACCOUNT:role/$YOUR_STACK_NAME-MyFunctionRole-*",
                "arn:aws:cloudformation:*:aws:transform/Serverless-2016-10-31",
                "arn:aws:cloudformation:*:$ACCOUNT:stack/$YOUR_STACK_NAME/*"
            ]
        }
    ]
}
```