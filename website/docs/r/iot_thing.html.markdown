---
subcategory: "IoT Core"
layout: "aws"
page_title: "AWS: aws_iot_thing"
description: |-
    Creates and manages an AWS IoT Thing.
---

# Resource: aws_iot_thing

Creates and manages an AWS IoT Thing.

## Example Usage

```terraform
resource "aws_iot_thing" "example" {
  name = "example"

  attributes = {
    First = "examplevalue"
  }
}
```

## Argument Reference

* `name` - (Required) The name of the thing.
* `attributes` - (Optional) Map of attributes of the thing.
* `thing_type_name` - (Optional) The thing type name.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `default_client_id` - The default client ID.
* `version` - The current version of the thing record in the registry.
* `arn` - The ARN of the thing.

## Import

Import IOT Things using the name. For example:

```
$ terraform import aws_iot_thing.example example
```
