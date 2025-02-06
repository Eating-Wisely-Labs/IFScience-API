# Check-in Data API

⚠️Warning: APIs in this section are in beta and may be modified without prior notice

## Get Check-in History

Retrieve check-in history for a plan.

```http
GET /api/v1/app/checkin/records?plan_id=123&start_date=2025-01-01&end_date=2025-01-31&page_no=1&page_size=10
Authorization: Bearer ACCESS_TOKEN
```

| Parameter | Description |
|-----------|-------------|
| plan_id | Optional |
| start_date | Optional, time range start, UTC Date |
| end_date | Optional, time range end, UTC Date |
| page_no | Optional, page number, default to 1 |
| page_size | Optional, page size, default to 10 |

**Response:**
```json
{
    "code": 0,
    "data": {
        "list": [
            {
                "record_id": 456,
                "plan_id": 123,
                "checkin_time": "2025-01-01T10:00:00Z",
            }
        ],
        "total": 25,
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

