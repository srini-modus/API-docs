1. A logged-in user clicks on the reset password link. He will be redirected to the reset password page.
The user enters the current password, new-password, confirms new-password.

```
request = self.factory.put(
    '/api/accounts/reset_password',
    {
        "password": "12345",
        "new_password": "srini",
        "confirm_new_password": "srini",
    },
    HTTP_AUTHORIZATION=f"Bearer {tokens['access']}",
    format="json",
)
self.assertEqual(
    response.data,
    {"success": True, "message": "Password updated successfully", "data": []},
)
```
2. If new password and confirm new password do not match,
```
request = self.factory.put(
    '/api/accounts/reset_password',
    {
        "password": "12345",
        "new_password": "srini",
        "confirm_new_password": "srini_vas",  # passwords do not match
    },
    HTTP_AUTHORIZATION=f"Bearer {access_token}",
    format="json",
)
self.assertEqual(
    response.data,
    {
        "success": False,
        "error-code": None,
        "errors": {
            "password": [
                "'new_password' and 'confirm_new_password' do not match"
            ]
        },
        "message": "Validation errors have occurred",
    },
)

```
3. If the user with the wrong password,
```
request = self.factory.put(
    '/api/accounts/reset_password',
    {
        "password": "123456",
        "new_password": "srini",
        "confirm_new_password": "srini",
    },
    HTTP_AUTHORIZATION=f"Bearer {tokens['access']}",
    format="json",
)
self.assertEqual(
    response.data,
    {
        "success": False,
        "error-code": None,
        "errors": {"password": ["Wrong password"]},
        "message": "Validation errors have occurred",
    },
)
self.assertEqual(response.status_code, status.HTTP_400_BAD_REQUEST)
```