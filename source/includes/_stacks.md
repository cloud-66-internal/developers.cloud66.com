# Stacks
<aside class="notice">
Most interactions with the Cloud 66 API are performed at the stack level. Using the Stacks resource, you can list stacks and view stack details, but you can only create, update, or delete stacks using the UI dashboard. However, new Docker-only stacks can also be created using API.
</aside>

### Methods

Using the Stacks endpoint, you can submit requests using the following methods.

* List all stacks
* View a stack
* Create a new stack (Docker only)
* List all stack actions
* View a stack action
* Perform a stack action
* Add an SSL certificate to a stack


## Stack List

```ruby
response = token.get("#{api_url}/stacks.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": [
        {
            "uid": "5999b763474b0eafa5fafb64bff0ba80",
            "name": "Awesome App",
            "git": "http://github.com/cloud66-samples/awesome-app.git",
            "git_branch": "fig",
            "environment": "production",
            "cloud": "DigitalOcean",
            "fqdn": "awesome-app.dev.c66.me",
            "language": "ruby",
            "framework": "rails",
            "status": 1,
            "health": 3,
            "last_activity": "2014-08-14T01:46:53+00:00",
            "last_activity_iso": "2014-08-14T01:46:53+00:00",
            "maintenance_mode": false,
            "has_loadbalancer": false,
            "created_at": "2014-08-14 00:38:14 UTC",
            "updated_at": "2014-08-14 01:46:52 UTC",
            "deploy_directory": "/var/deploy/awesome_app",
            "cloud_status": "partial",
            "created_at_iso": "2014-08-14T00:38:14Z",
            "updated_at_iso": "2014-08-14T01:46:52Z",
            "redeploy_hook": "http://hooks.cloud66.com/stacks/redeploy/b806f1c3344eb3aa2a024b23254b75b3/6d677352a6b2eefec6e345ee2b491521"
        }
    ],
    "count": 1,
    "pagination": {
        "previous": null,
        "next": null,
        "current": 1,
        "per_page": 30,
        "count": 1,
        "pages": 1
    }
}
```

