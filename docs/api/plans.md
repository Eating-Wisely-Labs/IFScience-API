# Check-in Plans API

## List Plans

Retrieve all intermittent fasting plans for a user.

```http
GET /api/v1/plans
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "status": "success",
    "data": {
        "plans": [
            {
                "plan_id": "plan123",
                "name": "16/8 Fasting",
                "fasting_hours": 16,
                "eating_hours": 8,
                "start_time": "08:00",
                "active": true,
                "created_at": "2025-01-20T00:00:00Z"
            }
        ]
    }
}
```

## Get Plan Details

Retrieve details of a specific plan.

```http
GET /api/v1/plans/{plan_id}
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "status": "success",
    "data": {
        "plan_id": "plan123",
        "name": "16/8 Fasting",
        "fasting_hours": 16,
        "eating_hours": 8,
        "start_time": "08:00",
        "active": true,
        "created_at": "2025-01-20T00:00:00Z",
        "stats": {
            "completion_rate": 92,
            "total_days": 30,
            "successful_days": 28
        }
    }
}
```

## Create Plan

Create a new intermittent fasting plan.

```http
POST /api/v1/plans
Authorization: Bearer ACCESS_TOKEN
Content-Type: application/json

{
    "name": "16/8 Fasting",
    "fasting_hours": 16,
    "eating_hours": 8,
    "start_time": "08:00"
}
```

**Response:**
```json
{
    "status": "success",
    "data": {
        "plan_id": "plan123",
        "name": "16/8 Fasting",
        "created_at": "2025-01-25T20:44:00Z"
    },
    "message": "Plan created successfully"
}
```

## Update Plan

Update an existing plan's details.

```http
PUT /api/v1/plans/{plan_id}
Authorization: Bearer ACCESS_TOKEN
Content-Type: application/json

{
    "name": "Modified 16/8 Fasting",
    "start_time": "09:00",
    "active": false
}
```

**Response:**
```json
{
    "status": "success",
    "message": "Plan updated successfully"
}
```

## Delete Plan

Delete an existing fasting plan.

```http
DELETE /api/v1/plans/{plan_id}
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "status": "success",
    "message": "Plan deleted successfully"
}
```

## Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| plan_id | string | Unique plan identifier |
| name | string | Plan name |
| fasting_hours | integer | Duration of fasting window |
| eating_hours | integer | Duration of eating window |
| start_time | string | Daily start time (HH:MM) |
| active | boolean | Whether plan is currently active |

## Error Responses

### Plan Not Found
```json
{
    "status": "error",
    "code": "plan_not_found",
    "message": "The specified plan does not exist"
}
```

### Invalid Plan Parameters
```json
{
    "status": "error",
    "code": "invalid_parameters",
    "message": "Invalid fasting/eating hours combination"
}
```
