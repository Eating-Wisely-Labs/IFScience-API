# OAuth Flow

This document describes the OAuth 2.0 authorization flow for integrating with IF Science platform.

## Authorization Flow Steps

### 1. User Initiates Sync

When a user clicks the "Sync IFS" button on your platform, redirect them to the IF Science authorization page:

```
GET https://ifsci.wtf/oauth/authorize
```

**Required Parameters:**

| Parameter | Description |
|-----------|-------------|
| response_type | Must be `code` |
| client_id | Your application's Client ID |
| redirect_uri | Your application's callback URL |
| scope | Space-separated list of permissions (e.g., `basic_data checkin_plans checkin_data`) |
| state | A random string to prevent CSRF attacks |

**Example Request:**
```
https://ifsci.wtf/oauth/authorize?
  response_type=code
  &client_id=YOUR_CLIENT_ID
  &redirect_uri=https://your-app.com/oauth/callback
  &scope=basic_data,checkin_plans,checkin_data
  &state=random_state_string
```

### 2. User Authorization

The user will be prompted to log in to IF Science (if not already logged in) and authorize your application. After authorization, they will be redirected back to your `redirect_uri` with an authorization code.

**Example Callback:**
```
https://your-app.com/oauth/callback?code=AUTH_CODE&state=random_state_string
```

### 3. Exchange Authorization Code

Exchange the authorization code for an access token:

```http
POST https://ifsci.wtf/oauth/token
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
  "access_token": "ACCESS_TOKEN",
  "refresh_token": "REFRESH_TOKEN",
  "expires_in": 3600
}
```

### 4. Use Access Token

Include the access token in the Authorization header when making API requests:

```http
GET https://ifsci.wtf/api/v1/user
Authorization: Bearer ACCESS_TOKEN
```

## Scopes

| Scope | Description |
|-------|-------------|
| basic_data | Access to user's basic information |
| checkin_plans | Access to user's intermittent fasting plans |
| checkin_data | Access to user's check-in data |

## Error Handling

If an error occurs during the OAuth flow, the authorization server will redirect the user back to your `redirect_uri` with error parameters:

```
https://your-app.com/oauth/callback?error=access_denied&error_description=The+user+denied+access
```
