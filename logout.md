1. A signed in user can logout from the system.

```
request = self.factory.post(
    '/api/accounts/logout',
    data={"refresh": tokens["refresh"]},
    HTTP_AUTHORIZATION=f"Bearer {tokens['access']}",
    format="json",
)
```

```
self.assertEqual(response.status_code, status.HTTP_204_NO_CONTENT)
self.assertEqual(response.content_type, "application/json")
```

2. A signed-in user with invalid credentials or a non-registered user cannot logout from the system.

```
request = self.factory.post(
    '/api/accounts/logout',
    data={"refresh": tokens["refresh"]},
    HTTP_AUTHORIZATION=f"Bearer {tokens['access']}dummy",
    format="json",
)
```

```
self.assertEqual(response.status_code, status.HTTP_401_UNAUTHORIZED)
self.assertEqual(response.content_type, None)
```