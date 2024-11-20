## Stack set with self-managed permissions 
If you set up stack sets with self-managed permissions, follow the instructions below. If you used service manager permissions, skip to “Stack Set with Service Managed permissions”.

The following command creates a stack set. 
```
aws cloudformation create-stack-set \
    --stack-set-name my-spoke-stack-set2 \
    --description "Creates SageMaker Studio Domain, User Profile, Jupyter and Mlflow Apps in spoke accounts" \
    --parameters ParameterKey="DomainNamePrefix",ParameterValue="string" ParameterKey="MlFlowName",ParameterValue="string" ParameterKey="UserProfileNamePrefix",ParameterValue="string" ParameterKey="OwnerID",ParameterValue="string" \
    --capabilities CAPABILITY_IAM \
    --template-body file://deployment/spoke-sagemaker-stack.yaml
```

Next, verify that the stack set has been created.

aws cloudformation list-stack-sets

Use the create-stack-instances command to add stack instances to your stack set. In this walkthrough, we use  us-east-2 as the value of the --regions option. Be sure to change the accounts parameter to the account IDs of your spoke accounts. 

```
aws cloudformation create-stack-instances \
  --stack-set-name my-spoke-stack-set2 \
  --accounts '["Spoke_Account_ID"]' \
  --regions '["us-east-2"]'
```

Using the operation-id that was returned as part of the create-stack-instances output, use the following describe-stack-set-operation command to verify that your stack instances were created successfully.
```
aws cloudformation describe-stack-set-operation \ --stack-set-name my-awsconfig-stackset \ --operation-id operation_ID
```

## Stack Set with Service Managed permissions 

When acting as a delegated administrator, you must set the --call-as option to DELEGATED_ADMIN each time you run a StackSets command.
```
--call-as DELEGATED_ADMIN
```
For this lab it would look like:
```
aws cloudformation create-stack-set \
    --stack-set-name my-spoke-stack-set \
    --description "Creates SageMaker Studio Domain, User Profile, Jupyter and Mlflow Apps in spoke accounts" \
    --parameters ParameterKey="DomainNamePrefix",ParameterValue="string" ParameterKey="MlFlowName",ParameterValue="string" ParameterKey="UserProfileNamePrefix",ParameterValue="string" ParameterKey="OwnerID",ParameterValue="string" \
    --permission-model SERVICE_MANAGED \
    --auto-deployment Enabled=true,RetainStacksOnAccountRemoval=true \
    --capabilities CAPABILITY_IAM \
    --template-body file://deployment/spoke-sagemaker-stack.yaml
```

After you create, check that your stack set is listed here:
```
aws cloudformation list-stack-sets
```
Next, add stack instances to your stack set. A stack instance refers to a stack in a specific account/OU and Region. 

```
aws cloudformation create-stack-instances \
--stack-set-name my-spoke-stack-set \
--deployment-targets OrganizationalUnitIds='["ou-id-1"]' \
--regions '["us-east-2"]'
```

Using the operation-id that was returned as part of the create-stack-instances output, use the following describe-stack-set-operation command to verify that your stack instances were created successfully.
```
aws cloudformation describe-stack-set-operation \
  --stack-set-name my-awsconfig-stackset \
  --operation-id operation_ID
```
