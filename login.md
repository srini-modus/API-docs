1. You can log in to the system with the username and password

```
request = factory.post(
    "api/accounts/login/",
    {
        "email": "john@gmail.com",
        "password": "12345",
    },
)

self.assertEqual(response.status_code, status.HTTP_200_OK)
self.assertIn("refresh", response.data)
self.assertIn("access", response.data)
```

```
{"refresh":"...............",
"access":".................."}
```
Lipak, please store `refresh` and `access` tokens in browsers' localstorage.

All the subsequent requests after login should include the `access` token in the `Authorization` header.
e.g: 

```
requests.post(
    ................
    headers={
        "Authorization": "Bearer {access_token}".format(access_token=access)
    }
)
```