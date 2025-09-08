<!-- Remember to update this file for your charm -- replace <charm-name> with the appropriate name. -->
# Terraform Modules

This project contains the [Terraform][Terraform] modules to deploy the 
[<charm-name> charm][<charm-name> charm] with its dependencies.

The modules use the [Terraform Juju provider][Terraform Juju provider] to model
the bundle deployment onto any Kubernetes environment managed by [Juju][Juju].

## Module structure

- **main.tf** - Defines the Juju application to be deployed.
- **variables.tf** - Allows customization of the deployment including Juju model name, charm's channel and configuration.
- **output.tf** - Responsible for integrating the module with other Terraform modules, primarily by defining potential integration endpoints (charm integrations).
- **versions.tf** - Defines the Terraform provider.

[Terraform]: https://www.terraform.io/
[Terraform Juju provider]: https://registry.terraform.io/providers/juju/juju/latest
[Juju]: https://juju.is
[<charm-name> charm]: https://charmhub.io/<charm-name>

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_juju"></a> [juju](#requirement\_juju) | >= 0.17.1 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_juju"></a> [juju](#provider\_juju) | >= 0.17.1 |
| <a name="provider_juju.charm_db"></a> [juju.charm\_db](#provider\_juju.charm\_db) | >= 0.17.1 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_charm_name"></a> [charm\_name](#module\_charm\_name) | ../charm | n/a |
| <a name="module_postgresql"></a> [postgresql](#module\_postgresql) | git::https://github.com/canonical/postgresql-operator//terraform | n/a |

## Resources

| Name | Type |
|------|------|
| [juju_access_offer.postgresql](https://registry.terraform.io/providers/juju/juju/latest/docs/resources/access_offer) | resource |
| [juju_integration.charm_name_postgresql_database](https://registry.terraform.io/providers/juju/juju/latest/docs/resources/integration) | resource |
| [juju_offer.postgresql](https://registry.terraform.io/providers/juju/juju/latest/docs/resources/offer) | resource |
| [juju_model.charm](https://registry.terraform.io/providers/juju/juju/latest/docs/data-sources/model) | data source |
| [juju_model.charm_db](https://registry.terraform.io/providers/juju/juju/latest/docs/data-sources/model) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_charm_name"></a> [charm\_name](#input\_charm\_name) | n/a | <pre>object({<br/>    app_name    = optional(string, "<charm-name>")<br/>    channel     = optional(string, "latest/stable")<br/>    config      = optional(map(string), {})<br/>    constraints = optional(string, "arch=amd64")<br/>    revision    = optional(number)<br/>    base        = optional(string, "ubuntu@24.04")<br/>    units       = optional(number, 1)<br/>  })</pre> | n/a | yes |
| <a name="input_db_model"></a> [db\_model](#input\_db\_model) | Reference to the VM Juju model to deploy database charm to. | `string` | n/a | yes |
| <a name="input_db_model_user"></a> [db\_model\_user](#input\_db\_model\_user) | Juju user used for deploying database charms. | `string` | n/a | yes |
| <a name="input_model"></a> [model](#input\_model) | Reference to the k8s Juju model to deploy application to. | `string` | n/a | yes |
| <a name="input_model_user"></a> [model\_user](#input\_model\_user) | Juju user used for deploying the application. | `string` | n/a | yes |
| <a name="input_postgresql"></a> [postgresql](#input\_postgresql) | n/a | <pre>object({<br/>    app_name    = optional(string, "postgresql")<br/>    channel     = optional(string, "14/stable")<br/>    config      = optional(map(string), {})<br/>    constraints = optional(string, "arch=amd64")<br/>    revision    = optional(number)<br/>    base        = optional(string, "ubuntu@22.04")<br/>    units       = optional(number, 1)<br/>  })</pre> | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_app_name"></a> [app\_name](#output\_app\_name) | Name of the deployed application. |
| <a name="output_provides"></a> [provides](#output\_provides) | n/a |
| <a name="output_requires"></a> [requires](#output\_requires) | n/a |
<!-- END_TF_DOCS -->