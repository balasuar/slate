## Rates by Zip Code

Retrieves the composite and local jurisdictional standard sales tax rates for a given zip5 location.

`GET http://api.taxrates.avalara.com/postal?<address>`

### Request
    
```shell
curl "https://api.taxrates.avalara.com/address?country=USA&postal=98101" \
  -H "Authorization: AvalaraApiKey {apikey}" \
  -H "Accept: text/json"
```

```csharp
// A C# sample is not available for this resource at this time.
```

```php
# A PHP sample is not available for this resource at this time.
```

```java
// A Java sample is not available for this resource at this time.
```

**country** string, *required*   
country code in ISO 3166-1 alpha-3 format e.g.: "USA", "CAN", "GBR"  
    
**postal** string, *required*   
zip code of the address e.g.: "98101", "V8X 3X4", "BH1 1AA" 


### Response

```json
{ 
   "totalRate":9.500000,
   "rates":[ 
      { 
         "rate":3.00000,
         "name":"SEATTLE",
         "type":"City"
      },
      { 
         "rate":6.500000,
         "name":"WASHINGTON",
         "type":"State"
      }
   ]
}
```

**totalRate** double  
Contains the total tax rate for the location in question. Note that it is not a percentage; in the example above, the totalRate of 0.086 represents a tax rate of 8.6%.

**rates** rate array  
Each object in the rates array represents a single jurisdiction's contribution to the totalRate.

**rate.rate** double  
Note that a rate field may not always be present; in these cases, the contribution is 0.0%.

**rate.name** string  

**rate.type** string 