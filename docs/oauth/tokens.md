# Access Token Management

## Token Types

### Access Token
- Used to authenticate API requests
- Short-lived (1 hour validity)
- Must be included in Authorization header

### Refresh Token
- Used to obtain new access tokens
- Long-lived (30 days validity)
- Should be stored securely

## Obtaining Tokens

### Initial Token Request

Exchange authorization code for tokens:

```http
POST https://ifsci.wtf/oauth/token
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "YOUR_CLIENT_ID",
    "client_secret": "YOUR_CLIENT_SECRET",
    "code": "AUTHORIZATION_CODE",
    "redirect_uri": "YOUR_REDIRECT_URI"
}
```

**Response:**
```json
{
    "access_token": "ACCESS_TOKEN",
    "refresh_token": "REFRESH_TOKEN",
    "expires_in": 3600,
    "token_type": "Bearer"
}
```

### Refreshing Tokens

When an access token expires, use the refresh token to obtain a new one:

```http
POST https://ifsci.wtf/oauth/token
Content-Type: application/json

{
    "grant_type": "refresh_token",
    "client_id": "YOUR_CLIENT_ID",
    "client_secret": "YOUR_CLIENT_SECRET",
    "refresh_token": "REFRESH_TOKEN"
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

## Token Storage

### Security Guidelines

1. Store tokens securely
   - Use encrypted storage
   - Never store in client-side code
   - Never expose in URLs

2. Implement proper token rotation
   - Track token expiration
   - Refresh before expiration
   - Handle refresh failures

3. Handle token revocation
   - Remove stored tokens when user revokes access
   - Implement logout functionality

## Error Handling

### Common Token Errors

1. Invalid Token
```json
{
    "error": "invalid_token",
    "error_description": "The access token has expired"
}
```

2. Invalid Refresh Token
```json
{
    "error": "invalid_grant",
    "error_description": "The refresh token is invalid or has expired"
}
```

3. Invalid Client
```json
{
    "error": "invalid_client",
    "error_description": "Client authentication failed"
}
```

### Error Recovery

1. Access Token Expired
   - Attempt to refresh the token
   - If successful, retry the original request
   - If unsuccessful, redirect to authorization

2. Refresh Token Expired
   - Clear stored tokens
   - Redirect user to authorization flow
   - Obtain new tokens

3. Invalid Client Credentials
   - Verify client ID and secret
   - Check API credentials in developer dashboard
   - Contact support if issues persist
