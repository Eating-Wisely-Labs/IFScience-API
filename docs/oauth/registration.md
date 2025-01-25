# Developer Registration

Before you can integrate with IF Science API, you need to register as a developer and obtain your API credentials.

## Registration Process

### 1. Register as a Developer

Visit the IF Science developer registration page:
```
https://ifsci.wtf/developer/register
```

You will need to provide the following information:

- Application Name (e.g., "Stadium Science")
- Application Description
- Application Website URL
- OAuth Callback URL
- Contact Email

### 2. Application Review

After submitting your registration:
1. The IF Science team will review your application
2. Upon approval, you will receive your `client_id` and `client_secret`
3. Store these credentials securely - they will be required for API authentication

### 3. Developer Dashboard

Once approved, you can manage your application through the developer dashboard:
```
https://ifsci.wtf/developer/dashboard
```

The dashboard allows you to:
- View your application details
- Update your application settings
- Monitor API usage
- Generate new client secrets if needed

## Security Guidelines

1. Never expose your `client_secret` in client-side code
2. Use secure HTTPS endpoints for your callback URLs
3. Implement proper token storage and management
4. Follow OAuth 2.0 best practices for security

## Next Steps

After receiving your credentials:
1. Review the [OAuth Flow](flow.md) documentation
2. Implement the OAuth authorization process
3. Start making API requests with the obtained access tokens

## Support

If you need assistance with the registration process or have questions about your application, contact our developer support team at support@ifsci.wtf.
