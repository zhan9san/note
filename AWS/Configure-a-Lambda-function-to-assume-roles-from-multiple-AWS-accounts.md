# aws-sample

Inspired by [How can I configure a Lambda function to assume a role from another AWS account](https://aws.amazon.com/premiumsupport/knowledge-center/lambda-function-assume-iam-role/)

## Short description

You can give Lambda functions created in one account ("account A") permissions to assume a role from multiple accounts ("account B/C") for the following reasons:

## Resolution

If you haven't already, configure these two [AWS Identity and Access Management (IAM) roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html):

* [Execution role](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html) – The primary role in account A that gives the Lambda function permission to do its work.
* [Assumed role](https://docs.aws.amazon.com/lambda/latest/dg/access-control-identity-based.html#permissions-user-xaccount) – A role in account B/C that the Lambda function in account A assumes to gain access to cross-account resources.

Then, follow these instructions:

1. [Attach the following IAM policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html) to your Lambda function's execution role in
account A to assume the role in account B and C:

    **Note**:  
    Replace **222222222222** with the AWS account ID of account B.  
    Replace **333333333333** with the AWS account ID of account C.  
    Replace **role-on-source-account-2** with the name of the assumed role of
    account B.  
    Replace **role-on-source-account-3** with the name of the assumed role of
    account C.  

    ```json
    {
        "Version": "2012-10-17",
        "Statement": {
            "Effect": "Allow",
            "Action": "sts:AssumeRole",
            "Resource": [
                "arn:aws:iam::222222222222:role/role-on-source-account-2",
                "arn:aws:iam::333333333333:role/role-on-source-account-3"
            ]
        }
    }
    ```

2. [Modify the trust policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/roles-managingrole-editing-console.html#roles-managingrole_edit-trust-policy) of the assumed role in account B and C to the following:

    **Note**:  
    Replace **111111111111** with the AWS account ID of account A.  
    Replace **my-lambda-execution-role** with the name of the execution role.  

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::111111111111:role/my-lambda-execution-role"
                },
                "Action": "sts:AssumeRole"
            }
        ]
    }
    ```

3. [Update your Lambda function code](https://docs.aws.amazon.com/lambda/latest/dg/resource-model.html) to add the AWS Security Token Service (AWS STS) [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) API call. This call returns a set of credentials that you can use to create a service client. When using this client, your function has the permissions conferred to it by the assumed role, and acts as if it belongs to account B. For more information, see [assume_role](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/sts.html#STS.Client.assume_role) in the AWS SDK for Python (Boto 3) documentation.

    You can use the following [Python function code](https://docs.aws.amazon.com/lambda/latest/dg/python-programming-model.html) as an example for your own use case. This code is provided as-is.

    **Note**:  
    Replace **222222222222** with the AWS account ID of account B.  
    Replace **333333333333** with the AWS account ID of account C.  
    Replace **role-on-source-account-2** with the name of the assumed role of
    account B.  
    Replace **role-on-source-account-3** with the name of the assumed role of
    account C.  

    ```Python
    import boto3

    account_ids = ['222222222222', '333333333333']
    assumed_roles = ['role-on-source-account-2', 'role-on-source-account-3']


    def lambda_handler(context, event):

        for account_id, assumed_role in zip(account_ids, assumed_roles):
            sts_connection = boto3.client('sts')
            account = sts_connection.assume_role(
                RoleArn=f"arn:aws:iam::{account_id}:role/{assumed_role}",
                RoleSessionName=f"cross_acct_lambda_in_{account_id}"
            )

            ACCESS_KEY = account['Credentials']['AccessKeyId']
            SECRET_KEY = account['Credentials']['SecretAccessKey']
            SESSION_TOKEN = account['Credentials']['SessionToken']

            # create service client using the assumed role credentials, e.g. S3
            client = boto3.client(
                's3',
                aws_access_key_id=ACCESS_KEY,
                aws_secret_access_key=SECRET_KEY,
                aws_session_token=SESSION_TOKEN,
            )

        return "Hello from Lambda"

    ```
