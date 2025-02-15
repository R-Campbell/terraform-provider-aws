---
subcategory: "Transit Gateway"
layout: "aws"
page_title: "AWS: aws_ec2_transit_gateway_route_table"
description: |-
  Get information on an EC2 Transit Gateway Route Table
---


<!-- Please do not edit this file, it is generated. -->
# Data Source: aws_ec2_transit_gateway_route_table

Get information on an EC2 Transit Gateway Route Table.

## Example Usage

### By Filter

```typescript
// Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { DataAwsEc2TransitGatewayRouteTable } from "./.gen/providers/aws/data-aws-ec2-transit-gateway-route-table";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new DataAwsEc2TransitGatewayRouteTable(this, "example", {
      filter: [
        {
          name: "default-association-route-table",
          values: ["true"],
        },
        {
          name: "transit-gateway-id",
          values: ["tgw-12345678"],
        },
      ],
    });
  }
}

```

### By Identifier

```typescript
// Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { DataAwsEc2TransitGatewayRouteTable } from "./.gen/providers/aws/data-aws-ec2-transit-gateway-route-table";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new DataAwsEc2TransitGatewayRouteTable(this, "example", {
      id: "tgw-rtb-12345678",
    });
  }
}

```

## Argument Reference

The following arguments are supported:

* `filter` - (Optional) One or more configuration blocks containing name-values filters. Detailed below.
* `id` - (Optional) Identifier of the EC2 Transit Gateway Route Table.

### filter Argument Reference

* `name` - (Required) Name of the filter.
* `values` - (Required) List of one or more values for the filter.

## Attribute Reference

In addition to all arguments above, the following attributes are exported:

* `arn` - EC2 Transit Gateway Route Table ARN.
* `defaultAssociationRouteTable` - Boolean whether this is the default association route table for the EC2 Transit Gateway
* `defaultPropagationRouteTable` - Boolean whether this is the default propagation route table for the EC2 Transit Gateway
* `id` - EC2 Transit Gateway Route Table identifier
* `transitGatewayId` - EC2 Transit Gateway identifier
* `tags` - Key-value tags for the EC2 Transit Gateway Route Table

## Timeouts

[Configuration options](https://developer.hashicorp.com/terraform/language/resources/syntax#operation-timeouts):

- `read` - (Default `20M`)

<!-- cache-key: cdktf-0.17.1 input-1208f03f1c84c0e2ce61d9b6b1a78aed169974d74a04009ae9e848da55024189 -->