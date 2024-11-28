
Deploy
-  aws s3 mb s3://ec2-owner-tag-$Name <- Creates a new s3 bucket
-  aws cloudformation package --template-file lambda_deploy.yaml --s3-bucket ec2-owner-tag-$Name --output-template-file output.yaml <- Creates a new template with the s3 location
-  aws cloudformation deploy --stack-name ec2-owner-tag --template-file output.yaml --capabilities CAPABILITY_IAM <- Deploy the function

Destroy
- CURRENT_ACCOUNT=$(aws sts get-caller-identity --query Account --output text)
- aws s3 rm --recursive s3://ec2-owner-tag-$Name
- aws cloudformation delete-stack --stack-name ec2-owner-tag-$Name
- aws s3 rb s3://ec2-owner-tag-$Name --force