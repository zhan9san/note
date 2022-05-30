# AWS SAM

* Unless function handlers share code, split them into their own independent Lambda function files or binaries.
  * Another option is to use language-specifi packages to share common code between functions
* Unless independent Lambda functions share event sources, split them into their own code repositories with their own AWS SAM templates
* Locally lint and validate your YAML or JSON SAM files before committing them. Then do it again in your CI/CD process.
