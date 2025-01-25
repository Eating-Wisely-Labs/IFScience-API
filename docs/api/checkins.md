# Check-in Data API

## Submit Check-in

Record a new check-in for a fasting plan.

```http
POST /api/v1/checkins
Authorization: Bearer ACCESS_TOKEN
Content-Type: application/json

{
    "plan_id": "plan123",
    "check_in_time": "2025-01-25T20:00:00Z",
    "status": "success",
    "notes": "Completed 16 hour fast"
}
```

**Response:**
```json
{
    "status": "success",
    "data": {
        "checkin_id": "check123",
        "points_earned": 10,
        "streak": 5
    },
    "message": "Check-in recorded successfully"
}
```

## Get Check-in History

Retrieve check-in history for a plan.

```http
GET /api/v1/checkins?plan_id=plan123&start_date=2025-01-01&end_date=2025-01-31
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "status": "success",
    "data": {
        "checkins": [
            {
                "checkin_id": "check123",
                "plan_id": "plan123",
                "check_in_time": "2025-01-25T20:00:00Z",
                "status": "success",
                "points_earned": 10,
                "notes": "Completed 16 hour fast"
            }
        ],
        "total_count": 25,
        "success_rate": 92
    }
}
```

## Get Check-in Details

Retrieve details of a specific check-in.

```http
GET /api/v1/checkins/{checkin_id}
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "status": "success",
    "data": {
        "checkin_id": "check123",
        "plan_id": "plan123",
        "check_in_time": "2025-01-25T20:00:00Z",
        "status": "success",
        "points_earned": 10,
        "notes": "Completed 16 hour fast",
        "streak_at_time": 5
    }
}
```

## Update Check-in

Update an existing check-in record.

```http
PUT /api/v1/checkins/{checkin_id}
Authorization: Bearer ACCESS_TOKEN
Content-Type: application/json

{
    "notes": "Updated: Completed 16 hour fast successfully",
    "status": "success"
}
```

**Response:**
```json
{
    "status": "success",
    "message": "Check-in updated successfully"
}
```

## Delete Check-in

Delete a check-in record.

```http
DELETE /api/v1/checkins/{checkin_id}
Authorization: Bearer ACCESS_TOKEN
```

**Response:**
```json
{
    "status": "success",
    "message": "Check-in deleted successfully"
}
```

## Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| checkin_id | string | Unique check-in identifier |
| plan_id | string | Associated plan identifier |
| check_in_time | ISO date | Time of check-in |
| status | string | Status of the fast (success/failed) |
| points_earned | integer | Points earned for the check-in |
| notes | string | Optional notes about the check-in |
| streak_at_time | integer | Streak count at time of check-in |

## Error Responses

### Invalid Check-in Time
```json
{
    "status": "error",
    "code": "invalid_checkin_time",
    "message": "Check-in time must be within the plan's fasting window"
}
```

### Duplicate Check-in
```json
{
    "status": "error",
    "code": "duplicate_checkin",
    "message": "A check-in already exists for this time period"
}
```
