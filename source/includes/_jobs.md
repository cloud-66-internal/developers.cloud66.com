# Jobs

## Jobs list

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
response = token.get("#{api_url}/stacks/#{stack_id}/jobs.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{id}/jobs HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": [
        {
            "uid": "b375afb170b468c238be44cec1058d0f",
            "name": "pies",
            "type": "DockerHostTaskJob",
            "cron": "01 00 1 * *",
            "status": 3,
            "paused": false,
            "params": {
                "command": "ls -lta"
            },
            "created_at": "2023-10-24 15:38:29 UTC",
            "updated_at": "2023-10-24 15:39:14 UTC"
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

Get list of all jobs of a stack.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{id}/jobs`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | stack UID | `5999b763474b0eafa5fafb64bff0ba80`

## Run a job

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
id = 98ee5a9b93919d9b63bd5377636675bd
response = token.get("#{api_url}/stacks/#{stack_id}/jobs/{job_id}/run_now.json")

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/jobs/{job_id}/run_now HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":
    {
      "id":2593,
      "user":"test@example.com",
      "resource_type":"stack",
      "action":"job_run_now",
      "resource_id":"1602",
      "started_via":"api",
      "started_at":"2016-02-04T12:52:24Z",
      "finished_at":null,
      "finished_success":null,
      "finished_message":null
    }
}
```

Run the job.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/jobs/{job_id}/run_now`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
job_id | **required** | string | Job ID | `98ee5a9b93919d9b63bd5377636675bd`
job_args | **optional** | string | Arguments passed to the command | `Arg1`


## Pause job

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
id = 98ee5a9b93919d9b63bd5377636675bd
response = token.post("#{api_url}/stacks/#{stack_id}/jobs/{job_id}/pause.json")

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/jobs/{job_id}/pause HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "id": 6626835,
        "user": "peep@parp.com",
        "resource_type": "stack",
        "action": "job_pause_handler",
        "resource_id": "84195",
        "started_via": "api",
        "started_at": "2023-10-27T14:07:38Z",
        "finished_at": null,
        "finished_success": null,
        "finished_message": null,
        "finished_result": null,
        "metadata": {}
    }
}
```

Pause a specific job running on this stack.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/jobs/{job_id}/pause`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
job_id | **required** | string | Job ID | `98ee5a9b93919d9b63bd5377636675bd`

## Unpause job

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
id = 98ee5a9b93919d9b63bd5377636675bd
response = token.post("#{api_url}/stacks/#{stack_id}/jobs/{job_id}/unpause.json")

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/jobs/{job_id}/unpause HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "id": 6626835,
        "user": "peep@parp.com",
        "resource_type": "stack",
        "action": "job_pause_handler",
        "resource_id": "84195",
        "started_via": "api",
        "started_at": "2023-10-27T14:07:38Z",
        "finished_at": null,
        "finished_success": null,
        "finished_message": null,
        "finished_result": null,
        "metadata": {}
    }
}
```

Unpause a specific job.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/jobs/{job_id}/unpause`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
job_id | **required** | string | Job ID | `98ee5a9b93919d9b63bd5377636675bd`


## Pause all jobs

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
id = 98ee5a9b93919d9b63bd5377636675bd
response = token.post("#{api_url}/stacks/#{stack_id}/jobs/pause_all.json")

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/jobs/pause_all HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "id": 6626835,
        "user": "peep@parp.com",
        "resource_type": "stack",
        "action": "job_pause_handler",
        "resource_id": "84195",
        "started_via": "api",
        "started_at": "2023-10-27T14:07:38Z",
        "finished_at": null,
        "finished_success": null,
        "finished_message": null,
        "finished_result": null,
        "metadata": {}
    }
}
```

Pause all the jobs for this stack.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/jobs/pause_all`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`



## Pause all jobs

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
id = 98ee5a9b93919d9b63bd5377636675bd
response = token.post("#{api_url}/stacks/#{stack_id}/jobs/unpause_all.json")

puts JSON.parse(response.body)['response']
```

```http
POST /stacks/{stack_id}/jobs/unpause_all HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "id": 6626835,
        "user": "peep@parp.com",
        "resource_type": "stack",
        "action": "job_pause_handler",
        "resource_id": "84195",
        "started_via": "api",
        "started_at": "2023-10-27T14:07:38Z",
        "finished_at": null,
        "finished_success": null,
        "finished_message": null,
        "finished_result": null,
        "metadata": {}
    }
}
```

Unpause all the jobs for this stack.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`POST /stacks/{stack_id}/jobs/unpause_all`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`



