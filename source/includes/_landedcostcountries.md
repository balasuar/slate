## Countries and Classifications

These are convenience APIs around supported countries and classification systems.

### Get a list of supported countries

Returns the countries we currently support, along with most common classification system for both import and export.

#### Request
```plaintext
GET http://sandbox.landedcost.api.avalara.com/v2/countries
```
No request parameters are required for this call. The method returns a full list of supported countries. 

#### Response
```plaintext
200
Content-type: application/json
```
```json
{
  "destination": [
    {
      "code": "US",
      "name": "The United States",
      "system": "HTS"
    },
    {
      "code": "BE",
      "name": "Belgium",
      "system": "TARIC"
    },
    {
      "code": "GB",
      "name": "The United Kingdom",
      "system": "TARIC"
    }
  ],
  "source": [
    {
      "code": "US",
      "name": "The United States",
      "system": "SCHEDULEB"
    },
    {
      "code": "BE",
      "name": "Belgium",
      "system": "TARIC"
    },  
    {
      "code": "GB",
      "name": "The United Kingdom",
      "system": "TARIC"
    }
  ]
}
```
Note that, in this sample response, the full list of supported countires had been abbreviated for brevity.


**destination** array  
A list of countries supported as import destinations, with the classification system used by that country to classify imported goods.

**source** array  
A list of countries supported as export origins, with the classificaiton system used by that country to classify exported goods.

**code** string  
The two-character ISO country code.

**name** string  
The name of the country.

**system** string  
The item classification system used by this country. Will be one of:  

- TARIC 
- SCHEDULEB
- HTS

### Get the classification systems for a country

Returns a pair of classification (import and export) systems for trade between two countries.

#### Request

```plaintext
GET http://sandbox.landedcost.api.avalara.com/v2/systems?source=US&destination=DE
```
**source** string, required  
The 2-character ISO code for the source country.

**destination** string, required
The 2-character ISO code for the destination country.

#### Response
```plaintext
200
Content-type: application/json
```
```json
{
  "export": {
    "system": "SCHEDULEB"
  },
  "import": {
    "system": "TARIC"
  }
}
```

**export** system  
The system of export classification between the source and destination countries specified.

**import** system  
The system of import classification between the source and destination countries specified.

**system** string  
The classification system. One of: 

- TARIC 
- SCHEDULEB
- HTS





