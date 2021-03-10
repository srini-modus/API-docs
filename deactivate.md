Only an admin can deactivate a user. 

1. An admin user deactivating an existing user

```
factory.put(
    "api/accounts/deactivate/",
    {"email": "test@gmail.com"},
    HTTP_AUTHORIZATION=f"Bearer {access_token}",
)

{
    "success": True,
    "message": "Profile with email :'test@gmail.com' has successfully been deactivated.",
    "data": [],
}
```

2. An admin user deactivating a non-existing user

```
factory.put(
    "api/accounts/deactivate/",
    {"email": "test@gmail.com"},
    HTTP_AUTHORIZATION=f"Bearer {access_token}",
)

{
    "success": False,
    "error-code": None,
    "errors": {
        "email": [f"No such user with the email address: '{email}' exists"]
    },
    "message": "Validation errors have occurred",
}
```

3. Any user trying to deactivate with invalid token/credentials,

```
factory.put(
    "/api/accounts/deactivate/",
    {"email": "test@gmail.com"},
    HTTP_AUTHORIZATION=f"Bearer {invalid_access_token}",
)

message = {
    'detail': ErrorDetail(string='Given token not valid for any token type', code='token_not_valid'),
    'code': ErrorDetail(string='token_not_valid', code='token_not_valid'),
    'messages': [
        {
            'token_class': ErrorDetail(string='AccessToken', code='token_not_valid'),
            'token_type': ErrorDetail(string='access', code='token_not_valid'),
            'message': ErrorDetail(string='Token is invalid or expired', code='token_not_valid')
        }
    ]
}
self.assertEqual(response.status_code, status.HTTP_401_UNAUTHORIZED)
```