Retrieves a paged list of all the stack objects the user can access.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks`

### The stack object

| Property | Data type | Description | Sample value |
| ---------- | ------------ | -------------------------------- | ------------- |
| uid | string | The unique identifier of the stack. | `5999b763474b0eafa5fafb64bff0ba80` |
| name | string | The name defined for the stack. | `My Awesome App` |
| git | string | The git repository URL associated with the stack. | `http://github.com/mysamples/awesome-app.git` |
| git_branch | string | The git repository branch associated with the stack. | `fig` |
| environment | string | The environment associated with the stack. | `production` |
| cloud | string | The cloud provider associated with the stack. | `DigitalOcean` |
| fqdn | string | The fully qualified namespace of the stack. | `awesome-app.dev.c66.me` |
| language | string | The programming language of the stack. | `ruby` |
| framework | string | The framework used for the stack. | `rails` |
| status | int | The current [status code](#stack-status-values) for the stack. | `1` |
| health | int | The current [health code](#stack-health-status-values) for the stack. | `3` |
| last_activity | datetime | The date and time the last action was performed for the stack, in UTC datetime. | `2014-08-14T01:46:53+00:00` |
| last_activity_iso | datetime | The date and time the last action was performed for the stack, in UTC datetime | `2014-08-14T01:46:53+00:00` |
| maintenance mode | bool | Whether the stack currently has maintenance mode enabled. | `false` |
| has_loadbalancer | bool | Whether the stack has an associated load balancer add-in. | `false` |
| created_at | datetime | The date and time the stack was created, in iso8601 format | `2014-09-01T19:08:05Z` |
| updated_at | datetime | The date and time the stack was last modified, in iso8601 format | `2014-09-01T19:18:05Z` |
| deploy_directory | string | The target directory for stack deployment. | `/var/deploy/awesome_app` |
| cloud_status | string | The current cloud provider status associated with the stack. | `partial` |
| redeploy_hook | string | If applicable, the deploy hook URL associated with the stack. | `http://hooks.cloud66.com/stacks/redeploy/ b806f1c3344eb3aa2a024b23254b75b3/6d677352a6b2eefec6e345ee2b491521` |

## Stack

```ruby
id = 'a6b583684833a2cf4845079c9d9350a8'
response = token.get("#{api_url}/stacks/#{id}.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
"response":
  {
    "uid": "5999b763474b0eafa5fafb64bff0ba80",
      "name": "Awesome App",
      "git": "http://github.com/cloud66-samples/awesome-app.git",
      "git_branch": "fig",
      "environment": "production",
      "cloud": "DigitalOcean",
      "fqdn": "awesome-app.dev.c66.me",
      "language": "ruby",
      "framework": "rails",
      "status": 1,
      "health": 3,
      "last_activity": "2014-08-14T01:46:53+00:00",
      "last_activity_iso": "2014-08-14T01:46:53+00:00",
      "maintenance_mode": false,
      "has_loadbalancer": false,
      "created_at": "2014-08-14 00:38:14 UTC",
      "updated_at": "2014-08-14 01:46:52 UTC",
      "deploy_directory": "/var/deploy/awesome_app",
      "cloud_status": "partial",
      "created_at_iso": "2014-08-14T00:38:14Z",
      "updated_at_iso": "2014-08-14T01:46:52Z",
      "redeploy_hook": "http://hooks.cloud66.com/stacks/redeploy/b806f1c3344eb3aa2a024b23254b75b3/6d677352a6b2eefec6e345ee2b491521"
  }
}
```

Retrieve the details of the stack specified in the request.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{id}`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
id | **required** | string | Unique identifier of the stack | `5999b763474b0eafa5fafb64bff0ba80`

### Stack status values

| Status | Code | Description |
| ----------- | :---: | ----------------------------------------- |
| STK_QUEUED | 0 | Pending analysis |
| STK_SUCCESS | 1 | Deployed successfully |
| STK_FAILED | 2 | Deployment failed |
| STK_ANALYSING | 3 | Analyzing |
| STK_ANALYSED | 4 | Analyzed |
| STK_QUEUED_FOR_DEPLOYING | 5 | Queued for deployment |
| STK_DEPLOYING | 6 | Deploying |
| STK_TERMINAL_FAILURE | 7 | Unable to analyze |

### Stack health status values

| Status | Code | Description |
| ----------- | :---: | ------------------------------------------ |
| HLT_UNKNOWN | 0 | Unknown |
| HLT_BUILDING | 1 | Building |
| HLT_PARTIAL | 2 | Impaired |
| HLT_OK | 3 | Healthy |
| HLT_BROKEN | 4 | Failed |

## Stack Create

```ruby
service_file = File.read('path/to/service.yml')
manifest_file = File.read('path/to/manifest.yml')

#Using manifest.yml
response = token.post("#{api_url}/stacks.json", {body: {:name => 'new_stack_name', :environment => 'production', :service_yaml => service_file, :manifest_yaml => manifest_file}})

#Using separate parameters
response = token.post("#{api_url}/stacks.json", {body: {:name => 'new_stack_name', :environment => 'production', :service_yaml => service_file, :cloud => 'digitalocean', :region => 'ams1', :size => '1gb', :build_type => 'single'}})

puts JSON.parse(response.body)['response']
```

```http
POST /stacks HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{ "response":
    {
        "id":10,
        "user":"test@cloud66.com",
        "resource_type":"stack",
        "action":"stack_create",
        "resource_id":"283",
        "started_via":"api",
        "started_at":"2015-09-01T19:08:05Z",
        "finished_at":null,
        "finished_success":null,
        "finished_message":null
    }
}
```

Create and build a new docker stack. Either manifest definition, or `cloud`, `region`, `size` and `build_type` must be passed as params.

<aside class="notice">
<b>Scope:</b> <i>redeploy</i>
</aside>

### HTTP Request

`POST /stacks`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
name | **required** | string | New stack name | `new_stack_name`
environment | **required** | string | New stack environment | `production`
service_yaml | **required** | string | The services definition of the new docker stack | `service_yaml_serialised`
manifest_yaml | optional | string | The manifest definition of the new docker stack | `manifest_yaml_serialised`
cloud | optional | string | Cloud provider to create servers in | `aws`
key_name | optional | string | Name of the cloud provider key (`Default` or first available key for the cloud if not specified) | `my_key`
region | optional | string | Region within the cloud to create servers in | `us-east-1`
size | optional | string | Size of the server | `t1.micro`
build_type | optional | string | Deploy all services to `single` or `multi` servers | `multi`

## Stack Action list

```ruby
id = 'a6b583684833a2cf4845079c9d9350a8'
response = token.get("#{api_url}/stacks/#{id}/actions.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{id}/actions HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":
        [
    {
      "id": 6566418,
      "user": "person@company.com",
      "resource_type": "stack",
      "action": "application_deployment",
      "resource_id": "84195",
      "started_via": "api",
      "started_at": "2023-10-11T11:43:57Z",
      "finished_at": "2023-10-11T11:47:42Z",
      "finished_success": true,
      "finished_message": "Completed successfully",
      "finished_result": {},
      "metadata": {
                "user_reference": "my-useful-id" 
                }
    }
  ],
  "count":1,
  "pagination":
    {
      "previous":null,
      "next":null,
      "current":1,
      "per_page":30,
      "count":1,
      "pages":1
    }
}
```

Retrieve a paged list of all asynchronous actions performed for the stack specified in the request. You can filter actions by your own metadata using `user_reference` (note: metadata needs to be added to the action when it is invoked to be available here).

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{id}/actions`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
id | **required** | string | Unique identifier of the stack | `5999b763474b0eafa5fafb64bff0ba80`

### The stack action object

| Property | Data type | Description | Sample value |
| ------------- | --------- | ----------------------------------- | ---------------- |
| id | int | The numeric identifier of the stack action. Identifiers increment by one for each performed action. | `10` |
| user_reference | string (up to 255 chars) | Returns actions where the metadata matches the query. | `useful-reference-123` |
| user | string | The email address of the user who performed the stack action. | `hello@cloud66.com`|
| resource_type | string | The resource for which the action was performed, which is `stack` in this case. | `stack` |
| action | string | The action that was performed for the stack. | `restart` |
| resource_id | int | The unique ID of the resource | `283` |
| started_via | string | The process that initiated the action, which is the UI, API, or command line. | `api` |
| started_at | datetime | The date and time the action was initiated, in UTC datetime. | `2014-09-01T19:08:05Z` |
| finished_at | datetime | The date and time the action was completed, in UTC datetime. | `2014-09-01T19:08:09Z` |
| finished_success | bool | Whether the action completed successfully. | `true` |
| finished_message | string | If applicable, the system message associated with the completed action. | `null` |

## Stack Action

```ruby
stack_id = 'a6b583684833a2cf4845079c9d9350a8'
id = '202161'
response = token.get("#{api_url}/stacks/#{stack_id}/actions/#{id}.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{stack_id}/actions/{id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

    {
    "id": 6566418,
    "user": "person@company.com",
    "resource_type": "stack",
    "action": "application_deployment",
    "resource_id": "84195",
    "started_via": "api",
    "started_at": "2023-10-11T11:43:57Z",
    "finished_at": "2023-10-11T11:47:42Z",
    "finished_success": true,
    "finished_message": "Completed successfully",
    "finished_result": {},
    "metadata": {
        "user_reference": "my-useful-id" 
                }
    }
```

Retrieve the details of an asynchronous action performed for the the stack specified in the request based on the supplied action ID.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{stack_id}/actions/{id}`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | Unique identifier of the stack | `5999b763474b0eafa5fafb64bff0ba80`
id | **required** | integer | Identifier of the asynchronous action | `4153`

## Run Stack action

```ruby
stack_id = 'a6b583684833a2cf4845079c9d9350a8'
response = token.post("#{api_url}/stacks/#{stack_id}/actions.json", {body: {:command => 'clear_caches'}})

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/actions HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":
    {
      "id":10,
      "user":"test@cloud66.com",
      "resource_type":"stack",
      "action":"clear_caches",
      "resource_id":"283",
      "started_via":"api",
      "started_at":"2014-09-01T19:08:05Z",
      "finished_at":null,
      "finished_success":null,
      "finished_message":null
    }
}
```

Perform an asynchronous action for the stack specified in the request. You can use this method to restart the stack, clear the stack's cache, or enable maintenance mode.

<aside class="notice">
<b>Scope:</b> <i>redeploy</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/actions`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | Unique identifier of the stack | `5999b763474b0eafa5fafb64bff0ba80`
command | **required** | string | The action to perform for the stack. Valid values are `clear_caches`, `maintenance_mode`, and `restart`. | `restart`

| Command | Comments | Extra Parameters |
| ---------- | ---------- | ---------------- |
| container_restart | Restarts a particular container on the given stack | &bull; `container`:`5999b763474b0eafa5fafb64bff0ba80` |
| disable_replication_slave_db | Disable replication to the specified slave database server | &bull; `server`:`server-name`<br/> &bull;`server_group`: valid values `all`, `mysql`, `postgresql`, `redis`, `mongodb` |
| maintenance_mode | Enable to Disable maintenance mode for a stack. | &bull; `value`:`1` for enable or `0` for disable |
| process_pause | Pauses the specified process. | &bull; `process-name` |
| process_restart | Restarts the specified process. | &bull; `process-name` |
| process_resume | Resumes the specified process. | &bull; `process-name` |
| promote_slave_db | Promote the specified slave database server to a standalone master | &bull; `server`:`server-name`<br/> &bull;`server_group`: valid values `all`, `mysql`, `postgresql`, `redis`, `mongodb` |
| restart | Restarts all stack components (nginx, db, etc.) | None |
| resync_slave_db | Re-sync the specified slave database server with its master database server | &bull; `server`:`server-name`<br/> &bull;`server_group`: valid values `all`, `mysql`, `postgresql`, `redis`, `mongodb` |
| service_pause | Pauses all the containers from the given service | &bull; `service_name`:`api` <br/> &bull;`server_id_filter`:`474b30a8fea888df8468fc145ea49bac` (optional)  |
| service_restart | Restarts all the containers from the given service | &bull; `service_name`:`web` <br/> &bull;`server_id_filter`:`f8468fc145ea49bac474b30a8fea888d` (optional)  |
| service_resume | Pauses all the containers from the given service | &bull; `service_name`:`api` <br/> &bull;`server_id_filter`:`474b30a8fea888df8468fc145ea49bac` (optional)  |

## Reboot the Stack

```ruby
stack_id = 'a6b583684833a2cf4845079c9d9350a8'
response = token.post("#{api_url}/stacks/#{stack_id}/reboot_servers.json")

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/reboot_servers HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":
    {
      "id":10,
      "user":"test@cloud66.com",
      "resource_type":"stack",
      "action":"stack_reboot",
      "resource_id":"283",
      "started_via":"api",
      "started_at":"2016-01-01T19:08:05Z",
      "finished_at":null,
      "finished_success":null,
      "finished_message":null
    }
}
```

You can use this method to reboot the stack or speific server group of a stack.

<aside class="notice">
<b>Scope:</b> <i>reboot</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/reboot_servers`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | Unique identifier of the stack | `5999b763474b0eafa5fafb64bff0ba80`
strategy | **required** | string | parallel or serial | `parallel`
group | **optional** | string | all or web/db/redis etc (default is web) | `mysql`



## SSL certificate

```ruby
stack_id = 'JReEhI8LboQjFcI4hMmbgLqvPbMkgT7T'
response = token.post("#{api_url}/stacks/#{stack_id}/ssl_certificates.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{stack_id}/ssl_certificates HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": [
        {
            "uuid": "ssl-9ad095613rrr4e0b8f718302bab8709e",
            "name": "pp-ticker-prod-cllaz",
            "server_group_id": null,
            "server_names": "www.fyp111.co",
            "sha256_fingerprint": "481f22f00e117e209dbde4c2ae3831401109fc824784943e39a194a3adb64082",
            "ca_name": "Let's Encrypt",
            "type": "lets_encrypt",
            "wildcard": false,
            "dns_provider_uuid": null,
            "ssl_termination": true,
            "has_intermediate_cert": true,
            "status": 3,
            "created_at": "2023-01-26T10:23:34Z",
            "updated_at": "2023-01-26T10:26:29Z",
            "expires_at": "2023-04-26T09:24:32Z",
            "certificate": null,
            "key": null,
            "intermediate_certificate": null
        }
    ],
    "count": 1,
    "pagination": {
        "previous": null,
        "next": null,
        "current": 1,
        "per_page": 30,
        "count": 1,
        "pages": 1
    }
}
```

You can use this method to query, add, delete or update SSL certificates on a stack.

<aside class="notice">
<b>Scope:</b> <i>admin</i>
</aside>

### HTTP Request

`GET /stacks/:stack_id/ssl_certificates`

`POST /stacks/:stack_id/ssl_certificates`

`GET /stacks/:stack_id/ssl_certificates/:id`

`PATCH /stacks/:stack_id/ssl_certificates/:id` 

`PUT /stacks/:stack_id/ssl_certificates/:id` 

`DELETE /stacks/:stack_id/ssl_certificates/:id`

POST, PATCH and PUT should use the following object format:

`{"ssl_certificate":{"server_names":"mywebsite.com","ssl_termination":true,"type":"lets_encrypt","wildcard":true,"dns_provider_uuid":"dp-fbe3dd78cdc600b187b38c4d4b6b016b"}}`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
type | **required** | string | Type of certificate (`manual` or `lets_encrypt`) | `lets_encrypt`
ssl_termination | **required** | bool | Whether SSL certificate is terminated on the load balancer or not | `true`
server_names | **required** | string | comma separated list of domains | `hello.com,world.co.uk`
wildcard | **optional** | bool | Whether the certificate must support wildcarded domain names - only applies to type `lets_encrypt` | `false`
dns_provider_uuid | **required for wildcard certs** | string | DNS provider to use for the Let's Encrypt DNS challenge | `dp-fbe3dd78cdc...`
certificate | **required for manual certs** | string | The certificate address | -----BEGIN CERTIFICATE----- <br /> `entire cert hash` <br /> -----END CERTIFICATE----- |
key | **required for manual certs** | string | The certificate key | -----BEGIN RSA PRIVATE KEY----- <br /> `entire key hash` <br /> -----END RSA PRIVATE KEY-----
intermediate_certificate | **optional** | string | The intermediate certificate chain | -----BEGIN CERTIFICATE----- <br /> `entire cert hash` <br /> -----END CERTIFICATE-----


## DNS providers

```ruby
response = token.get("#{api_url}/dns_providers.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/dns_providers HTTP/1.1

{
    "response": [
        {
            "uuid": "dp-fbe3d478cdc610b187b38c1d2b6b016b",
            "type": "Cloudflare",
            "key": "My Cloudflare",
            "display_name": "Cloudflare (My Cloudflare)",
            "created_at": "2023-01-25T14:08:28Z",
            "updated_at": "2023-01-25T14:08:28Z"
        }
    ],
    "count": 1,
    "pagination": {
        "previous": null,
        "next": null,
        "current": 1,
        "per_page": 30,
        "count": 1,
        "pages": 1
    }
}

```

You can use this method to query, add, delete or update SSL certificates on a stack.

<aside class="notice">
<b>Scope:</b> <i>admin</i>
</aside>
