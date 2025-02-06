# Check-in Plans API

⚠️Warning: APIs in this section are in beta and may be modified without prior notice

## List Plans

Retrieve all intermittent fasting plans for a user.

```http
GET /api/v1/app/checkin/plan?page_no=1&page_size=10
Authorization: Bearer ACCESS_TOKEN
```

| Parameter | Description |
|-----------|-------------|
| page_no | Optional, Page number, default to 1 |
| page_size | Optional, Page size, default to 10 |

**Response:**
```json
{
    "code": 0,
    "data": {
        "list": [
            { 
                "id": 123,
                "checkin_type": "sixteen_and_eight",
                "start_time": "10:00",
                "end_time": "16:00"
            }
        ],
        "total": 1,
        "page_no": 1,
        "page_size": 10
    },
    "message": "success"
}
```

## Error Responses

### Invalid Access Token
```json
{
    "code": 401,
    "data": null,
    "message": "Invalid token"
}
```
