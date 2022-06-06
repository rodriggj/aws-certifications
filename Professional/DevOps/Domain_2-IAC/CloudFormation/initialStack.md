# Steps

## Region 
1. Select the N. Virginia region

## CF Wizard

### 1. Select Template
Steps: 
1. Choose method of CF template creation. 2 Options presented: 
    1. `Design a Template`: Utilize the CloudFormation Designer to create/use a Template
    2. `Choose a Template`: 1. Select a sample template from dropdown, 2. upload to Amazon S3 or 3. specify an S3 URL to an existing template
2. Click `Next`

### 2. Specify Stack Details
Steps: 
1. Provide Stack name
2. Review Parameters defined in CF template

### 3. Configure Stack Options
Steps: 
1. Input Tags (key/value pairs)
2. Configure Permissions. Here you need to specify an IAM role(s). If none are provided the credentials used at sign-in are referenced.
3. Configure Stack Failure Options. 1. Rollback or 2. Preserve state of created resources
4. Configure Advanced Options. 1. Stack Policy(s), 2. Rollback Configuration (Monitoring Time & CloudWatch Alarms) 3. Notification Options (SNS) 4. Stack Create Options (Timeout & Termination Protection)

### 4. Review