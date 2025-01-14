---
subcategory: "IoT Core"
layout: "aws"
page_title: "AWS: aws_iot_role_alias"
description: |-
  Provides an IoT role alias.
---

# Resource: aws_iot_role_alias

Provides an IoT role alias.

## Example Usage

```terraform
data "aws_iam_policy_document" "assume_role" {
  effect = "Allow"

  principals {
    type        = "Service"
    identifiers = ["credentials.iot.amazonaws.com"]
  }

  actions = ["sts:AssumeRole"]
}

resource "aws_iam_role" "role" {
  name               = "dynamodb-access-role"
  assume_role_policy = data.aws_iam_policy_document.assume_role.json
}

resource "aws_iot_role_alias" "alias" {
  alias    = "Thermostat-dynamodb-access-role-alias"
  role_arn = aws_iam_role.role.arn
}
```

## Argument Reference

This resource supports the following arguments:

* `alias` - (Required) The name of the role alias.
* `role_arn` - (Required) The identity of the role to which the alias refers.
* `credential_duration` - (Optional) The duration of the credential, in seconds. If you do not specify a value for this setting, the default maximum of one hour is applied. This setting can have a value from 900 seconds (15 minutes) to 43200 seconds (12 hours).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN assigned by AWS to this role alias.

## Import

Import IOT Role Alias using the alias. For example:

```sh
$ terraform import aws_iot_role_alias.example myalias
```
