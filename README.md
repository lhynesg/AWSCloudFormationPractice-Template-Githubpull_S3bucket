
## My Code Explanation

AWSTemplateformatVersion: 2018-09-09
Description: Create an S3 Bucket, Pull HTML file from Github, Put it in S3 bucket

(to pull html on github)

Parameters:
Type:String
Description: Link of html to pull
Default: https://github.com/lhynesg/html/index.html

(bucket name)

Bucketname:  sgbucket1
Type: String
Description: Name of the bucket

(Lambda Function:
-Pull HTML from github
-CreatesBucket
-Add HTML
-Sets Read Permission)

Resources:
Deploytos3:
Type: AWS::Serverless::Function
Properties:
Handler: index.handler
Runtime: nodejs 6.10
CodeURL: htmldeploy
Memorysize: 512
Timeout: 300
Environment:
Variables:
TEST: WORKS
Policies: 
-AWSLambdaBasicExecutionRole
-AmazonS3FullAccess

(CloudFormation Template invokes a Lambda using something called a custom resource)

DeploymentCustomResource:
Type: Custom:deploytoS3
Properties:
ServiceToken: GetAtt deploytos3.Arm
Bucketname: sgbucket1


