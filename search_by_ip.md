1. User enters the IPaddress or a CIDR to search the database.

```
request = self.factory.get(
        "/api/search/ipaddress",
        {"ipaddress": "41.78.68.0"},
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```
Assuming the request is a success, The following response will be sent to the client,

```
[{
    'rir_provider_code':'ARIN',
    'status_code': 'ALLOCATED',
    'address_type': 'IPv4',
    'network_address': '41.78.68.0/22',
    'country_or_economic_zone': 'TZ',
    'last_updated_at': '2017-12-20',
    'organisation_name': 'Vodacom',
    'organisation_country': 'ZA',
    'organisation_address': 'PO Box 7243,Roggebaai,Cape Town 8012',
    'phone_number': 'tel:+27-21-940-9400',
    'fax_number': '',
    'parent_network_address': '41.0.0.0/8',
    'source', 'ARIN'
}]
```
2. User does not enter any data and hits search 
```
request = self.factory.get(
        "/api/search/ipaddress",
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```

he would receive an 400 bad request response with the following error message,

```
{
    "success": False,
    "error-code": None,
    "errors": {"ipaddress": ["'ipaddress' parameter is required."]},
    "message": "Validation errors have occurred",
}
```

3. User enters an invalid input data such as an invalid ipaddress or CIDR.

```
request = self.factory.get(
        "/api/search/ipaddress",
        {"ipaddress": "41.78.68.0/34"},
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```

he would receive an 400 bad request response with the following error message,

```
{
    "success": False,
    "error-code": None,
    "errors": {"ipaddress": ["'41.78.68.0/34' is not a valid IPAddress or CIDR"]},
    "message": "Validation errors have occurred",
}
```