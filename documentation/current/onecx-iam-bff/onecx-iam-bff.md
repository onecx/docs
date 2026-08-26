# undefined

 Configuration property fixed at build time - All other configuration properties are overridable at runtime

| Configuration property                                                                                                                                                                                                                          | Type    | Default  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- |
| [onecx.iam.clients."clients".url](#onecx-iam-bff%5Fonecx-iam-clients-clients-url) Url of the iam rest client. Environment variable: ONECX\_IAM\_CLIENTS\_\_CLIENTS\_\_URL                                                                       | string  | required |
| [onecx.iam.clients."clients".shared](#onecx-iam-bff%5Fonecx-iam-clients-clients-shared) Set to true to share the HTTP client between REST clients. Environment variable: ONECX\_IAM\_CLIENTS\_\_CLIENTS\_\_SHARED                               | boolean | true     |
| [onecx.iam.clients."clients".connection-pool-size](#onecx-iam-bff%5Fonecx-iam-clients-clients-connection-pool-size) The size of the rest client connection pool. Environment variable: ONECX\_IAM\_CLIENTS\_\_CLIENTS\_\_CONNECTION\_POOL\_SIZE | int     | 30       |
