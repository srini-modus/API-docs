1. Trying to register a new non-existing  user

request = factory.post(
    "/api/accounts/register/",
    {
        "email": "johnny@gmail.com",
        "password": "12345",
        "confirm_password": "12345",
    },
)

message = {
    "message": "The email Address 'johnny@gmail.com' has successfully been registered",
    "success": True,
    "data": [],
}
self.assertEqual(response.status_code, status.HTTP_201_CREATED)

2. Without any input data,

request = factory.post(
    "/api/accounts/register/",
    {},
)

message = {
    "success": False,
    "error-code": None,
    "errors": {
        "email": ["email field is required"],
        "password": ["password field is required"],
        "confirm_password": ["confirm_password field is required"],
    },
    "message": "Validation errors has occurred",
}
self.assertEqual(response.status_code, status.HTTP_400_BAD_REQUEST)

3. password and confirm_passwords do not match

request = factory.post(
    "/api/accounts/register/",
    {
        "email": "raja@gmail.com",
        "password": "12345",
        "confirm_password": "123456",
    },
)

message = {
    "success": False,
    "error-code": None,
    "errors": {
        "password": ["'password' and 'confirm_password' do not match"],
    },
    "message": "Validation errors has occurred",
}
self.assertEqual(response.status_code, status.HTTP_400_BAD_REQUEST)


