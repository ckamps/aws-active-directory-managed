# Deploy AWS Managed Microsoft Active Directory (AD)

This AWS CloudFormation template demonstrates deployment of [AWS Managed Microsoft Active Directory](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_microsoft_ad.html).

## Usage

Use AWS CloudFormation to create a stack using the template `active-directory-managed.yml`. See the next section for an explanation of the supported [parameters](#parameters).

Stack creation cn take ~20 minutes.

## Adding Users and Groups

See [https://github.com/ckamps/samples-ad-users-groups](https://github.com/ckamps/samples-ad-users-groups) for an example of how to add sample users and groups to your new directory.

## Parameters

|Parameter|Required|Description|Default|
|---------|--------|-----------|-------|
|`pDomainAdminPasswordSecretName`|Required|Name of secret in AWS Secrets Manager containing the password for the domain administrator user. By default, the user name is set to `Admin`.<br><br>The AWS Secrets Manager secret must be in the form of `password:<value>` where `password` is the key and `<value>` is the password value.|None|
|`pDomainDnsName`|Optional|Fully qualified domain name (FQDN) of the forest root domain|`corp.example.com`|
|`pDomainNetBiosName`|Optional|NetBIOS name of the domain (up to 15 characters) for users of earlier versions of Windows|`CORP`|
|`pAdEdition`|Optional|The AWS Microsoft AD edition. Valid values include `Standard` and `Enterprise`.|`Standard`|
|`pVpcId`|Required|ID of the VPC with which to associated the managed AD.|None|
|`pPrivateSubnet1Id`|Required|ID of the private subnet 1 in one AZ||
|`pPrivateSubnet2Id`|Required|ID of the private subnet 2 in a different AZ||
|`pCreateVpcDhcpOptions`|Optional|`true` or `false`. Whether or not you want a VPC DHCP options set to be created. If you are using shared subnets, you should considering setting to `false` since you might not have write access to the VPC to perform this operation.|`false`|