WCP AWS Debug Application

#### Create the package artifacts for your application
---
> `./1-local-build-layer.sh`

##### Prerequisite: Consider you want to create a new stack for QA. Following properties to be changed prior to running the script.

1. Save as parameters-dev.properties with new name, e.g. > parameters-qa.properties
2. Update following properties in parameters-qa.properties <br/>
2.1 stage="dev" to stage="qa" (Note: "dev", "staging" and "prod" are reserved words) <br/>
3. Create S3 bucket "wcp-debug-backend-qa" from AWS console
5. Configure 'wcp-debug' aws profile in your local environment if not available by executing `aws configure --profile wcp-debug`
#
#### Create the package

##### sam package --template-file stack-main.yaml --output-template-file package.yml --s3-bucket BUCKET_NAME --profile AWS_PROFILE
<br>

##### e.g. *sam package --template-file stack-main.yaml --output-template-file package.yml --s3-bucket wcp-debug-backend-qa --profile wcp-debug*
<br>

#### Deploy the SAM app

##### sam deploy --template-file package.yml --stack-name STACK_NAME --capabilities CAPABILITY_IAM CAPABILITY_AUTO_EXPAND --region us-east-1 --parameter-overrides $(cat parameters-STACK.properties) --profile AWS_PROFILE
<br>

##### e.g. *sam deploy --template-file package.yml --stack-name wcp-debug-backend-qa --capabilities CAPABILITY_IAM CAPABILITY_AUTO_EXPAND --region us-east-1 --parameter-overrides $(cat parameters-eic.properties) --profile wcp-debug*