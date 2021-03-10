1. A user has already been registered, now he has to be approved by an administrator to use the system.
An admin can log in to the system with his credentials and can approve the user.
Ignoring the approval process is very much like disapproving.

If the user sends repeated registering requests, then  maybe we can block that user permanently.


```
factory.put(
    "/api/accounts/approve/",
    {"email": "test@gmail.com"},
    HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
message = {
    "success": True,
    "message": "User with the email address: 'test@gmail.com' has been approved.",
    "data": [],
},
self.assertEqual(response.status_code, status.HTTP_200_OK)
```
Note: `PUT` method is idempotent here.

2. An user trying to approve with invalid token/ credentials,


```
factory.put(
    "/api/accounts/approve/",
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