# Failover Groups

## List Failover Groups

```ruby
response = token.get("#{api_url}/clouds.json")

puts JSON.parse(response.body)['response']
```

```http
GET /failover_groups HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": [
        {
            "uid": "fg-5be3dca6d3c4bf1eaddcb5b555d993bb",
            "address": "958-797-516.cloud66.net",
            "current_stack": 1,
            "primary_stack_uid": null,
            "primary_stack_name": null,
            "secondary_stack_uid": null,
            "secondary_stack_name": null,
            "busy_toggling": false,
            "readonly": false,
            "created_at": "2018-11-23T14:44:03Z",
            "updated_at": "2021-12-06T11:43:46Z"
        }
    ],
    "count": 1
}
```

Get a list of all the Failover Groups for the Cloud 66 account.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET / failover_groups`

## Create Failover Group

```ruby
response = token.post("#{api_url}/failover_groups.json")

puts JSON.parse(response.body)['response']
```

```http
POST /failover_groups HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "ok": true,
        "message": "Failover Group created"
    }
}

```

Create a new Failover Groups in a Cloud 66 account

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`POST / failover_groups`

### Query parameters

| Parameter | Presence | Data type | Description | Sample value |
| --- | --- | --- | --- | --- |
| primary_stack_uid | optional | string | The UID of the "primary" application in the Failover Group | `bf13586c5c8fbd6272f9ce78c74aea6c` |
| secondary_stack_uid | optional | string | The UID of the "secondary" application in the Failover Group | `bf13586c5c8fbd6272f9ce78c74aea6c` |
| current_stack | optional | int | Which application the Failover Group is currently pointed at. Valid options: `1` for the primary application or `2` for the secondary application. | `1` |


## Update	 Failover Group

```ruby
response = token.put("#{api_url}/failover_groups.json")

puts JSON.parse(response.body)['response']
```

```http
PUT /failover_groups HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "ok": true,
        "message": "Failover Group created"
    }
}

```

Update an existing Failover Groups in a Cloud 66 account. If  `primary_stack_uid` and/or `secondary_stack_uid` are set to an empty string, the existing application(s) will be removed from the Failover Group. If either of these parameters are not specified the current values will not be changed.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`PUT / failover_groups`

### Query parameters

| Parameter | Presence | Data type | Description | Sample value |
| --- | --- | --- | --- | --- |
| primary_stack_uid | optional | string | The UID of the application to set as the "primary" in the Failover Group. Will replace current value. | `bf13586c5c8fbd6272f9ce78c74aea6c` |
| secondary_stack_uid | optional | string | The UID of the application to set as the "secondary" in the Failover Group. Will replace current value. | `bf13586c5c8fbd6272f9ce78c74aea6c` |
| current_stack | optional | int | The application that the Failover Group should be pointed at. Valid options: `1` for the primary application or `2` for the secondary application. | -- |


## Delete	 Failover Group

```ruby
{fg_id} = '5999b763474b0eafa5fafb64bff0ba80'
response = token.delete("#{api_url}/failover_groups/#{fg_id}.json")

puts JSON.parse(response.body)['response']
```

```http
DELETE /failover_groups/fg-5be3dca6d3c4bf1eaddcb5b555d993bb HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "ok": true,
        "message": "Failover Group deleted"
    }
}

```

Delete an existing Failover Group from a Cloud 66 account.

### HTTP Request

`DELETE / failover_groups/{fg_id}`

### Query parameters

| Parameter | Presence | Data type | Description | Sample value |
| --- | --- | --- | --- | --- |
| fg_uid | required | string | The UID of the Failover Group that will be deleted | `fg-5be3dca6d3c4bf1eaddcb5b555d993bb` |