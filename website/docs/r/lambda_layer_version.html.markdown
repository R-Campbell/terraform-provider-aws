---
subcategory: "Lambda"
layout: "aws"
page_title: "AWS: aws_lambda_layer_version"
description: |-
  Provides a Lambda Layer Version resource. Lambda Layers allow you to reuse shared bits of code across multiple lambda functions.
---

# Resource: aws_lambda_layer_version

Provides a Lambda Layer Version resource. Lambda Layers allow you to reuse shared bits of code across multiple lambda functions.

For information about Lambda Layers and how to use them, see [AWS Lambda Layers][1].

~> **NOTE:** Setting `skip_destroy` to `true` means that the AWS Provider will _not_ destroy any layer version, even when running `terraform destroy`. Layer versions are thus intentional dangling resources that are _not_ managed by Terraform and may incur extra expense in your AWS account.

## Example Usage

```terraform
resource "aws_lambda_layer_version" "lambda_layer" {
  filename   = "lambda_layer_payload.zip"
  layer_name = "lambda_layer_name"

  compatible_runtimes = ["nodejs16.x"]
}
```

## Specifying the Deployment Package

AWS Lambda Layers expect source code to be provided as a deployment package whose structure varies depending on which `compatible_runtimes` this layer specifies.
See [Runtimes][2] for the valid values of `compatible_runtimes`.

Once you have created your deployment package you can specify it either directly as a local file (using the `filename` argument) or
indirectly via Amazon S3 (using the `s3_bucket`, `s3_key` and `s3_object_version` arguments). When providing the deployment
package via S3 it may be useful to use [the `aws_s3_object` resource](s3_object.html) to upload it.

For larger deployment packages it is recommended by Amazon to upload via S3, since the S3 API has better support for uploading large files efficiently.

## Argument Reference

The following arguments are required:

* `layer_name` - (Required) Unique name for your Lambda Layer

The following arguments are optional:

* `compatible_architectures` - (Optional) List of [Architectures][4] this layer is compatible with. Currently `x86_64` and `arm64` can be specified.
* `compatible_runtimes` - (Optional) List of [Runtimes][2] this layer is compatible with. Up to 5 runtimes can be specified.
* `description` - (Optional) Description of what your Lambda Layer does.
* `filename` (Optional) Path to the function's deployment package within the local filesystem. If defined, The `s3_`-prefixed options cannot be used.
* `license_info` - (Optional) License info for your Lambda Layer. See [License Info][3].
* `s3_bucket` - (Optional) S3 bucket location containing the function's deployment package. Conflicts with `filename`. This bucket must reside in the same AWS region where you are creating the Lambda function.
* `s3_key` - (Optional) S3 key of an object containing the function's deployment package. Conflicts with `filename`.
* `s3_object_version` - (Optional) Object version containing the function's deployment package. Conflicts with `filename`.
* `skip_destroy` - (Optional) Whether to retain the old version of a previously deployed Lambda Layer. Default is `false`. When this is not set to `true`, changing any of `compatible_architectures`, `compatible_runtimes`, `description`, `filename`, `layer_name`, `license_info`, `s3_bucket`, `s3_key`, `s3_object_version`, or `source_code_hash` forces deletion of the existing layer version and creation of a new layer version.
* `source_code_hash` - (Optional) Used to trigger updates. Must be set to a base64-encoded SHA256 hash of the package file specified with either `filename` or `s3_key`. The usual way to set this is `${filebase64sha256("file.zip")}` (Terraform 0.11.12 or later) or `${base64sha256(file("file.zip"))}` (Terraform 0.11.11 and earlier), where "file.zip" is the local filename of the lambda layer source archive.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Lambda Layer with version.
* `created_date` - Date this resource was created.
* `layer_arn` - ARN of the Lambda Layer without version.
* `signing_job_arn` - ARN of a signing job.
* `signing_profile_version_arn` - ARN for a signing profile version.
* `source_code_size` - Size in bytes of the function .zip file.
* `version` - Lambda Layer version.

[1]: https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html
[2]: https://docs.aws.amazon.com/lambda/latest/dg/API_PublishLayerVersion.html#SSS-PublishLayerVersion-request-CompatibleRuntimes
[3]: https://docs.aws.amazon.com/lambda/latest/dg/API_PublishLayerVersion.html#SSS-PublishLayerVersion-request-LicenseInfo
[4]: https://docs.aws.amazon.com/lambda/latest/dg/API_PublishLayerVersion.html#SSS-PublishLayerVersion-request-CompatibleArchitectures

## Import

Import Lambda Layers using `arn`. For example:

```
$ terraform import \
    aws_lambda_layer_version.test_layer \
    arn:aws:lambda:_REGION_:_ACCOUNT_ID_:layer:_LAYER_NAME_:_LAYER_VERSION_
```
