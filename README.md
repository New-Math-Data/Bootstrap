# SAML Setup

## Customer Account

[Installing CF Template](https://github.com/New-Math-Data/cloudformation-setup-saml-gsuite/blob/main/CF_TEMPLATE_INSTALL.md)

## CLI Deploy
From Customer account
```bash
aws cloudformation deploy \
  --template-file main.yaml \
  --stack-name nmd-saml-idp \
  --parameter-overrides \
    idpName="NMDGoogle" \
    samlMetadata="YOUR_SAML_METADATA_XML_AS_STRING" \
    custNameAbbreviation="customer_name" \
    accessPolicy="AdministratorAccess" \
  --capabilities CAPABILITY_NAMED_IAM \
  --region us-west-2
```
## NMD GSuite

1. Navigate to a user profile
   https://admin.google.com/ac/users/
1. Add the following to the Amazon section
   arn:aws:iam::{AWS_ACCOUNT_NUMBER}:role/NMD-Freeside-Admin,arn:aws:iam::{AWS_ACCOUNT_NUMBER}:saml-provider/GSuite

https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html

## Setup SSO

The SAML roles installed also work with AWS CLI credentials.
We use saml2aws:
```bash
brew install saml2aws
saml2aws configure 
   Configuration saved for IDP account: default
   saml2aws configure
   ? Please choose a provider: GoogleApps
   ? AWS Profile saml
   ? URL https://accounts.google.com/o/saml2/initsso?idpid=C03vzt6hn&spid=804580507359&forceauthn=false
   ? Username cking@newmathdata.com
   ? Password ***************
   ? Confirm ***************
   
   account {
     URL: https://accounts.google.com/o/saml2/initsso?idpid=C03vzt6hn&spid=804580507359&forceauthn=false
     Username: cking@newmathdata.com
     Provider: GoogleApps
     MFA: Auto
     SkipVerify: true
     AmazonWebservicesURN: urn:amazon:webservices
     SessionDuration: 3600
     Profile: saml
     RoleARN:
     Region:
   }
saml2aws login
   Using IdP Account default to access GoogleApps https://accounts.google.com/o/saml2/initsso?idpid=C03vzt6hn&spid=804580507359&forceauthn=false
   To use saved password just hit enter.
   ? Username cking@newmathdata.com
   ? Password
   
   Authenticating as cking@newmathdata.com ...
   Check your phone and tap 'Yes' on the prompt. Then press ENTER to continue.
   
   ? Please choose the role Account: 12345678901 / NMD-Admin
   Selected role: arn:aws:iam::12345678901:role/NMD-Admin
   Requesting AWS credentials using SAML assertion.
   Logged in as: arn:aws:sts::12345678901:assumed-role/NMD-Admin/cking@newmathdata.com
   
   Your new access key pair has been stored in the AWS configuration.
   Note that it will expire at 2024-11-18 11:43:24 -0800 PST
   To use this credential, call the AWS CLI with the --profile option (e.g. aws --profile saml ec2 describe-instances).
```
