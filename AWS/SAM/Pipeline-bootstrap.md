# sam pipeline bootstrap

Create AWS infrastructure resource

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
Enter the pipeline IAM user ARN if you have previously created one, or we will create one for you []:

[3] Reference application build resources
Enter the pipeline execution role ARN if you have previously created one, or we will create one for you []:
Enter the CloudFormation execution role ARN if you have previously created one, or we will create one for you []:
Please enter the artifact bucket ARN for your Lambda function. If you do not have a bucket, we will create one for you []:
Does your application contain any IMAGE type Lambda functions? [y/N]: N

[4] Summary
Below is the summary of the answers:
	1 - Account: 869233492367
	2 - Stage name: stg-1
	3 - Region: us-west-2
	4 - Pipeline user: [to be created]
	5 - Pipeline execution role: [to be created]
	6 - CloudFormation execution role: [to be created]
	7 - Artifacts bucket: [to be created]
	8 - ECR image repository: [skipped]
Press enter to confirm the values above, or select an item to edit the value:

This will create the following required resources for the 'stg-1' environment:
	- Pipeline IAM user
	- Pipeline execution role
	- CloudFormation execution role
	- Artifact bucket
Should we proceed with the creation? [y/N]: y

	Looking for resources needed for deployment: Not found.
	Creating the required resources...
	Successfully created!
The following resources were created in your account:
	- Pipeline IAM user
	- Pipeline execution role
	- CloudFormation execution role
	- Artifact bucket
Pipeline IAM user credential:
	AWS_ACCESS_KEY_ID: AKIA4UYS2QGHTT4CDH66
	AWS_SECRET_ACCESS_KEY: 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
View the definition in .aws-sam/pipeline/pipelineconfig.toml,
run sam pipeline bootstrap to generate another set of resources, or proceed to
sam pipeline init to create your pipeline configuration file.

Before running sam pipeline init, we recommend first setting up AWS credentials
in your CI/CD account. Read more about how to do so with your provider in
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-generating-example-ci-cd-others.html.
```
