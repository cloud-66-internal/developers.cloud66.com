# notifications

## List notifications

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
response = token.get("#{api_url}/stacks/#{stack_id}/notifications.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{stack_id}/notifications HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": [
        {
            "notification_name": "noticent_stack_provisioned_success",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "notification_name": "noticent_stack_provisioned_failed",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "notification_name": "noticent_stack_redeploy_success",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "notification_name": "noticent_stack_redeploy_failed",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "notification_name": "noticent_server_stopped",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "notification_name": "noticent_server_back",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        }
   ],
    "count": 33
}

```

List the notifications configured on an application.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{stack_id}/notifications/`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | Unique identifier of the application | `5999b763474b0eafa5fafb64bff0ba80`

## notifications info

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
notification_name = `noticent_stack_update_failed`
response = token.get("#{api_url}/stacks/#{stack_id}/notifications/#{notification_name}.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/5999b763474b0eafa5fafb64bff0ba80/notifications/noticent_stack_provisioned_success HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "notification_name": "noticent_stack_provisioned_success",
        "subscriptions": [
            {
                "channel": "email"
            }
        ]
    }
}
```

Get information of a single notification

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{stack_id}/notifications/{notification_name}/`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The application's UID | `5999b763474b0eafa5fafb64bff0ba80`
notification_name | **required** | string | The name of the notification to query | `noticent_stack_update_failed`

## notifications update

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'

response = token.patch("#{api_url}/stacks/#{stack_id}/notifications.json", {body:{"notifications":[{"notification_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}})

puts JSON.parse(response.body)['response']

```

```http
PATCH /stacks/{stack_id}/notifications/ HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "successes": {
            "notifications": [
                "noticent_stack_health_check_failed"
            ],
            "count": 1
        },
        "not_applicable": {
            "notifications": [],
            "count": 0
        },
        "failures": {
            "notifications": [],
            "count": 0
        }
    }
}

```

Update the notifications for an application. You can use the JSON response from one application to effectively copy those settings to another application. 

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`PATCH /stacks/{stack_id}/notifications/`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | Unique identifier of the stack | `5999b763474b0eafa5fafb64bff0ba80`
notifications | **required** | json | A JSON formatted description of notification settings | {"notifications":[{"notification_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}

## notifications update application group

```ruby
application_group_name = 'production-apps'

response = token.patch("#{api_url}/application_groups/#{application_group_name}/notifications.json", {body:{"notifications":[{"notification_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}})

puts JSON.parse(response.body)['response']
```

```http
PATCH /application_groups/notifications/ HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "successes": {
            "notifications": [
                "noticent_stack_health_check_failed"
            ],
            "count": 1
        },
        "not_applicable": {
            "notifications": [],
            "count": 0
        },
        "failures": {
            "notifications": [],
            "count": 0
        }
    }
}

```

Update the notifications for an application group. You can use the JSON response from one application to effectively copy those settings to an entire application group. 

### HTTP Request

`PATCH /application_groups/notifications`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
application_group_name | **required** | string | Name of the application group | `production-apps`
notifications | **required** | json | A JSON formatted description of notification settings | {"notifications":[{"notification_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}