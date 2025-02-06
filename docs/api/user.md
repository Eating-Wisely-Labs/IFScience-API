# User API

## Get User Profile

Retrieve the user's profile information.

```http
GET /api/oauth/user
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "code": 0,
    "data": {
        "account_id": "xyz",
    },
    "message": "success"
}
```

## Error Responses

### Invalid Token
```json
{
    "code": 401,
    "data": null,
    "message": "Invalid Token"
}
```
