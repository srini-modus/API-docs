1. User enters malformed date, which cannot be parsed into 'YYYY-MM-DD' format, 

```
request = self.factory.get(
        "/api/search/date",
        {"date" : "2000-12-121"}, 
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```

he would receive a 400 bad request response with the following error message,

```
{
    "success": False,
    "error-code": None,
    "errors": {"date": ["'2000-12-121' is not a valid date.""]},
    "message": "Validation errors have occurred",
}
```
2. User sends more than one querystring to the search API. 

```
request = self.factory.get(
        "/api/search/date",
        {"date" : "2000-12-12", "company_name": "Vodacom"}, 
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```

That the response will be a 400 bad request with error(s) message as,

```
{
    "success": False,
    "error-code": None,
    "errors": {
        "params": [
            "Please use only one of the query parameters - "
            "'company_name', 'date', 'ipaddress'"
        ]
    },
    "message": "Validation errors have occurred",
}
```

3. User enters a date name which exists in the database, 

```
request = self.factory.get(
        "/api/search/date",
        {"date": "2017-12-20"},
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```
Assuming the request is a success, all the records that match `last_updated_at` will be sent back to the client,

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
