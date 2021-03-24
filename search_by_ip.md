1. User enters the IPaddress or a CIDR to search the database.

```
request = self.factory.get(
        "/api/search",
        {"ipaddress": "41.78.68.0"},
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```
Assuming the request is a success, The following response will be sent to the client,

```
{
    'success': True,
    'message': 'Search results for the query: 41.78.68.0',
    'data': {
        'links': {
            'next': None,
            'previous': None
        },
        'total': 1,
        'page': 1, 
        'page_size': 10,
        'results': [{
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
    }
}
```
2. User enters a invalid input data such as an invalid ipaddress or CIDR.

```
request = self.factory.get(
        "/api/search",
        {"ipaddress": "41.78.68.0/34"},
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```

he would receive a 400 bad request response with the following error message,

```
{
    "success": False,
    "error-code": None,
    "errors": {"ipaddress": ["'41.78.68.0/34' is not a valid IPAddress or CIDR"]},
    "message": "Validation errors have occurred",
}
```