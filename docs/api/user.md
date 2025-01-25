# User API

## Get User Profile

Retrieve the user's profile information.

```http
GET /api/v1/user
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "status": "success",
    "data": {
        "user_id": "xyz",
        "if_bool": true,
        "if_start": "2025-01-25T08:00:00Z",
        "if_end": "2025-01-26T00:00:00Z",
        "calories": 2000
    }
}
```

## Update User Settings

Update user's intermittent fasting settings.

```http
PUT /api/v1/user/settings
Authorization: Bearer ACCESS_TOKEN
Content-Type: application/json

{
    "if_bool": true,
    "if_start": "2025-01-25T08:00:00Z",
    "if_end": "2025-01-26T00:00:00Z",
    "calories": 2000
}
```

**Response:**
```json
{
    "status": "success",
    "message": "User settings updated successfully"
}
```

## Get User Statistics

Retrieve user's fasting statistics and achievements.

```http
GET /api/v1/user/stats
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "status": "success",
    "data": {
        "total_fasts": 30,
        "successful_fasts": 28,
        "current_streak": 5,
        "longest_streak": 15,
        "total_points": 280
    }
}
```

## Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| if_bool | boolean | Whether intermittent fasting is active |
| if_start | ISO date | Start time of fasting window |
| if_end | ISO date | End time of fasting window |
| calories | integer | Optional daily calorie target |
| user_id | string | Unique user identifier |

## Error Responses

### Invalid Token
```json
{
    "status": "error",
    "code": "invalid_token",
    "message": "The access token is invalid or has expired"
}
```

### Invalid Request
```json
{
    "status": "error",
    "code": "invalid_request",
    "message": "Invalid time format for if_start or if_end"
}
```
