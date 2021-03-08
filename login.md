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

{"refresh":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTYxNTI1Mjg3NywianRpIjoiNGQzODE0ZGNiMTZkNDA2ZGI5YjgzOTg0ZDIyZWQ4YjciLCJ1c2VyX2lkIjoxOH0.rhVECzKZcN98HF7KkF8Vn9A1TzLJYRrC3H7-mKDdP-Q","access":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjE1MTY2Nzc3LCJqdGkiOiI4NGFhNTRiYWNkMTA0NDYwODBjNTA2NjFjZDYyMzEwOCIsInVzZXJfaWQiOjE4fQ.G-vAAcqWuxloMJ7ba8CstTSueWyawRf6Dx3CGinghCU"}
```