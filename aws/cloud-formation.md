# AWS CloudFormation

AWS CloudFormation is a comprehensive templating language that enables you to create managed 'stacks' of AWS resources.

- [AWS CloudFormation Masterclass](https://www.youtube.com/watch?v=6R44BADNJA8)

## Create Template

CloudFormation template can either written in JSON or YAML. There are DSL build on top of it to make tasks easier. 

- [Template Reference](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-reference.html)
- [cfndsl](https://github.com/stevenjack/cfndsl) a Ruby based DSL
  - [cfndsl_examples](https://github.com/neillturner/cfndsl_examples) Cloud Formation examples written in cfndsl
- [Troposphere](https://github.com/cloudtools/troposphere) a Python based DSL

### Concepts

- [Resources](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html) a stacks is a collection of resources, they can be S3 bucket, EC2 instances, API Gateway, IAM Role ... etc
- [Intrinsic functions](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html)
	- [Ref](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) use reference to get APN to a resource, or get the value of parameter. 
	- GetAtt - get attributes
	- FindInMap - find values from a map
- [Psuedo Parameters](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html) Pseudo Parameters are parameters that are predefined by AWS CloudFormation
	- AWS::AccountId
	- AWS::Region
	- AWS::StackId

## Deployment

### Create Stack

```
aws --profile myprofile --region us-east-1 cloudformation create-stack \
  --stack-name my-stack \
  --template-body file://mystack.json \
  --parameters '[{"ParameterKey":"Environment","ParameterValue":"dev"}]' \
  --on-failure ROLLBACK
```

### Update Stack

```
aws --profile myprofile --region us-east-1 cloudformation update-stack \
  --stack-name my-stack \
  --template-body file://stack.json \
  --parameters '[{"ParameterKey":"Environment","UsePreviousValue":true}]'
```

### Delete Stack

```
aws --profile myprofile --region us-east-1 cloudformation delete-stack --stack-name my-stack
```