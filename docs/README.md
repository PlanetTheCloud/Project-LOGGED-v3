# Documentation for Project LOGGED v3
## Response
All response from the server are in JSON and always have `status` key. Which can be `success` or `error`.
Any `error` will always be followed by `message` key. `success` may or may not have the `message` key and or the `data` key.

**NOTE:** The `message` can either be a string or an array. If an array, that means it is a validation error which looks like this:
```
{
 "status": "error",
 "message": {
 	"email": "The Email is required"
 }
}
```

**NOTE:** When in `debug_mode`, any errors or warnings that occur will be placed under the `error` key.
The `error` key contains the `message`, `file`, `line`, and `trace` keys. All which are derived from Exceptions.

## Rate Limit
Some endpoints may be restricted by means of rate limiting. Example of rate limited request:
```
{
 	"message": "Too many attempts.",
 	"available_in": 33,
 	"status": "error"
}
```
`available_in` indicates how many seconds before the request can be accepted.

## Authentication
Some endpoints may only be accessed with authentication token. 
See [Authentication] to learn more about authentication.