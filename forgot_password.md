1. A signed-in user clicks on the forgot password link. He is prompted with a text box to enter his registered email address.
Upon entering his registered email he clicks on the forgot password button. An email message with password reset link is sent to
his registered email address.

```
 request = self.factory.put(
    reverse("forgot_password"),
    HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```

```
self.assertEqual(response.status_code, status.HTTP_200_OK)
self.assertEqual(
    response.data,
    {
        "success": True,
        "message": "An email with the password reset link has been sent to your registered email",
        "data": [],
    },
)
```

User clicks on his forgot password hyperlink  - '/api/accounts/forgot_password?token=mnks3K903cBccE_roofibAOzwLlOjfGCxkE-7MBq4m4'
the querystring `token` is validated against users' reset password token, 

```
url = '/api/accounts/forgot_password?token=mnks3K903cBccE_roofibAOzwLlOjfGCxkE-7MBq4m4'
request = self.factory.get(url)
```

The received response contains `Location` header where the client should redirect to, It is generally a `reset-password` link.

```
self.assertIn("Location", response)
self.assertEqual(response.status_code, status.HTTP_307_TEMPORARY_REDIRECT)
```

2. Anonymous user enters a random email to reset password,

If the email is registered with the system, he will receive an email with password reset hyperlink.
If the email is not registered with the system, he dont receive any email.In both cases the response
code is 200.

```
request = factory.put(
    reverse("forgot_password"),
    {"email": "john@gmail.com"},
)

message = {
    "success": True,
    "message": "An email with the password reset link has been sent to your registered email",
    "data": [],
}
self.assertEqual(response.status_code, status.HTTP_200_OK)
```
