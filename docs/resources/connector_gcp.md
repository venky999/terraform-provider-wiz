---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "wiz_connector_gcp Resource - terraform-provider-wiz"
subcategory: ""
description: |-
  Connectors are used to connect GCP resources to Wiz.
---

# wiz_connector_gcp (Resource)

Connectors are used to connect GCP resources to Wiz.

## Example Usage

```terraform
# Provision a simple GCP connector, organization-wide
resource "wiz_connector_gcp" "example" {
  name = "example"
  auth_params = jsonencode({
    "isManagedIdentity" : true,
    "organization_id" : "o-example"
  })

  extra_config = jsonencode(
    {
      "projects" : [],
      "excludedProjects" : [],
      "includedFolders" : [],
      "excludedFolders" : [],
      "auditLogMonitorEnabled" : false
    }
  )
}

# Provision a GCP connector targeting an individual Google project
resource "wiz_connector_gcp" "example" {
  name = "example"
  auth_params = jsonencode({
    "isManagedIdentity" : true,
    "project_id" : "exmaple-project-id"
  })

  extra_config = jsonencode(
    {
      "projects" : [],
      "excludedProjects" : [],
      "includedFolders" : [],
      "excludedFolders" : [],
      "auditLogMonitorEnabled" : false
    }
  )
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `auth_params` (String, Sensitive) The authentication parameters. Must be represented in `JSON` format.
- `name` (String) The connector name.

### Optional

- `enabled` (Boolean) Whether the connector is enabled.
    - Defaults to `true`.
- `extra_config` (String) Extra configuration for the connector. Must be represented in `JSON` format.

### Read-Only

- `audit_log_monitor_enabled` (Boolean) Whether audit log monitor is enabled. Note an advanced license is required.
- `events_pub_sub_subscription_id` (String) If using Wiz Cloud Events, the Pub/Sub Subscription ID.
- `events_topic_name` (String) If using Wiz Cloud Events, the Topic Name in format `projects/<project_id>/topics/<topic_id>`.
- `excluded_folders` (List of String) The GCP folders excluded by the connector.
- `excluded_projects` (List of String) The GCP projects excluded by the connector.
- `folder_id` (String) The GCP folder ID.
- `id` (String) Wiz internal identifier for the connector.
- `included_folders` (List of String) The GCP folders included by the connector.
- `is_managed_identity` (String) Is managed identity?
- `organization_id` (String) The GCP organization ID.
- `projects` (List of String) The GCP projects to target with the connector.

## Import

Import is supported using the following syntax:

```shell
# Importing Considerations:
#
# Please note this is considered experimental, exercise caution and consider the following:
#
# - Make sure that the `auth_params` field is set to the same values as set when the resource was created outside of Terraform.
#   This is due to the way we need to handle change as under normal diff conditions, `auth_params` requires a resource recreation.
#
# - For `auth_params` include `isManagedIdentity`. If using outposts, also include `outPostId` and `diskAnalyzer` structure.
#
# For more information, refer to the examples in the documentation.
#
terraform import wiz_connector_gcp.import_example "7be792ba-bfd1-46d0-9fba-5f6bc19df4a8"

# Optional - this is to set auth_params in state.
#
# If not run post-import, the next `terraform apply` will take care of it.
# Note any speculative changes to `auth_params` are for setting state for the one-time import only, any further changes would require a resource recreation as normal.
terraform apply --target=wiz_connector_gcp.import_example
```
