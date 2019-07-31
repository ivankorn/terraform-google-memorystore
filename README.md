# [Google Cloud Memorystore Terraform Module](https://registry.terraform.io/modules/terraform-google-modules/memorystore/google/)

A Terraform module for creating a fully functional Google Memorystore (redis) instance.

## Compatibility
This module is meant for use with Terraform 0.12. If you haven't [upgraded](https://www.terraform.io/upgrade-guides/0-12.html) and need a Terraform 0.11.x-compatible version of this module, the last released version intended for Terraform 0.11.x
is [0.1.0](https://registry.terraform.io/modules/terraform-google-modules/memorystore/google/0.1.0).

## Usage

Check the [examples/](./examples/) directory for more.

```hcl
module "memorystore" {
  source  = "terraform-google-modules/memorystore/google"
  version = "0.1.0"

  name    = "my-memorystore"
  project = "my-gcp-project"
}
```

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| alternative\_location\_id | The alternative zone where the instance will be provisioned. | string | `"null"` | no |
| authorized\_network | The full name of the Google Compute Engine network to which the instance is connected. If left unspecified, the default network will be used. | string | `"null"` | no |
| display\_name | An arbitrary and optional user-provided name for the instance. | string | `"null"` | no |
| enable\_apis | Enable required APIs for Cloud Memorystore. | bool | `"true"` | no |
| labels | The resource labels to represent user provided metadata. | object | `<map>` | no |
| location\_id | The zone where the instance will be provisioned. If not provided, the service will choose a zone for the instance. For STANDARD_HA tier, instances will be created across two zones for protection against zonal failures. If [alternativeLocationId] is also provided, it must be different from [locationId]. | string | `"null"` | no |
| memory\_size\_gb | Redis memory size in GiB. Defaulted to 1 GiB | number | `"1"` | no |
| name | The ID of the instance or a fully qualified identifier for the instance. | string | n/a | yes |
| project | The ID of the project in which the resource belongs to. | string | n/a | yes |
| redis\_version | The version of Redis software. | string | `"null"` | no |
| region | The GCP region to use. | string | `"null"` | no |
| reserved\_ip\_range | The CIDR range of internal addresses that are reserved for this instance. | string | `"null"` | no |
| tier | The service tier of the instance. https://cloud.google.com/memorystore/docs/redis/reference/rest/v1/projects.locations.instances#Tier | string | `"STANDARD_HA"` | no |

## Outputs

| Name | Description |
|------|-------------|
| current\_location\_id | The current zone where the Redis endpoint is placed. |
| host | The IP address of the instance. |
| id | The memorystore instance ID. |
| region | The region the instance lives in. |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## File structure

The project has the following folders and files:

- /: root folder
- /examples: examples for using this module
- /scripts: Scripts for specific tasks on module (see Infrastructure section on this file)
- /test: Folders with files for testing the module (see Testing section on this file)
- /helpers: Optional helper scripts for ease of use
- /main.tf: main file for this module, contains all the resources to create
- /variables.tf: all the variables for the module
- /output.tf: the outputs of the module
- /readme.md: this file

## Testing

### Requirements

- Terraform is [installed](#software-dependencies) on the machine where Terraform is executed.
- An existing google cloud project
- The `redis.googleapis.com` API should be enabled
- A service account key
- Docker

### Software Dependencies
### Terraform
- [Terraform](https://www.terraform.io/downloads.html) >= 0.12.0
- [terraform-provider-google](https://github.com/terraform-providers/terraform-provider-google) >= v2.5.0

### Running Integration Tests

Tests are run inside of an existing google cloud project.

1. Create tfvars file for test:

```sh
cp test/fixtures/minimal/terraform.tfvars.example test/fixtures/minimal/terraform.tfvars
```

2. Edit new `test/fixtures/minimal/terraform.tfvars` and add project id to run test in.

3. Copy a service account key (`credentials.json` file) into root of this repo.

4. Run `make test_integration_docker`.

## Autogeneration of documentation from .tf files

Run:

```
make generate_docs
```