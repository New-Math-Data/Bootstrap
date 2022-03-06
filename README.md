# SAML Setup

## Customer Account

[Installing CF Template](https://github.com/New-Math-Data/cloudformation-setup-saml-gsuite/blob/main/CF_TEMPLATE_INSTALL.md)

## NMD GSuite

1. Navigate to a user profile
   https://admin.google.com/ac/users/
1. Add the following to the Amazon section
   arn:aws:iam::{AWS_ACCOUNT_NUMBER}:role/NMD-Freeside-Admin,arn:aws:iam::{AWS_ACCOUNT_NUMBER}:saml-provider/GSuite
1.

https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html

## Setup SSO

The SAML roles installed also work with AWS CLI credentials.

### Install aws-google-auth

https://github.com/cevoaustralia/aws-google-auth
`pip install aws-google-auth`

Open your ~/.aws/config file and add the following block, replacing values in <>
with the correct values. For GOOGLEIDP and GOOGLESDP, you can ask in the `#freeside` channel in slack.

Customer account number can be retrieved from customer or from your login page using the GSuite
SSO/SAML App.

Username is your newmathdata.com email address.

```
[profile <PROFILE_NAME>]
region = us-east-1
google_config.ask_role = False
google_config.duration = 3600
google_config.google_idp_id = <GOOGLEIDP>
google_config.role_arn = arn:aws:iam::<CUSTOMER_ACCOUNT_NUMBER>:role/NMD-Admin
google_config.google_sp_id = <GOOGLESPID>
google_config.u2f_disabled = False
google_config.google_username = <USERNAME>
google_config.keyring = False
google_config.bg_response = None
```
