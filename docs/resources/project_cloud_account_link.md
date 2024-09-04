---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "wiz_project_cloud_account_link Resource - terraform-provider-wiz"
subcategory: ""
description: |-
  Associate a cloud subscription with a project. Use either this resource or the cloud_account_link block set for the wiz_project, never both.
---

# wiz_project_cloud_account_link (Resource)

Associate a cloud subscription with a project. Use either this resource or the cloud_account_link block set for the wiz_project, never both.

## Example Usage

```terraform
# A link from a project to a cloud account can be created using the accounts id in wiz
resource "wiz_project_cloud_account_link" "example" {
  project_id       = "ee25cc95-82b0-4543-8934-5bc655b86786"
  cloud_account_id = "5cc3a684-44cb-4cd5-b78f-f029c25dc617"
  environment      = "PRODUCTION"
}

# Or using the external id of the cloud account
resource "wiz_project_cloud_account_link" "example" {
  project_id                = "ee25cc95-82b0-4543-8934-5bc655b86786"
  external_cloud_account_id = "04e56587-4408-402a-9c8c-f454ed45da65"
  environment               = "PRODUCTION"
}

# Both can be supplied but they have to belong to the same account
resource "wiz_project_cloud_account_link" "example" {
  project_id                = "ee25cc95-82b0-4543-8934-5bc655b86786"
  cloud_account_id          = "5cc3a684-44cb-4cd5-b78f-f029c25dc617"
  external_cloud_account_id = "04e56587-4408-402a-9c8c-f454ed45da65"
  environment               = "PRODUCTION"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `project_id` (String) The Wiz internal identifier of the Wiz project to link the cloud account to

### Optional

- `cloud_account_id` (String) The Wiz internal identifier for the Cloud Account Subscription.
- `environment` (String) The environment.
    - Allowed values: 
        - PRODUCTION
        - STAGING
        - DEVELOPMENT
        - TESTING
        - OTHER

    - Defaults to `PRODUCTION`.
- `external_cloud_account_id` (String) The external identifier for the Cloud Account, e.g. an azure subscription id or an aws account id.
- `resource_groups` (List of String) Please provide a list of resource group identifiers for filtering by resource groups. `shared` must be true to define resource_groups.
- `resource_tags` (Block Set) Provide a key and value pair for filtering resources. `shared` must be true to define resource_tags. (see [below for nested schema](#nestedblock--resource_tags))
- `shared` (Boolean) Subscriptions that host a few projects can be marked as ‘shared subscriptions’ and resources can be filtered by tags.

### Read-Only

- `id` (String) Unique tf-internal identifier for the project cloud account link

<a id="nestedblock--resource_tags"></a>
### Nested Schema for `resource_tags`

Required:

- `key` (String)
- `value` (String)

## Import

Import is supported using the following syntax:

```shell
# The id for importing a wiz_project_cloud_account_link has to be in this format: 'link|<project_id>|<cloud_account_id>'
terraform import wiz_project_cloud_account_link.example_import "link|ee25cc95-82b0-4543-8934-5bc655b86786|5cc3a684-44cb-4cd5-b78f-f029c25dc617"
```