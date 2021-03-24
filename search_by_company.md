1. User enters a company name which exists in the database, 

```
request = self.factory.get(
        "/api/search",
        {"company_name": "Vodacom"},
        HTTP_AUTHORIZATION=f"Bearer {access_token}",
)
```
Assuming the request is a success, the below response will be sent to the client,

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

Also, remember that the API searches for partial names too. At this moment, I do not the know 
the performance impact, by will find a way or return partial search results
