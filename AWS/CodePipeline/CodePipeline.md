# CodePipeline Permission

S3 As Source stage ArtifactStore

Use S3 bucket, `arn:aws:s3:::src-1`, as source stage
Use S3 bucket, `arn:aws:s3:::arti-1`, as ArtifactStore

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "lambda:ListFunctions",
                "lambda:InvokeFunction"
            ],
            "Resource": "*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:GetBucketVersioning"
            ],
            "Resource": [
                "arn:aws:s3:::arti-1",
                "arn:aws:s3:::src-1"
            ]
        },
        {
            "Sid": "VisualEditor2",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:GetObjectVersion",
                "s3:DeleteObject"
            ],
            "Resource": [
                "arn:aws:s3:::arti-1/*",
                "arn:aws:s3:::src-1/*"
            ]
        }
    ]
}
```

Invoke Action Lambda Assumed role

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "logs:*"
            ],
            "Effect": "Allow",
            "Resource": "arn:aws:logs:*:*:*"
        },
        {
            "Action": [
                "codepipeline:PutJobSuccessResult",
                "codepipeline:PutJobFailureResult"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
```

CodePipeline Cloudformation Template

```yml
Resources:
  AppPipeline:
    Type: AWS::CodePipeline::Pipeline
    Properties:
      Name: pipeline-1
      RoleArn: arn:aws:iam::869233492367:role/service-role/AWSCodePipelineServiceRole-us-east-2-test
      Stages:
        - Name: stage-0
          Actions: 
            - Name: SourceAction
              ActionTypeId:
                Category: Source
                Owner: AWS
                Version: 1
                Provider: S3
              OutputArtifacts: 
                - Name: SourceOutput
              Configuration: 
                S3Bucket: src-1
                S3ObjectKey: blank
                PollForSourceChanges: false
              RunOrder: 1
        - Name: stage-1
          Actions:
            - Name: InvokeAction
              ActionTypeId: 
                Category: Invoke
                Owner: AWS
                Provider: Lambda
                Version: 1
              Configuration: 
                FunctionName: test-1
              OutputArtifacts: []
              InputArtifacts: []
              RunOrder: 2
        - Name: stage-1
          Actions:
            - Name: InvokeAction
              ActionTypeId: 
                Category: Invoke
                Owner: AWS
                Provider: Lambda
                Version: 1
              Configuration: 
                FunctionName: test-1
              OutputArtifacts: []
              InputArtifacts: []
              RunOrder: 2
      ArtifactStore:
        Type: S3
        Location: arti-1

```

Lambda Function

```Python
import boto3
import traceback

print('Loading function')
code_pipeline = boto3.client('codepipeline')

def lambda_handler(event, context):

    print(f"event: {event}, context: {context}")
    job_id = event['CodePipeline.job']['id']
    code_pipeline.put_job_success_result(jobId=job_id)
    # code_pipeline.put_job_failure_result(jobId=job_id, failureDetails={'message': 'fake_msg', 'type': 'JobFailed'})
    print("Success End")


    return "Complete."

```
