# Authentication

## Introduction
Project LOGGED uses the `token` key to authenticate request.
The `token` is a string consists of letters and numbers up to 128 characters in length.
All token have an expire date. This information can be accessed when the token is acquired.
To change how long the token expires, please take a look at the configuration file.

## Token
The client is expected to store the token and get a new one once the token has expired.
Error with the message `Token is invalid or expired.` will be returned if token is no longer accepted.

## Validation Rules
| Name         | Rule(s)                          |
| ------------ | -------------------------------- |
| email        | required\|email\|max:128         |
| password     | required\|string\|min:8\|max:128 |
| new_password | required\|string\|min:8\|max:128 |
| token        | required\|string\|min:8\|max:128 |
| code         | required\|string\|min:8\|max:64  |
| name         | required\|alpha_spaces\|max:32   | 

## Available Methods
| Name               | Method | Route                  | Description               | Parameter(s)                  |
| ------------------ | ------ | ---------------------- | ------------------------- | ----------------------------- |
| register           | POST   | /auth/register         | Register new account      | email, password, name         |
| verify             | POST   | /auth/verify           | Verify email address      | email, code                   |
| resendVerification | POST   | /auth/verify/resend    | Resend verification email | email                         |
| login              | POST   | /auth/login            | Get login token           | email, password               |
| change             | POST   | /auth/password/change  | Change password           | email, password, new_password |
| requestReset       | POST   | /auth/password/request | Request password reset    | email                         |
| reset              | POST   | /auth/password/reset   | Reset password            | email, token, password        | 

## Methods

### Register
Response sample:
```
{
 	"status": "success",
 	"message": "Account successfully created."
}
```

### Login
Response sample:
```
{
	"status": "success",
	"message": "Token acquired.",
	"data": {
		"token": "904b7379307849cbf84a9b77db9226e5691d4d30c9e4e103406803bebdf83ccb",
		"expires": 1983456789
	}
}
```

### The rest of the methods
All return `status` that can be `success` or `error` along with `message` that can be shown to user.