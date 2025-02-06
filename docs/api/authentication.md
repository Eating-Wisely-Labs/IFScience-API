# API Authentication

All API requests to IF Science platform must be authenticated using OAuth 2.0 access tokens.

## Access Token Usage

Include the access token in the `Authorization` header of all API requests:

```http
GET /api/oauth/user
Authorization: Bearer YOUR_ACCESS_TOKEN
```

## Token Lifecycle

### Token Expiration

Access tokens are valid for 1 hour (3600 seconds) after issuance. The expiration time is included in the token response as `expires_in`.

### Token Refresh

When an access token expires, use the refresh token to obtain a new one:

```http
POST https://ifsci.wtf/api/oauth/token
Content-Type: application/json

{
  "client_id": "YOUR_CLIENT_ID",
  "client_secret": "YOUR_CLIENT_SECRET",
  "grant_type": "authorization_code",
  "code": "AUTH_CODE",
  "redirect_uri": "https://your-app.com/oauth/callback"
}
```

**Response:**
```json
{
  "access_token": "NEW_ACCESS_TOKEN",
  "refresh_token": "NEW_REFRESH_TOKEN",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

## Error Responses

### Invalid Authorization Code

```json
{
  "code": "401",
  "data": null,
  "message": "Invalid code"
}
```

### Invalid Client Id

```json
{
  "code": "401",
  "data": null,
  "message": "Invalid client_id"
}
```

### Invalid Client Secret

```json
{
  "code": "401",
  "data": null,
  "message": "Invalid client_secret"
}
```

## Best Practices

1. Store tokens securely
2. Refresh tokens before they expire
3. Handle token errors gracefully
4. Implement proper token rotation
5. Never expose tokens in client-side code or URLs
