## Requirements

| Name | Version |
|------|---------|
| terraform | ~> 0.12.0 |
| aws | ~> 2.0 |
| null | ~> 2.0 |
| template | ~> 2.0 |

## Providers

| Name | Version |
|------|---------|
| aws | ~> 2.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| allocated\_storage | The allocated storage in GBs | `number` | n/a | yes |
| allow\_major\_version\_upgrade | Allow major version upgrade | `bool` | `false` | no |
| allowed\_cidr\_blocks | The whitelisted CIDRs which to allow `ingress` traffic to the DB instance | `list(string)` | `[]` | no |
| apply\_immediately | Specifies whether any database modifications are applied immediately, or during the next maintenance window | `bool` | `false` | no |
| associate\_security\_group\_ids | The IDs of the existing security groups to associate with the DB instance | `list(string)` | `[]` | no |
| attributes | Additional attributes (e.g. `1`) | `list(string)` | `[]` | no |
| auto\_minor\_version\_upgrade | Allow automated minor version upgrade (e.g. from Postgres 9.5.3 to Postgres 9.5.4) | `bool` | `true` | no |
| backup\_retention\_period | Backup retention period in days. Must be > 0 to enable backups | `number` | `0` | no |
| backup\_window | When AWS can perform DB snapshots, can't overlap with maintenance window | `string` | `"22:00-03:00"` | no |
| ca\_cert\_identifier | The identifier of the CA certificate for the DB instance | `string` | `"rds-ca-2019"` | no |
| copy\_tags\_to\_snapshot | Copy tags from DB to a snapshot | `bool` | `true` | no |
| database\_name | The name of the database to create when the DB instance is created | `string` | n/a | yes |
| database\_password | (Required unless a snapshot\_identifier or replicate\_source\_db is provided) Password for the master DB user | `string` | `""` | no |
| database\_port | Database port (\_e.g.\_ `3306` for `MySQL`). Used in the DB Security Group to allow access to the DB instance from the provided `security_group_ids` | `number` | n/a | yes |
| database\_user | (Required unless a `snapshot_identifier` or `replicate_source_db` is provided) Username for the master DB user | `string` | `""` | no |
| db\_options | A list of DB options to apply with an option group. Depends on DB engine | <pre>list(object({<br>    db_security_group_memberships  = list(string)<br>    option_name                    = string<br>    port                           = number<br>    version                        = string<br>    vpc_security_group_memberships = list(string)<br><br>    option_settings = list(object({<br>      name  = string<br>      value = string<br>    }))<br>  }))</pre> | `[]` | no |
| db\_parameter | A list of DB parameters to apply. Note that parameters may differ from a DB family to another | <pre>list(object({<br>    apply_method = string<br>    name         = string<br>    value        = string<br>  }))</pre> | `[]` | no |
| db\_parameter\_group | Parameter group, depends on DB engine used | `string` | n/a | yes |
| deletion\_protection | Set to true to enable deletion protection on the RDS instance | `bool` | `false` | no |
| delimiter | Delimiter to be used between `namespace`, `environment`, `stage`, `name` and `attributes` | `string` | `"-"` | no |
| dns\_zone\_id | The ID of the DNS Zone in Route53 where a new DNS record will be created for the DB host name | `string` | `""` | no |
| enabled | Set to false to prevent the module from creating any resources | `bool` | `true` | no |
| enabled\_cloudwatch\_logs\_exports | List of log types to enable for exporting to CloudWatch logs. If omitted, no logs will be exported. Valid values (depending on engine): alert, audit, error, general, listener, slowquery, trace, postgresql (PostgreSQL), upgrade (PostgreSQL). | `list(string)` | `[]` | no |
| engine | Database engine type | `string` | n/a | yes |
| engine\_version | Database engine version, depends on engine type | `string` | n/a | yes |
| environment | Environment, e.g. 'prod', 'staging', 'dev', 'pre-prod', 'UAT' | `string` | `""` | no |
| final\_snapshot\_identifier | Final snapshot identifier e.g.: some-db-final-snapshot-2019-06-26-06-05 | `string` | `""` | no |
| host\_name | The DB host name created in Route53 | `string` | `"db"` | no |
| iam\_database\_authentication\_enabled | Specifies whether or mappings of AWS Identity and Access Management (IAM) accounts to database accounts is enabled | `bool` | `false` | no |
| instance\_class | Class of RDS instance | `string` | n/a | yes |
| iops | The amount of provisioned IOPS. Setting this implies a storage\_type of 'io1'. Default is 0 if rds storage type is not 'io1' | `number` | `0` | no |
| kms\_key\_arn | The ARN of the existing KMS key to encrypt storage | `string` | `""` | no |
| license\_model | License model for this DB. Optional, but required for some DB Engines. Valid values: license-included \| bring-your-own-license \| general-public-license | `string` | `""` | no |
| maintenance\_window | The window to perform maintenance in. Syntax: 'ddd:hh24:mi-ddd:hh24:mi' UTC | `string` | `"Mon:03:00-Mon:04:00"` | no |
| major\_engine\_version | Database MAJOR engine version, depends on engine type | `string` | `""` | no |
| max\_allocated\_storage | The upper limit to which RDS can automatically scale the storage in GBs | `number` | `0` | no |
| monitoring\_interval | The interval, in seconds, between points when Enhanced Monitoring metrics are collected for the DB instance. To disable collecting Enhanced Monitoring metrics, specify 0. Valid Values are 0, 1, 5, 10, 15, 30, 60. | `string` | `"0"` | no |
| multi\_az | Set to true if multi AZ deployment must be supported | `bool` | `false` | no |
| name | Solution name, e.g. 'app' or 'jenkins' | `string` | `""` | no |
| namespace | Namespace, which could be your organization name or abbreviation, e.g. 'eg' or 'cp' | `string` | `""` | no |
| option\_group\_name | Name of the DB option group to associate | `string` | `""` | no |
| parameter\_group\_name | Name of the DB parameter group to associate | `string` | `""` | no |
| performance\_insights\_enabled | Specifies whether Performance Insights are enabled. | `bool` | `false` | no |
| performance\_insights\_kms\_key\_id | The ARN for the KMS key to encrypt Performance Insights data. Once KMS key is set, it can never be changed. | `string` | `null` | no |
| performance\_insights\_retention\_period | The amount of time in days to retain Performance Insights data. Either 7 (7 days) or 731 (2 years). | `number` | `7` | no |
| publicly\_accessible | Determines if database can be publicly available (NOT recommended) | `bool` | `false` | no |
| security\_group\_ids | The IDs of the security groups from which to allow `ingress` traffic to the DB instance | `list(string)` | `[]` | no |
| skip\_final\_snapshot | If true (default), no snapshot will be made before deleting DB | `bool` | `true` | no |
| snapshot\_identifier | Snapshot identifier e.g: rds:production-2019-06-26-06-05. If specified, the module create cluster from the snapshot | `string` | `""` | no |
| stage | Stage, e.g. 'prod', 'staging', 'dev', OR 'source', 'build', 'test', 'deploy', 'release' | `string` | `""` | no |
| storage\_encrypted | (Optional) Specifies whether the DB instance is encrypted. The default is false if not specified | `bool` | `false` | no |
| storage\_type | One of 'standard' (magnetic), 'gp2' (general purpose SSD), or 'io1' (provisioned IOPS SSD) | `string` | `"standard"` | no |
| subnet\_ids | List of subnets for the DB | `list(string)` | n/a | yes |
| tags | Additional tags (e.g. `map('BusinessUnit','XYZ')` | `map(string)` | `{}` | no |
| timezone | (Optional) Time zone of the DB instance. timezone is currently only supported by Microsoft SQL Server. The timezone can only be set on creation. | `string` | `null` | no |
| vpc\_id | VPC ID the DB instance will be created in | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| hostname | DNS host name of the instance |
| instance\_address | Address of the instance |
| instance\_arn | ARN of the instance |
| instance\_endpoint | DNS Endpoint of the instance |
| instance\_id | ID of the instance |
| option\_group\_id | ID of the Option Group |
| parameter\_group\_id | ID of the Parameter Group |
| security\_group\_id | ID of the Security Group |
| subnet\_group\_id | ID of the Subnet Group |

