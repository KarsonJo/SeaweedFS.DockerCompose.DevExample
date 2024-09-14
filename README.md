# Introduction

A seaweedFS setup for development.

# Get started
```bash
$ docker compose up -d
```

# Containers

## seaweedfs

A single node seaweedFS instance with S3 API enabled.

## aws

Aws cli.

## nginx

A reversed proxy for seaweedFS.

# Suggested debug clients

## Postman

Postman can generate AWS authorization header for you.

## AWS cli

1. AWS Cli can also authorize by providing `accese_key` and `secret_key`.
2. The docker compose setup provide a service (`aws`) that preinstalled with AWS cli.

# Usage

## environment

| name              | value                     |
| ----------------- | ------------------------- |
| aws s3 access key | admin                     |
| aws s3 secret key | P@ssw0rd                  |
| s3 host           | https://s3.swfs.lndo.site |

## Send a file

> All methods are compatible with AWS S3 API.

### Definition

```text
PUT https://s3.swfs.lndo.site/{bucket}/{key}
```

### Headers

#### Authorization

AWS Authorization signature.

### Body

Binary file data.

## Retrieve a file

### Definition

```text
GET https://s3.swfs.lndo.site/{bucket}/{key}
```

### Headers

#### Authorization

AWS Authorization signature.

## Retrieve a file from presigned URL

### Definition

```text
GET https://s3.swfs.lndo.site/{bucket}/{key}?<presign-signature>
```

### Get presign signature

Use the `aws` docker compose service to generate a signature.

Exec into the `aws` container and type the following command:

```bash
# presign url, default to 1 hour
$ aws --endpoint-url https://s3.swfs.lndo.site s3 presign s3://{bucket}/{key}
```

> 1. Change `{bucket}` and `{key}` to your file.
> 2. `--endpoint-url` should be the request hostname.
