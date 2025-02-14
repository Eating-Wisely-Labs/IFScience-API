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
                "account_id": 80,
                "record_id": 245,
                "plan_id": 21,
                "comment_uid": "1889882969084666073",
                "checkin_time": "2025-02-13T11:42:00.000Z",
                "post": {
                    "comment_uid": "1889882969084666073",
                    "image": "https://image.ifsci.wtf/tw/img/Gjo2ii6aIAQHfsY.jpg",
                    "text": "Beef noodles stir-fried. Two servings, roughly 400g each. Estimated per serving: 600 kcal, 25g fat, 80g carbs, 30g protein. Total: 1200 kcal, 50g fat, 160g carbs, 60g protein.",
                    "food_items": [
                        {
                            "name": "calories",
                            "value": "1200",
                            "unit": " kcal"
                        },
                        {
                            "name": "fat",
                            "value": "50",
                            "unit": " g"
                        },
                        {
                            "name": "carbs",
                            "value": "160",
                            "unit": " g"
                        },
                        {
                            "name": "protein",
                            "value": "60",
                            "unit": " g"
                        }
                    ],
                    "create_time": "2025-02-13T11:43:06.000Z"
                }
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

