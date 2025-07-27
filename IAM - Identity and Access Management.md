# IAM - Identity and Access Management

## Users & Groups
 
- IAM = Identity and Access Management, **Global service**
- **Root account** created by default, shouldn’t be used or shared
- **Users** are people within your organization, and can be grouped
- **Groups** only contain users, not other groups
- **Users** don’t have to belong to a group, and user can belong to multiple groups

## Permissions

- **Users or Groups** can be assigned JSON documents called policies
- These policies define the **permissions** of the users
- In AWS you apply the **least privilege principle**: don’t give more permissions than a user needs

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "elasticloadbalancing:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudwatch:ListMetrics",
        "cloudwatch:GetMetricStatistics",
        "cloudwatch:Describe*"
      ],
      "Resource": "*"
    }
  ]
}
```

## Policies

- **Consists of**
	> <ul><li><b>Version:</b> policy language version, always include “2012 -10 - 17”</li><li><b>Id:</b> an identifier for the policy (optional)</li><li><b>Statement:</b> one or more individual statements (required)</li></ul>
- **Statements consists of**
	> <ul><li><b>Sid:</b> an identifier for the statement (optional)</li><li><b>Effect:</b> whether the statement allows or denies access (Allow, Deny)</li><li><b>Principal:</b> account/user/role to which this policy applied to</li><li><b>Action:</b> list of actions this policy allows or denies</li><li><b>Resource:</b> list of resources to which the actions applied to</li><li><b>Condition:</b> conditions for when this policy is in effect (optional)</li></ul>

## Password Policy

- Strong passwords = higher security for your account
- In AWS, you can setup a password policy:
	> <ul><li>Set a minimum password length</li><li>Require specific character types<ul><li>Uppercase letters</li><li>Lowercase letters</li><li>Numbers</li><li>Non-alphanumeric characters</li></ul></li><li>Allow all IAM users to change their own passwords</li><li>Require users to change their password after some time (password expiration)</li><li>Prevent password re-use</li></ul>

## Multi Factor Authentication - MFA

- Users have access to your account and can possibly change configurations or delete resources in your AWS account
- You want to protect your Root Accounts and IAM users
- MFA = password you know + security device you own
- **Main benefit of MFA:** if a password is stolen or hacked, the account is not compromised

## MFA devices options in AWS

- **Virtual MFA device** (Support for multiple tokens on a single device): **Google Authenticator**, **Authy**
- **Universal 2nd Factor (U2F) Security Key** (Support for multiple root and IAM users using a single security key): **YubiKey** by Yubico (3rd party)
- **Hardware Key Fob MFA Device:** provided by Gemalto (3rd party)
- **Hardware Key Fob MFA Device for AWS GovCloud (US):** provided by SurePassID (3rd party)

## How can users access AWS?

- To access AWS, you have three options:
	> <ul><li><b>AWS Management Console</b> protected by password + MFA</li><li><b>AWS Command Line Interface (CLI):</b> protected by access keys</li><li><b>AWS Software Developer Kit (SDK) - for code:</b> protected by access keys</li></ul>
- Access Keys are generated through the AWS Console
- Users manage their own access keys
- *Access Keys are secret, just like a password. Don’t share them*
- Access Key ID ~= username
- Secret Access Key ~= password

## What’s the AWS CLI?

- A tool that enables you to interact with AWS services using commands in your command-line shell
- Direct access to the public APIs of AWS services
- You can develop scripts to manage your resources
- It’s open-source https://github.com/aws/aws-cli
- Alternative to using AWS Management Console

## What’s the AWS SDK?

- AWS Software Development Kit (AWS SDK)
- Language-specific APIs (set of libraries)
- Enables you to access and manage AWS services programmatically
- Supports
	> <ul><li>SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++)</li><li>Mobile SDKs (Android, iOS, …)</li><li>IoT Device SDKs (Embedded C, Arduino, …)</li></ul> 

## IAM Roles for Services

- Some AWS service will need to perform actions on your behalf
- To do so, we will assign **permissions** to AWS services with **IAM Roles**
- Common roles
	> <ul><li>EC2 Instance Roles</li><li>Lambda Function Roles</li><li>Roles for CloudFormation</li></ul>

## IAM Security Tools

- **IAM Credentials Report (account-level)**
	> A report that lists all your account's users and the status of their various credentials
- **IAM Access Advisor (user-level)**
	> <ul><li>Access advisor shows the service permissions granted to a user and when those services were last accessed</li><li>You can use this information to revise your policies</li></ul>

## IAM Guidelines & Best Practices

- Don’t use the root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions to groups
- Create a **strong password policy**
- Use and enforce the use of **Multi Factor Authentication (MFA)**
- Create and use **Roles** for giving permissions to AWS services
- Use Access Keys for Programmatic Access (CLI / SDK)
- Audit permissions of your account using IAM Credentials Report & IAM Access Advisor
- *Never share IAM users & Access Keys*
