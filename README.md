# SAML Setup

## Customer Account

1. Download SAML XML Data from
   https://admin.google.com/ac/apps/saml/804580507359
1. Generate an external Id for the customer (Random number or Use a customer UUID from the Freeside console?)
1. Launch Cloud Formation Stack in client account
   https://github.com/New-Math-Data/cloudformation-setup-saml-gsuite
1. Give the stack the name `nmd-freeside-saml`
1. Click Next
1. Check the box for `I acknowledge that AWS CloudFormation might create IAM resources with custom names.`
1. Click Create Stack
1. Note the Customer AWS Account Number

## NMD GSuite

1. Navigate to a user profile
   https://admin.google.com/ac/users/
1. Add the following to the Amazon section
   arn:aws:iam::{AWS_ACCOUNT_NUMBER}:role/NMD-Freeside-Admin,arn:aws:iam::{AWS_ACCOUNT_NUMBER}:saml-provider/GSuite
1.

https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html
