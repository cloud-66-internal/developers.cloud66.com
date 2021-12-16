# Alerts

## Alerts list

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
response = token.get("#{api_url}/stacks/#{stack_id}/alerts.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/{stack_id}/alerts HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": [
        {
            "alert_name": "noticent_stack_provisioned_success",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "alert_name": "noticent_stack_provisioned_failed",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "alert_name": "noticent_stack_redeploy_success",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "alert_name": "noticent_stack_redeploy_failed",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "alert_name": "noticent_server_stopped",
            "subscriptions": [
                {
                    "channel": "email"
                }
            ]
        },
        {
            "alert_name": "noticent_server_back",
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

List the alerts configured on an application.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /stacks/{stack_id}/alerts/`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | Unique identifier of the application | `5999b763474b0eafa5fafb64bff0ba80`

## Alerts info

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
alert_name = `noticent_stack_update_failed`
response = token.get("#{api_url}/stacks/#{stack_id}/alerts/#{alert_name}.json")

puts JSON.parse(response.body)['response']
```

```http
GET /stacks/5999b763474b0eafa5fafb64bff0ba80/alerts/noticent_stack_provisioned_success HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "alert_name": "noticent_stack_provisioned_success",
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

`GET /stacks/{stack_id}/alerts/{alert_name}/`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | The application's UID | `5999b763474b0eafa5fafb64bff0ba80`
alert_name | **required** | string | The name of the alert to query | `noticent_stack_update_failed`

## Alerts update

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'

response = token.patch("#{api_url}/stacks/#{stack_id}/alerts.json", {body:{"alerts":[{"alert_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}})

puts JSON.parse(response.body)['response']

```

```http
PATCH /stacks/{stack_id}/alerts/ HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "successes": {
            "alerts": [
                "noticent_stack_health_check_failed"
            ],
            "count": 1
        },
        "not_applicable": {
            "alerts": [],
            "count": 0
        },
        "failures": {
            "alerts": [],
            "count": 0
        }
    }
}

```

Update the alerts for an application. You can use the JSON response from one application to effectively copy those settings to another application. 

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`PATCH /stacks/{stack_id}/alerts/`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
stack_id | **required** | string | Unique identifier of the stack | `5999b763474b0eafa5fafb64bff0ba80`
alerts | **required** | json | A JSON formatted description of alert settings | {"alerts":[{"alert_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}

## Alerts update application group

```ruby
application_group_name = 'production-apps'

response = token.patch("#{api_url}/application_groups/#{application_group_name}/alerts.json", {body:{"alerts":[{"alert_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}})

puts JSON.parse(response.body)['response']
```

```http
PATCH /application_groups/alerts/ HTTP/1.1
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "response": {
        "successes": {
            "alerts": [
                "noticent_stack_health_check_failed"
            ],
            "count": 1
        },
        "not_applicable": {
            "alerts": [],
            "count": 0
        },
        "failures": {
            "alerts": [],
            "count": 0
        }
    }
}

```

Update the alerts for an application group. You can use the JSON response from one application to effectively copy those settings to an entire application group. 

### HTTP Request

`PATCH /application_groups/alerts`

### Query parameters 

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
application_group_name | **required** | string | Name of the application group | `production-apps`
alerts | **required** | json | A JSON formatted description of alert settings | {"alerts":[{"alert_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}