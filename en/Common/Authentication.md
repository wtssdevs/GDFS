
# Credential Authentication & Authorization

Authenticate the user account and obtain the bearer authentication token from the response.
Note - Token expires in 86400 Seconds

**URL** : `/api/TokenAuth/Authenticate`

**Method** : `POST`

**Headers**

| Key | Value |
|--------------|--------------|
| Content-Type | application/json  |
| Accept | application/json |


**Data constraints**

| Type| Params| Values| Validation |
|--------------|---------- |-------------- |------------ |
|AuthenticateModel|UsernameOrEmailAddress|string [256]|**Required**|
|AuthenticateModel|Password|string [32]|**Required**|
|AuthenticateModel|RememberClient|bool|**Required**|


**Body Raw (application/json)**

**Content Example**

```json

{
    "userNameOrEmailAddress": "UserName",
    "password": "password123",
    "rememberClient": true
}

```

## Response *Success* 
**Success** : `true`

**Content Example**

```json

{
    "result": {
        "accessToken": "yJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi...",
        "encryptedAccessToken": "wNYmO41/48SHNstaLVXxHCCre29BZQl1NhC6NM3==...",
        "expireInSeconds": 86400,
        "userId": 2
    },
    "targetUrl": null,
    "success": true,
    "error": null,
    "unAuthorizedRequest": false,
    "__abp": true
}

```


## Response *Failed*
**Result** : `false`

**Content Example**

```json

{
    "result": null,
    "targetUrl": null,
    "success": false,
    "error": {
        "code": 400,
        "message": "Login failed!",
        "details": "Invalid user name or password",
        "validationErrors": null
    },
    "unAuthorizedRequest": false,
    "__abp": true
}

```

