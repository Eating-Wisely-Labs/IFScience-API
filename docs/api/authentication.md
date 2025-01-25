# API Authentication

All API requests to IF Science platform must be authenticated using OAuth 2.0 access tokens.

## Access Token Usage

Include the access token in the `Authorization` header of all API requests:

```http
GET /api/v1/user
Authorization: Bearer YOUR_ACCESS_TOKEN
```

## Token Lifecycle

### Token Expiration

Access tokens are valid for 1 hour (3600 seconds) after issuance. The expiration time is included in the token response as `expires_in`.

### Token Refresh

When an access token expires, use the refresh token to obtain a new one:

```http
POST https://ifsci.wtf/oauth/token
Content-Type: application/json

{
  "grant_type": "refresh_token",
  "client_id": "YOUR_CLIENT_ID",
  "client_secret": "YOUR_CLIENT_SECRET",
  "refresh_token": "YOUR_REFRESH_TOKEN"
}
```

**Response:**
```json
{
  "access_token": "NEW_ACCESS_TOKEN",
  "refresh_token": "NEW_REFRESH_TOKEN",
  "expires_in": 3600
}
```

## Error Responses

### Invalid Token

```json
{
  "error": "invalid_token",
  "error_description": "The access token has expired"
}
```

### Invalid Refresh Token

```json
{
  "error": "invalid_grant",
  "error_description": "The refresh token is invalid or has expired"
}
```

## Best Practices

1. Store tokens securely
2. Refresh tokens before they expire
3. Handle token errors gracefully
4. Implement proper token rotation
5. Never expose tokens in client-side code or URLs
