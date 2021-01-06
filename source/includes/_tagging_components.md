# Tagging Components

## List tags

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
server_id = 'f8468fc145ea49bac474b30a8fea888d'
response = token.get("#{api_url}/tags/{entity_type}/{entity_id}/tags.json")
puts JSON.parse(response.body)['response']
```

```http
GET /tags/{entity_type}/{entity_id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":[
    {
	"entity_type":"loadbalancer",                    
	"entity_id":"17823",                      
	"tags": ["foo","bar"],
	"created_at_iso":"2021-01-04T21:32:33+0000"
	"updated_at_iso":"2021-01-05T11:12:23+0000"}
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

Get a list of tags for entities (servers & loadbalancers) by entity type and entity ID.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`GET /tags/{entity_type}/{entity_id}`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
entity_type | optional | string | Type of the entity | `server`
server_id | optional | string | ID of the entity | `57648`

## Add tags

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
server_id = 'f8468fc145ea49bac474b30a8fea888d'
response = token.post("#{api_url}/tags/{entity_type}/{entity_id}/tags.json")
puts JSON.parse(response.body)['response']
```

```http
POST /tags/{entity_type}/{entity_id} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":[
    {
	"entity_type":"loadbalancer",                    
	"entity_id":"17823",                      
	"tags": ["foo","bar"],
	"created_at_iso":"2021-01-04T21:32:33+0000"
	"updated_at_iso":"2021-01-05T11:12:23+0000"}
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

Add tags to an entity (server or loadbalancer). Completely **replaces** tags of the object with tags provided.

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`POST /tags/{entity_type}/{entity_id}`

### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
entity_type | **required** | string | Type of the entity | `server`
entity_id | **required** | string | ID of the entity | `57648`

## Update (patch) tags

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
server_id = 'f8468fc145ea49bac474b30a8fea888d'
response = token.patch("#{api_url}/tags/{entity_type}/{entity_id}/{operations}/tags.json")
puts JSON.parse(response.body)['response']
```

```http
PATCH /tags/{entity_type}/{entity_id}/{operations} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":[
    {
	"entity_type":"loadbalancer",                    
	"entity_id":"17823",                      
	"tags": ["foo","bar"],
	"created_at_iso":"2021-01-04T21:32:33+0000"
	"updated_at_iso":"2021-01-05T11:12:23+0000"}
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

Update tags on an entity (server or loadbalancer). **Adds** or **deletes** tags based on the `operations` parameter. Deleting non-existent tags is not an error, will simply be ignored. Performs deletions first, then additions. 

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`PATCH /tags/{entity_type}/{entity_id}/{operations}`

### Operation API objects

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
op | **required** | string | "add" or "delete" - specifies what to do with the below tag values | `add`
tags | **required** | array | Array of tag values for above operation | `["foo","bar"]`


### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
entity_type | **required** | string | Type of the entity | `server`
entity_id | **required** | string | ID of the entity | `57648`
operations | **required** | array | An array of `Operation API objects` | `[add,["foo","bar"]]`

## Delete tags

```ruby
stack_id = '5999b763474b0eafa5fafb64bff0ba80'
server_id = 'f8468fc145ea49bac474b30a8fea888d'
response = token.delete("#{api_url}/tags/{entity_type}/{entity_id}/tags.json")
puts JSON.parse(response.body)['response']
```

```http
DELETE /tags/{entity_type}/{entity_id}/{operations} HTTP/1.1
X-RateLimit-Limit: 3600
X-RateLimit-Remaining: 3597
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "response":[
    {
	"entity_type":"loadbalancer",                    
	"entity_id":"17823",                      
	"tags": ["foo","bar"],
	"created_at_iso":"2021-01-04T21:32:33+0000"
	"updated_at_iso":"2021-01-05T11:12:23+0000"}
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

Delete all tags on an entity (server or loadbalancer).

<aside class="notice">
<b>Scope:</b> <i>public</i>
</aside>

### HTTP Request

`DELETE /tags/{entity_type}/{entity_id}`


### Query parameters

Parameter | Presence | Data type | Description |  Sample value
--------- | ------- | ------- |----------- |  -------
entity_type | **required** | string | Type of the entity | `server`
entity_id | **required** | string | ID of the entity | `57648`