# IBM Cloud Transit Gateway - Terraform Module

<!-- UPDATE BADGE: Update the link for the following badge-->
[![Stable (With quality checks)](https://img.shields.io/badge/Status-Stable%20(With%20quality%20checks)-green)](https://terraform-ibm-modules.github.io/documentation/#/badge-status)
[![Build status](https://github.com/terraform-ibm-modules/terraform-ibm-transit-gateway/actions/workflows/ci.yml/badge.svg)](https://github.com/terraform-ibm-modules/terraform-ibm-transit-gateway/actions/workflows/ci.yml)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
[![latest release](https://img.shields.io/github/v/release/terraform-ibm-modules/terraform-ibm-transit-gateway?logo=GitHub&sort=semver)](https://github.com/terraform-ibm-modules/terraform-ibm-transit-gateway/releases/latest)


With IBM Cloud® Transit Gateway, you can create single or multiple transit gateways to connect VPCs. You can also connect your IBM Cloud classic infrastructure to a transit gateway to provide seamless communication with classic infrastructure resources. Any new network that you connect to a transit gateway is then made available to every other network connected to it. For more information, see [About IBM Cloud Transit Gateway](https://cloud.ibm.com/docs/transit-gateway?topic=transit-gateway-about) in the IBM Cloud docs.

## Usage

```hcl
data "ibm_resource_group" "resource_group" {
  name = "resource_group_name"
}

module "tg_gateway_connection" {
  # Replace "main" with a GIT release version to lock into a specific release
  source = "git::https://github.com/terraform-ibm-modules/transit-gateway.git?ref=main"
  transit_gateway_name = "transit gateway name"
  location             = "eu-de"
  global_routing       = true
  tags                 = ["tag1", "tag2"]
  resource_group_id    = data.ibm_resource_group.resource_group.id
  vpc_connections      = ["crn:v1:bluemix:public:is:eu-de:a/7aa6f7b185f2e3170fac9919aa1769ee::vpc:r010-a9fdc623-d702-4381-a116-07546dba1b87","crn:v1:bluemix:public:is:eu-de:a/7aa6f7b185f2e3170fac9919aa1769ee::vpc:r010-4c39039d-e7ef-411d-a191-3cb549dc41a1"]
  classic_connections_count   = false
}
```

<!-- BEGIN EXAMPLES HOOK -->
## Examples

- [ Transit Gateway Module Example](examples/basic)
- [ Transit Gateway connecting two VPCs](examples/two-vpcs)
<!-- END EXAMPLES HOOK -->

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.0.0 |
| <a name="requirement_ibm"></a> [ibm](#requirement\_ibm) | >= 1.41.1 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [ibm_tg_connection.classic_connections](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_connection) | resource |
| [ibm_tg_connection.vpc_connections](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_connection) | resource |
| [ibm_tg_gateway.tg_gw_instance](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/tg_gateway) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_classic_connections_count"></a> [classic\_connections\_count](#input\_classic\_connections\_count) | Number of classic connections to add. | `number` | n/a | yes |
| <a name="input_global_routing"></a> [global\_routing](#input\_global\_routing) | Gateways with global routing (true) to connect to the networks outside their associated region | `bool` | `false` | no |
| <a name="input_region"></a> [region](#input\_region) | The IBM Cloud region where all resources will be provisioned. | `string` | n/a | yes |
| <a name="input_resource_group_id"></a> [resource\_group\_id](#input\_resource\_group\_id) | Resource group ID where the transit gateway to be created. | `string` | `null` | no |
| <a name="input_resource_tags"></a> [resource\_tags](#input\_resource\_tags) | List of tags | `list(string)` | `null` | no |
| <a name="input_transit_gateway_name"></a> [transit\_gateway\_name](#input\_transit\_gateway\_name) | Name of the transit gateway | `string` | n/a | yes |
| <a name="input_vpc_connections"></a> [vpc\_connections](#input\_vpc\_connections) | The list of vpc instance resource\_crn to add network connections for. | `list(string)` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_classic_conn_ids"></a> [classic\_conn\_ids](#output\_classic\_conn\_ids) | List of classic connection IDs |
| <a name="output_tg_crn"></a> [tg\_crn](#output\_tg\_crn) | CRN of the gateway |
| <a name="output_tg_id"></a> [tg\_id](#output\_tg\_id) | The ID of the transit gateway |
| <a name="output_vpc_conn_ids"></a> [vpc\_conn\_ids](#output\_vpc\_conn\_ids) | List of vpc connection IDs |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Contributing

You can report issues and request features for this module in the [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues) repo. See [Report an issue or request a feature](https://github.com/terraform-ibm-modules/.github/blob/main/.github/SUPPORT.md).

To set up your local development environment, see [Local development setup](https://terraform-ibm-modules.github.io/documentation/#/local-dev-setup) in the project documentation.
