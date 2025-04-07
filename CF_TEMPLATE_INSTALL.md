# Install the CF template

1. Launch Cloud Formation Stack in client account
   https://github.com/New-Math-Data/Bootstrap
1. Give the stack the name `nmd-developer-access-saml`
1. Open the file in this repo called GoogleIDPMetadata.xml and copy the entire contents to the input field called `samlMetadata`
1. Click Next
1. Check the box for `I acknowledge that AWS CloudFormation might create IAM resources with custom names.`
1. Click Create Stack
1. Note the Customer AWS Account Number
