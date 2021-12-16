<<<<<<< HEAD
# notifications

## List notifications

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
response = token.get("#{api_url}/stacks/#{stack_id}/notifications.json")
=======
# Notifications

## Notifications list

```ruby
id = '5999b763474b0eafa5fafb64bff0ba80'
response = token.get("#{api_url}/stacks/#{id}/notifications.json")
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

puts JSON.parse(response.body)['response']
```

```http
<<<<<<< HEAD
GET /stacks/{stack_id}/notifications HTTP/1.1
=======
GET /stacks/{id}/notifications HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
<<<<<<< HEAD
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
=======
  "response":[
    {
      "id":1189,
      "user_id":18,
      "alert_type":"stack.provision.ok",
      "channels":["email"],
      "stack_id":"5acd43412ea412e32897c40d46f91183",
      "params":{},
      "created_at":"2014-05-29T17:29:54Z",
      "updated_at":"2014-05-29T17:29:54Z"
    },
    {
      "id":1190,
      "user_id":18,
      "alert_type":"stack.provision.fail",
      "channels":["email"],
      "stack_id":"5acd43412ea412e32897c40d46f91183",
      "params":{},
      "created_at":"2014-05-29T17:29:54Z",
      "updated_at":"2014-05-29T17:29:54Z"
    },
    {
      "id":1191,
      "user_id":18,
      "alert_type":"stack.redeploy.ok",
      "channels":["email"],
      "stack_id":"5acd43412ea412e32897c40d46f91183",
      "params":{},
      "created_at":"2014-05-29T17:29:54Z",
      "updated_at":"2014-05-29T17:29:54Z"
    }
  ],
  "count":30,
  "pagination":
    {
      "previous":null,
      "next":2,
      "current":1,
      "per_page":30,
      "count":48,
      "pages":2
    }
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)
}
```

<<<<<<< HEAD
List the notifications configured on an application.
=======
Get list of all environment variables of stack
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

<<<<<<< HEAD
`GET /stacks/{stack_id}/notifications/`
=======
`GET /stacks/{id}/notifications`
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
alert_type | optional | string | Type of alert | `server.stopped`

<<<<<<< HEAD
## notifications info

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
notification_name = `noticent_stack_update_failed`
response = token.get("#{api_url}/stacks/#{stack_id}/notifications/#{notification_name}.json")
=======
## Notification

```ruby
stack_id = 'a6b583684833a2cf4845079c9d9350a8'
id = 1191
response = token.get("#{api_url}/stacks/#{stack_id}/notifications/#{id}.json")
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

puts JSON.parse(response.body)['response']
```

```http
<<<<<<< HEAD
GET /stacks/5999b763474b0eafa5fafb64bff0ba80/notifications/noticent_stack_provisioned_success HTTP/1.1
=======
GET /stacks/{stack_id}/notifications/{id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
<<<<<<< HEAD
    "response": {
        "notification_name": "noticent_stack_provisioned_success",
        "subscriptions": [
            {
                "channel": "email"
            }
        ]
=======
  "response":
    {
      "id":1191,
      "user_id":18,
      "alert_type":
      "stack.redeploy.ok",
      "channels":["email"],
      "stack_id":"5acd43412ea412e32897c40d46f91183",
      "params":{},
      "created_at":"2014-05-29T17:29:54Z",
      "updated_at":"2014-05-29T17:29:54Z"
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)
    }
}
```

Get information of a single notification

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

<<<<<<< HEAD
`GET /stacks/{stack_id}/notifications/{notification_name}/`
=======
`GET /stacks/{stack_id}/notifications/{id}`
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
<<<<<<< HEAD
stack_id | **required** | string | The application's UID | `5999b763474b0eafa5fafb64bff0ba80`
notification_name | **required** | string | The name of the notification to query | `noticent_stack_update_failed`

## notifications update
=======
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
id | **required** | integer | The notification ID | `1191`

## Update Notification
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

```ruby
stack_id = 'a6b583684833a2cf4845079c9d9350a8'
id = 1191

<<<<<<< HEAD
response = token.patch("#{api_url}/stacks/#{stack_id}/notifications.json", {body:{"notifications":[{"notification_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}})
=======
channels = ['email','hipchat']
params = {:hipchat_room => 'test', :hipchat_token => 'YOUR_TOKEN'}
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

response = token.put("#{api_url}/stacks/#{stack_id}/notifications/#{id}.json", {body: {:channels => channels, :params => params}})

puts JSON.parse(response.body)['response']
```

```http
<<<<<<< HEAD
PATCH /stacks/{stack_id}/notifications/ HTTP/1.1
=======
PUT /stacks/{stack_id}/notifications/{id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
<<<<<<< HEAD
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
=======
  "response":
  {
    "id":85,
    "user_id":1,
    "alert_type":"active.protect.block",
    "channels":["email","hipchat"],
    "stack_id":"3ee97c150d95a9dc4fc801783d18087c",
    "params":{},
    "created_at":"2015-11-16T18:14:04Z",
    "updated_at":"2015-12-09T13:06:14Z"
  }
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)
}

```

<<<<<<< HEAD
Update the notifications for an application. You can use the JSON response from one application to effectively copy those settings to another application. 
=======
Update `channels` or `params` of a notification
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

<<<<<<< HEAD
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
=======
`PUT /stacks/{stack_id}/notifications/{id}`
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
<<<<<<< HEAD
application_group_name | **required** | string | Name of the application group | `production-apps`
notifications | **required** | json | A JSON formatted description of notification settings | {"notifications":[{"notification_name":"noticent_stack_health_check_failed","subscriptions":[{"channel":"email"}]}]}
=======
stack_id | **required** | string | The stack UID | `5999b763474b0eafa5fafb64bff0ba80`
id | **required** | integer | The notification ID | `1191`
channels | optional | string | Notification channels (valid channels are: `email`, `ios`, `hipchat`, `webhook`, `slack`) | `[email,ios]`
params | optional | string | Notification channel parameters (as JSON string with valid keys: `hipchat_token`, `hipchat_room`, `slack_url`, `slack_channel`, `webhook_url`) | `{'hipchat_room' : 'test'}`
>>>>>>> parent of 316daa4 (Alerts & Failover Groups)
