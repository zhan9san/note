# Pipeline

`sam pipeline bootstrap` creates

1. the pipeline IAM user ARN
2. the pipeline execution role ARN
3. the CloudFormation execution role ARN
4. the artifact bucket ARN for your Lambda function

## `sam pipeline bootstrap`

```bash
$ sam pipeline bootstrap

sam pipeline bootstrap generates the required AWS infrastructure resources to connect
to your CI/CD system. This step must be run for each deployment stage in your pipeline,
prior to running the sam pipeline init command.

We will ask for [1] stage definition, [2] account details, and
[3] references to existing resources in order to bootstrap these pipeline resources.

[1] Stage definition
Enter a name for this stage. This will be referenced later when you use the sam pipeline init command:
Stage name: stg-1

[2] Account details
The following AWS credential sources are available to use:
To know more about configuration AWS credentials, visit the link below:
https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html
	1 - Environment variables (not available)
	2 - default (named profile)
	q - Quit and configure AWS credentials
Select a credential source to associate with this stage: 2
Associated account 869233492367 with stage stg-1.

Enter the region in which you want these resources to be created [us-east-1]: us-west-2
Enter the pipeline IAM user ARN if you have previously created one, or we will create one for you []: iam-user-arn-1

[3] Reference application build resources
Enter the pipeline execution role ARN if you have previously created one, or we will create one for you []: pipeline-execution-role-arn-1
Enter the CloudFormation execution role ARN if you have previously created one, or we will create one for you []: cfn-execution-role-arn-1
Please enter the artifact bucket ARN for your Lambda function. If you do not have a bucket, we will create one for you []: artifact-bucket-1
Does your application contain any IMAGE type Lambda functions? [y/N]: N

[4] Summary
Below is the summary of the answers:
	1 - Account: 869233492367
	2 - Stage name: stg-1
	3 - Region: us-west-2
	4 - Pipeline user ARN: iam-user-arn-1
	5 - Pipeline execution role ARN: pipeline-execution-role-arn-1
	6 - CloudFormation execution role ARN: cfn-execution-role-arn-1
	7 - Artifacts bucket ARN: artifact-bucket-1
	8 - ECR image repository: [skipped]
Press enter to confirm the values above, or select an item to edit the value:


All required resources for the stg-1 environment exist, skipping creation.
View the definition in .aws-sam/pipeline/pipelineconfig.toml,
run sam pipeline bootstrap to generate another set of resources, or proceed to
sam pipeline init to create your pipeline configuration file.
```

```bash
$ cat .aws-sam/pipeline/pipelineconfig.toml
version = 0.1
[default]
[default.pipeline_bootstrap]
[default.pipeline_bootstrap.parameters]
pipeline_user = "iam-user-arn-1"

[stg-1]
[stg-1.pipeline_bootstrap]
[stg-1.pipeline_bootstrap.parameters]
pipeline_execution_role = "pipeline-execution-role-arn-1"
cloudformation_execution_role = "cfn-execution-role-arn-1"
artifacts_bucket = ""
image_repository = ""
region = "us-west-2"

[stg-2]
[stg-2.pipeline_bootstrap]
[stg-2.pipeline_bootstrap.parameters]
pipeline_execution_role = "pipeline-execution-role-arn-2"
cloudformation_execution_role = "cfn-execution-role-arn-2"
artifacts_bucket = ""
image_repository = ""
region = "us-west-2"

[stg-3]
[stg-3.pipeline_bootstrap]
[stg-3.pipeline_bootstrap.parameters]
pipeline_execution_role = "pipeline-execution-role-arn-3"
cloudformation_execution_role = "cfn-execution-role-arn-3"
artifacts_bucket = ""
image_repository = ""
region = "us-west-2"
```

## `sam pipeline init`

