---
subcategory: "AppConfig"
layout: "aws"
page_title: "AWS: aws_appconfig_application"
description: |-
  Provides an AppConfig Application resource.
---

# Resource: aws_appconfig_application

Provides an AppConfig Application resource.

## Example Usage

```terraform
resource "aws_appconfig_application" "example" {
  name        = "example-application-tf"
  description = "Example AppConfig Application"

  tags = {
    Type = "AppConfig Application"
  }
}
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) Name for the application. Must be between 1 and 64 characters in length.
* `description` - (Optional) Description of the application. Can be at most 1024 characters.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider [`default_tags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block) present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the AppConfig Application.
* `id` - AppConfig application ID.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider [`default_tags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block).

## Import

Import AppConfig Applications using their application ID. For example:

```
$ terraform import aws_appconfig_application.example 71rxuzt
```
