## Address Resolution

### Resolve a single address
```html
POST https://tax.api.avalara.com/address/account/<accountId>/company/<companyCode>/resolve
```
#### Request
```csharp
TBD
```

```java
TBD
```

```php
TBD
```
```shell
curl --include \
     --request POST \
     --header "Content-Type: application/json" \
     --header "Accept: application/json; tax-version=1" \
     --header "User-Agent: Agent X Connector v12" \
     --header "Authorization: AvalaraAuth MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \
     --@/Docs/address.json
     'https://tax.api.avalara.com/address/account/98723878-2323-8742-2387-639826739098/company/Default/resolve'
```
```json
{
  "line1": "100 Ravine Ln NE",
  "city": "Bainbridge Island",
  "state": "WA",
  "zipcode": "98110",
  "country": "USA"
}
```
**line1** string  
The first line of the address.

**line2** string  
The second line of the address.

**line3** string  
The third line of the address.

**city, municipality, town** string  
The city of the address. Synonyms are provided to allow for regional terminology, but only one of the three should be included in a given location.

**state, province** string  
The state of the address. Synonyms are provided to allow for regional terminology, but only one of the two should be included in a given location.

**country** string  
The country code in ISO 3166-1 alpha-2 or alpha-3 format.

**zipcode, postalCode, postCode** string  
The zip code of the address. Synonyms are provided to allow for regional terminology, but only one of the three should be included in a given location.

#### Response
```plaintext
200
Content-Type: application/json
```
```json
{
  "address": {
    "line1": "100 Ravine Lane Northeast",
    "city": "Bainbridge Island",
    "state": "WA",
    "country": "US",
    "postalCode": "98110-2687",
    "zipcode": "98110-2687",
    "municipality": "Bainbridge Island",
    "town": "Bainbridge Island",
    "province": "WA",
    "postcode": "98110-2687"
  },
  "coordinates": {
    "latitude": 47.62489,
    "longitude": -122.514964
  },
  "resolutionQuality": "Rooftop",
  "taxAuthorities": [
    {
      "avalaraId": "0000000000000000cb8f020000000000",
      "jurisdictionName": "BAINBRIDGE ISLAND",
      "jurisdictionType": "City",
      "signatureCode": "BVXY"
    },
    {
      "avalaraId": "0000000000000000ab0b000000000000",
      "jurisdictionName": "KITSAP",
      "jurisdictionType": "County",
      "signatureCode": "BVXV"
    },
    {
      "avalaraId": "00000000000000003d00000000000000",
      "jurisdictionName": "WASHINGTON",
      "jurisdictionType": "State",
      "signatureCode": "BVPJ"
    },
    {
      "avalaraId": "00000000000000007b00000000000000",
      "jurisdictionName": "United States",
      "jurisdictionType": "Country",
      "signatureCode": ""
    },
    {
      "avalaraId": "00000000000000000000000000000001",
      "jurisdictionName": "Planet",
      "jurisdictionType": "Global"
    }
  ]
}
```

**address** address  
The validated address. Note that if all synonymous keys will be returned (e.g. city/town/municipality)

**coordinates** coordinates  
The latitude and longitude representing the address resolution location.

**resolutionQuality** string  
An indication of how precisely the location information was able to be translated into a latitude / longitude. It will contain one of the following values:

- `NotCoded` location was not geocoded
- `External` location was already geocoded on the request
- `CountryCentroid` Avalara-defined country centroid
- `egionCentroid` Avalara-defined state / province centroid
- `PartialCentroid` geocoded at a level more coarse than a PostalCentroid1
- `PostalCentroidGood` largest postal code (zip5 in US, left three in CA, etc
- `PostalCentroidBetter` better postal code (zip7 in US) 
- `PostalCentroidBest` best postal code (zip9 in US, complete postal code elsewhere)
- `Intersection` nearest intersection
- `Interpolated` interpolated to rooftop
- `Rooftop` assumed to be rooftop level, non-interpolated
- `Constant` pulled from a static list of geocodes for specific jurisdictions

**taxAuthorities** taxAuthority[]  
A list of taxing authorities associated with the resolved address location.

#### taxAuthority
**avalaraId** string  
For internal use only

**jurisdictionName** string  
The name of the jurisdiction

**jurisdictionType** string  
The type of the jurisdiction

**signatureCode** string  
The jurisdiction-assigned reporting code, if available.