```bash
$ sam pipeline init

sam pipeline init generates a pipeline configuration file that your CI/CD system
can use to deploy serverless applications using AWS SAM.
We will guide you through the process to bootstrap resources for each stage,
then walk through the details necessary for creating the pipeline config file.

Please ensure you are in the root folder of your SAM application before you begin.

Select a pipeline structure template to get started:
Select template
	1 - AWS Quick Start Pipeline Templates
	2 - Custom Pipeline Template Location
Choice: 1

Cloning from https://github.com/aws/aws-sam-cli-pipeline-init-templates.git
Unable to download updated app pipeline templates, using existing ones
CI/CD system
	1 - Jenkins
	2 - GitLab CI/CD
	3 - GitHub Actions
	4 - AWS CodePipeline
Choice: 4
You are using the 2-stage pipeline template.
 _________    _________
|         |  |         |
| Stage 1 |->| Stage 2 |
|_________|  |_________|

Checking for existing stages...

What is the Git provider?
	1 - Bitbucket
	2 - CodeCommit
	3 - GitHub
	4 - GitHubEnterpriseServer
Choice []: 2
What is the CodeCommit repository name?: code-commit-repo-1
What is the Git branch used for production deployments? [main]:
What is the template file path? [template.yaml]:
We use the stage name to automatically retrieve the bootstrapped resources created when you ran `sam pipeline bootstrap`.

Here are the stage names detected in .aws-sam/pipeline/pipelineconfig.toml:
	1 - stg-1
	2 - stg-2
	3 - stg-3
What is the name of stage 1 (as provided during the bootstrapping)?
Select an index or enter the stage name: 1
What is the sam application stack name for stage 1? [sam-app]:
Stage 1 configured successfully, configuring stage 2.

Here are the stage names detected in .aws-sam/pipeline/pipelineconfig.toml:
	1 - stg-1
	2 - stg-2
	3 - stg-3
What is the name of stage 2 (as provided during the bootstrapping)?
Select an index or enter the stage name: 2
What is the sam application stack name for stage 2? [sam-app]:
Stage 2 configured successfully.

To deploy this template and connect to the main git branch, run this against the leading account:
`sam deploy -t codepipeline.yaml --stack-name <stack-name> --capabilities=CAPABILITY_IAM`.
SUMMARY
We will generate a pipeline config file based on the following information:
	What is the Git provider?: CodeCommit
	What is the CodeCommit repository name?: code-commit-repo-1
	What is the Git branch used for production deployments?: main
	What is the template file path?: template.yaml
	What is the name of stage 1 (as provided during the bootstrapping)?
Select an index or enter the stage name: 1
	What is the sam application stack name for stage 1?: sam-app
	What is the pipeline execution role ARN for stage 1?: pipeline-execution-role-arn-1
	What is the CloudFormation execution role ARN for stage 1?: cfn-execution-role-arn-1
	What is the S3 bucket name for artifacts for stage 1?:
	What is the ECR repository URI for stage 1?:
	What is the AWS region for stage 1?: us-west-2
	What is the name of stage 2 (as provided during the bootstrapping)?
Select an index or enter the stage name: 2
	What is the sam application stack name for stage 2?: sam-app
	What is the pipeline execution role ARN for stage 2?: pipeline-execution-role-arn-2
	What is the CloudFormation execution role ARN for stage 2?: cfn-execution-role-arn-2
	What is the S3 bucket name for artifacts for stage 2?:
	What is the ECR repository URI for stage 2?:
	What is the AWS region for stage 2?: us-west-2
Successfully created the pipeline configuration file(s):
	- codepipeline.yaml
	- assume-role.sh
	- pipeline/buildspec_unit_test.yml
	- pipeline/buildspec_build_package.yml
	- pipeline/buildspec_integration_test.yml
	- pipeline/buildspec_feature.yml
	- pipeline/buildspec_deploy.yml
```


## Codepipeline template

### Donot understand this snippet

CodeBuildServiceRole

```yml
          PolicyDocument:
            Version: "2012-10-17"
            Statement:
              - Action:
                  - sts:AssumeRole
                Effect: Allow
                Resource: "*"
                Condition:
                  StringEquals:
                    aws:ResourceTag/Role: pipeline-execution-role
```

PipelineStackCloudFormationExecutionRole

```yml
      Policies:
        - PolicyName: GrantCloudFormationFullAccess
          PolicyDocument:
            Version: 2012-10-17
            Statement:
              - Effect: Allow
                Action: '*'
                Resource: '*'
```

ocr_demo

PipelineStackCloudFormationExecutionRole

```yml
        ManagedPolicyArns:
          - 'arn:aws:iam::aws:policy/AdministratorAccess'
```
