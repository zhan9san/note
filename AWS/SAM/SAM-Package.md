# Package

`sam package --template-file template.yaml --output-template-file packaged.yaml --s3-bucket ej-mw-us-west-2`

It creates zip of your code and dependencies and uploads it to S3 for other package types. The command returns a copy of your template, replacing references to local artifacts with the AWS location where the command uploaded the artifacts.

`sam deploy --template-file packaged.yaml --stack-name aws-sam-ocr-test --capabilities CAPABILITY_IAM`
