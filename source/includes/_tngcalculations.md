## Calculations

To calculate tax but not include that calculate on a future filing (e.g. to present tax on a quote or pre-sale order), use the `Calculations` resource. When you want to record that sale for filing and reporting, you should call the `Transactions` resource.

The request and response formats for both resources is the same, and the response simply adds tax calculation and resolution information to the request format. All formats are documented in the TaxDocument Format section.

### Create a Calculation

`POST https://tax.api.avalara.com/calculations`

To calculate tax, AvaTax requires a TaxDocument request body.
Making multiple POSTs to the /calculations service with the same companyCode and documentCode will result in the creation of a calculation record on the first call and then updates to that calculation record on subsequent calls.

Note that DocumentCode is an optional input field on this resource only.

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
     --header "Authorization: AvalaraAuth : MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \
     --@/Docs/cancelTaxRequest.json
     'https://tax.api.avalara.com/calculations'
     
{
  "header": {
    "accountId": "2ead98c1-ecbf-4708-8d86-b01af8bc13e5",
    "companyCode": "MyCo2",
    "transactionType": "Sale",
    "documentCode": "#12345",
    "vendorCode": "VENDOR",
    "currency": "USD",
    "customerCode": "ArgosyCruises",
    "transactionDate": "2014-11-11",
    "purchaseOrderNumber": "32323",
    "metadata": {
      "Ref1": "ABC",
      "Ref2": "DEF"
    },
    "defaultLocations": {
      "ShipTo": {
        "address": {
          "line1": "1100 2nd Ave",
          "line2": "",
          "line3": "",
          "city": "Seattle",
          "state": "WA",
          "zipcode": "98101",
          "country": "USA"
        }
      },
      "ShipFrom": {
        "address": {
          "line1": "1101 Alaskan Way",
          "city": "Seattle",
          "state": "WA",
          "zipcode": "98101",
          "country": "USA"
        }
      }
    }
  },
  "lines": [
    {
      "lineCode": "1",
      "itemCode": "22456366",
      "quantity": 1,
      "avalaraGoodsAndServicesType": "P0000000",
      "extendedAmount": 32.5,
      "itemDescription": "Mens adidas FREEFOOTBALL JANEIRINHA Soccer Shoes",
      "taxIncluded": "false",
      "metadata": {
        "Ref1": "ABC",
        "Ref2": "DEF"
      }
    }
  ],
  "feedback": {
    "latencyData": [
      {
        "latency": 100,
        "versionId": "023897420394782308947230987"
      }
    ]
  }
}

```



#### Response

```plaintext
Content-Type: application/json
Location: https://tax.api.avalara.com/calculations/account/2ead98c1-ecbf-4708-8d86-b01af8bc13e5/company/MyCo2/Sale/%3A12345
```

```json

{
  "header": {
    "accountId": "2ead98c1-ecbf-4708-8d86-b01af8bc13e5",
    "documentCode": "#12345",
    "defaultLocations": {
      "shipFrom": {
        "address": {
          "line1": "1101 Alaskan Way",
          "line3": "",
          "city": "Seattle",
          "state": "WA",
          "country": "US",
          "postalCode": "98101-2981",
          "zipcode": "98101-2981",
          "municipality": "Seattle",
          "town": "Seattle",
          "province": "WA",
          "postcode": "98101-2981"
        },
        "latlong": {
          "latitude": 47.604751,
          "longitude": -122.339483
        }
      },
      "shipTo": {
        "address": {
          "line1": "1100 2nd Avenue",
          "line2": "",
          "line3": "",
          "city": "Seattle",
          "state": "WA",
          "country": "US",
          "postalCode": "98101-2908",
          "zipcode": "98101-2908",
          "municipality": "Seattle",
          "town": "Seattle",
          "province": "WA",
          "postcode": "98101-2908"
        },
        "latlong": {
          "latitude": 47.605984,
          "longitude": -122.335772
        }
      }
    },
    "totalTaxOverrideAmount": 0,
    "transactionType": "sale",
    "companyCode": "MyCo2",
    "customerCode": "ArgosyCruises",
    "transactionDate": "2014-11-11",
    "currency": "USD",
    "taxCalculationDate": "2014-11-11",
    "metadata": {
      "ref1": "ABC",
      "ref2": "DEF"
    }
  },
  "lines": [
    {
      "calculatedTax": {
        "appliedTax": 3.09,
        "subtotalTaxable": 32.5,
        "subtotalExempt": 0,
        "taxAuthorities": [
          {
            "jurisdictionName": "KING",
            "jurisdictionType": "County",
            "details": [
              {
                "taxType": "Sales",
                "rateType": "General",
                "subtotalTaxable": 32.5,
                "subtotalExempt": 0,
                "rate": 0,
                "tax": 0,
                "exempt": false,
                "exemptionReason": "",
                "originLocation": "shipFrom",
                "destinationLocation": "shipTo"
              }
            ]
          },
          {
            "jurisdictionName": "SEATTLE",
            "jurisdictionType": "City",
            "details": [
              {
                "taxType": "Sales",
                "rateType": "General",
                "subtotalTaxable": 32.5,
                "subtotalExempt": 0,
                "rate": 0.03,
                "tax": 0.98,
                "exempt": false,
                "exemptionReason": "",
                "originLocation": "shipFrom",
                "destinationLocation": "shipTo"
              }
            ]
          },
          {
            "jurisdictionName": "WASHINGTON",
            "jurisdictionType": "State",
            "details": [
              {
                "taxType": "Sales",
                "rateType": "General",
                "subtotalTaxable": 32.5,
                "subtotalExempt": 0,
                "rate": 0.065,
                "tax": 2.11,
                "exempt": false,
                "exemptionReason": "",
                "originLocation": "shipFrom",
                "destinationLocation": "shipTo"
              }
            ]
          }
        ]
      },
      "lineCode": "1",
      "itemCode": "22456366",
      "quantity": 1,
      "extendedAmount": 32.5,
      "taxIncluded": false,
      "itemDescription": "Mens adidas FREEFOOTBALL JANEIRINHA Soccer Shoes",
      "locations": {
        "shipFrom": {
          "address": {
            "line1": "1101 Alaskan Way",
            "line3": "",
            "city": "Seattle",
            "state": "WA",
            "country": "US",
            "postalCode": "98101-2981",
            "zipcode": "98101-2981",
            "municipality": "Seattle",
            "town": "Seattle",
            "province": "WA",
            "postcode": "98101-2981"
          },
          "latlong": {
            "latitude": 47.604751,
            "longitude": -122.339483
          }
        },
        "shipTo": {
          "address": {
            "line1": "1100 2nd Avenue",
            "line2": "",
            "line3": "",
            "city": "Seattle",
            "state": "WA",
            "country": "US",
            "postalCode": "98101-2908",
            "zipcode": "98101-2908",
            "municipality": "Seattle",
            "town": "Seattle",
            "province": "WA",
            "postcode": "98101-2908"
          },
          "latlong": {
            "latitude": 47.605984,
            "longitude": -122.335772
          }
        }
      },
      "metadata": {
        "ref1": "ABC",
        "ref2": "DEF"
      }
    }
  ],
  "calculatedTaxSummary": {
    "numberOfTaxableLines": 1,
    "numberOfExemptLines": 0,
    "numberOfLines": 1,
    "subtotalTaxable": 32.5,
    "subtotalExempt": 0,
    "subtotal": 32.5,
    "tax": 3.09,
    "grandTotal": 35.59
  },
  "processingInfo": {
    "transactionState": "Recorded",
    "versionId": "617618abc38c11e48fef06e9f1154310",
    "formatId": 3,
    "duration": 112,
    "modifiedDate": "2015-03-05T23:07:22.6862321Z",
    "documentId": "231438abc38c11e48fef06e9f1154310"
  }
}
```




### Get a Calculation

```plaintext
GET https://tax.api.avalara.com/calculations/account/<accountId>/company/<companycode>/<transactionType>/<documentCode>
```

Retrieves the most recent version of a single calculation record.

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
     --header "Accept: application/json; tax-version=1" \
     --header "User-Agent: "QBO v12"" \
     --header "Authorization: AvalaraAuth : MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \
  'https://tax.api.avalara.com/calculations/account/98723878-2323-8742-2387-639826739098/company/Default/Sale/1233122'
```

**accountId:** URL encoded string, *required*  
This string is a UUID issued by Avalara to identify the Avalara account that owns the company identified by the companyCode.

**companyCode:** URL encoded string, *required*  
Identifies the company profile/legal entity with which the calculation is associated. This is set when the company is created in the AvaTax system, and is an original parameter of the `POST /calculations` call used to create the calculation record. It is unique within the context of an Account.

**transactionType:** URL encoded string, *required*  
Indicates the type of transaction. Must be one of "Sale", "Purchase" or "Transfer", as identified on the original `POST /calculations` call used to create the calculation record.

**documentCode:** URL encoded string, *required*  
Typically an invoice number, receipt number, returned merchandise authorization number, etc. maintained by the client application to uniquely identify the transaction. Determined by the value passed on the original `POST /calculations` call used to create the calculation record.

#### Response

```plaintext
Content-Type: application/json
```

```json

{
  "header": {
    "accountId": "2ead98c1-ecbf-4708-8d86-b01af8bc13e5",
    "documentCode": "#12345",
    "defaultLocations": {
      "shipFrom": {
        "address": {
          "line1": "1101 Alaskan Way",
          "line3": "",
          "city": "Seattle",
          "state": "WA",
          "country": "US",
          "postalCode": "98101-2981",
          "zipcode": "98101-2981",
          "municipality": "Seattle",
          "town": "Seattle",
          "province": "WA",
          "postcode": "98101-2981"
        },
        "latlong": {
          "latitude": 47.604751,
          "longitude": -122.339483
        }
      },
      "shipTo": {
        "address": {
          "line1": "1100 2nd Avenue",
          "line2": "",
          "line3": "",
          "city": "Seattle",
          "state": "WA",
          "country": "US",
          "postalCode": "98101-2908",
          "zipcode": "98101-2908",
          "municipality": "Seattle",
          "town": "Seattle",
          "province": "WA",
          "postcode": "98101-2908"
        },
        "latlong": {
          "latitude": 47.605984,
          "longitude": -122.335772
        }
      }
    },
    "totalTaxOverrideAmount": 0,
    "transactionType": "sale",
    "companyCode": "MyCo2",
    "customerCode": "ArgosyCruises",
    "transactionDate": "2014-11-11",
    "currency": "USD",
    "taxCalculationDate": "2014-11-11",
    "metadata": {
      "ref1": "ABC",
      "ref2": "DEF"
    }
  },
  "lines": [
    {
      "calculatedTax": {
        "appliedTax": 3.09,
        "subtotalTaxable": 32.5,
        "subtotalExempt": 0,
        "taxAuthorities": [
          {
            "jurisdictionName": "KING",
            "jurisdictionType": "County",
            "details": [
              {
                "taxType": "Sales",
                "rateType": "General",
                "subtotalTaxable": 32.5,
                "subtotalExempt": 0,
                "rate": 0,
                "tax": 0,
                "exempt": false,
                "exemptionReason": "",
                "originLocation": "shipFrom",
                "destinationLocation": "shipTo"
              }
            ]
          },
          {
            "jurisdictionName": "SEATTLE",
            "jurisdictionType": "City",
            "details": [
              {
                "taxType": "Sales",
                "rateType": "General",
                "subtotalTaxable": 32.5,
                "subtotalExempt": 0,
                "rate": 0.03,
                "tax": 0.98,
                "exempt": false,
                "exemptionReason": "",
                "originLocation": "shipFrom",
                "destinationLocation": "shipTo"
              }
            ]
          },
          {
            "jurisdictionName": "WASHINGTON",
            "jurisdictionType": "State",
            "details": [
              {
                "taxType": "Sales",
                "rateType": "General",
                "subtotalTaxable": 32.5,
                "subtotalExempt": 0,
                "rate": 0.065,
                "tax": 2.11,
                "exempt": false,
                "exemptionReason": "",
                "originLocation": "shipFrom",
                "destinationLocation": "shipTo"
              }
            ]
          }
        ]
      },
      "lineCode": "1",
      "itemCode": "22456366",
      "quantity": 1,
      "extendedAmount": 32.5,
      "taxIncluded": false,
      "itemDescription": "Mens adidas FREEFOOTBALL JANEIRINHA Soccer Shoes",
      "locations": {
        "shipFrom": {
          "address": {
            "line1": "1101 Alaskan Way",
            "line3": "",
            "city": "Seattle",
            "state": "WA",
            "country": "US",
            "postalCode": "98101-2981",
            "zipcode": "98101-2981",
            "municipality": "Seattle",
            "town": "Seattle",
            "province": "WA",
            "postcode": "98101-2981"
          },
          "latlong": {
            "latitude": 47.604751,
            "longitude": -122.339483
          }
        },
        "shipTo": {
          "address": {
            "line1": "1100 2nd Avenue",
            "line2": "",
            "line3": "",
            "city": "Seattle",
            "state": "WA",
            "country": "US",
            "postalCode": "98101-2908",
            "zipcode": "98101-2908",
            "municipality": "Seattle",
            "town": "Seattle",
            "province": "WA",
            "postcode": "98101-2908"
          },
          "latlong": {
            "latitude": 47.605984,
            "longitude": -122.335772
          }
        }
      },
      "metadata": {
        "ref1": "ABC",
        "ref2": "DEF"
      }
    }
  ],
  "calculatedTaxSummary": {
    "numberOfTaxableLines": 1,
    "numberOfExemptLines": 0,
    "numberOfLines": 1,
    "subtotalTaxable": 32.5,
    "subtotalExempt": 0,
    "subtotal": 32.5,
    "tax": 3.09,
    "grandTotal": 35.59
  },
  "processingInfo": {
    "transactionState": "Recorded",
    "versionId": "617618abc38c11e48fef06e9f1154310",
    "formatId": 3,
    "duration": 112,
    "modifiedDate": "2015-03-05T23:07:22.6862321Z",
    "documentId": "231438abc38c11e48fef06e9f1154310"
  }
}
```




### Get a List of Calculations

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
     --header "Accept: application/json; tax-version=1" \
     --header "User-Agent: NetDynamics Connector v12" \
     --header "Authorization: AvalaraAuth : MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \
  'https://tax.api.avalara.com/calculations/account/98723878-2323-8742-2387-639826739098/company/Argosy%20Cruises/Sale?limit=100&startCode=Invoice123&startDate=2014-06-10&endDate=2014-06-12'
```

`GET https://tax.api.avalara.com/calculations/account/<accountId>/company/<companyCode>/<transactionType>?<filterCriteria>`

Retrieves a set of calculation records that fall within the specified filter criteria.

**accountId:** URL encoded string, *required*  
This string is a UUID issued by Avalara to identify the Avalara account that owns the company identified by the companyCode.

**companyCode:** URL encoded string, *required*  
Identifies the company profile/legal entity with which the calculation is associated. This is set when the company is created in the AvaTax system, and is an original parameter of the `POST /calculations` call used to create the calculation record. It is unique within the context of an Account.

**transactionType:** URL encoded string, *required*  
Indicates the type of transaction. Must be one of "Sale", "Purchase" or "Transfer", as identified on the original `POST /calculations` call used to create the calculation record.

**limit:** integer, *optional*  
The maximum number of records that should be returned. Records are ordered by TransactionDate and then by ModifiedDate.

**startDate:** URL encoded date in ISO format, *optional*  
This is the first TransactionDate to include in the search.

**endDate:** URL encoded date in ISO format, *optional*  
This is the first TransactionDate to include in the search.

**startCode:** URL encoded string, *optional*  
Not Implemented

#### Response

```json
[
  {
    "header": {
      "accountId": "2ead98c1-ecbf-4708-8d86-b01af8bc13e5",
      "companyCode": "MyCo2",
      "transactionType": "Sale",
      "documentCode": "#12345",
      "customerCode": "ArgosyCruises",
      "transactionDate": "2014-06-11"
    },
    "lines": [
      {
        "avalaraGoodsAndServicesModifierType": "Title"
      }
    ],
    "calculatedTaxSummary": {
      "subtotalTaxable": 32.5,
      "subtotalExempt": 0,
      "tax": 3.09
    },
    "processingInfo": {
      "transactionState": "Recorded",
      "modifiedDate": "2015-03-05T23:07:22.6862321Z",
      "batchId": "123213"
    }
  },
  {
    "header": {
      "accountId": "2ead98c1-ecbf-4708-8d86-b01af8bc13e5",
      "companyCode": "A1 Boats",
      "transactionType": "Sale",
      "documentCode": "#12346",
      "customerCode": "LetsGoSailing",
      "transactionDate": "2014-06-12"
    },
    "lines": [
      {
        "avalaraGoodsAndServicesModifierType": "Title"
      },
      {
        "avalaraGoodsAndServicesModifierType": "Rental"
      }
    ],
    "calculatedTaxSummary": {
      "subtotalTaxable": 11.23,
      "subtotalExempt": 4,
      "tax": 2.53
    },
    "processingInfo": {
      "transactionState": "Recorded",
      "modifiedDate": "2014-06-11 19:33:53Z"
    }
  },
  {
    "header": {
      "accountId": "2ead98c1-ecbf-4708-8d86-b01af8bc13e5",
      "companyCode": "A1 Boats",
      "transactionType": "Sale",
      "documentCode": "#12347",
      "customerCode": "WSDOT",
      "transactionDate": "2014-06-13"
    },
    "lines": [
      {
        "avalaraGoodsAndServicesModifierType": "Title"
      }
    ],
    "calculatedTaxSummary": {
      "subtotalTaxable": 12.23,
      "subtotalExempt": 7,
      "tax": 0.53
    },
    "processingInfo": {
      "transactionState": "Voided",
      "modifiedDate": "2014-06-11 19:33:53Z",
      "batchId": "123213"
    }
  }
]
```

Calculation records are returned as an array of TaxDocuments with summary information, as listed below.

##### header
**accountId:** string 
This string is a UUID issued by Avalara to identify the Avalara account that owns the company identified by the companyCode.

**companyCode:** string  
Identifies the company profile/legal entity with which the calculation is associated. This is set when the company is created in the AvaTax system, and is an original parameter of the `POST /calculations` call used to create the calculation record. It is unique within the context of an Account.

**transactionType:** string 
Indicates the type of transaction. Must be one of "Sale", "Purchase" or "Transfer", as identified on the original `POST /calculations` call used to create the calculation record.

**documentCode:** string 
Typically an invoice number, receipt number, returned merchandise authorization number, etc. maintained by the client application to uniquely identify the transaction. Determined by the value passed on the original `POST /calculations` call used to create the calculation record.

**customerCode** string  
A unique identifier of the transactee determined and maintained by the client application. For a sale, this would uniquely identify the customer.

**transactionDate** string: date in ISO 8601 format  
The reporting date of the transaction. Note that this may differ from the date the transaction is recorded and/or the date the effective tax date of the calculation.

##### lines
**avalaraGoodsAndServicesModifiertype** string  
Identifies a category of products for tax purposes. It will likely be one of Avalara's standard avalaraGoodsAndServicesTypes, but may be a custom type configured in the Customer Portal. 

##### calculatedTaxSummary
**subtotalTaxable** decimal  
Total sale amount to which tax was applied.

**subtotalExempt**  decimal  
Total sale amount which was excluded from tax.

**tax** decimal  
Amount of tax due for this transaction.

##### processingInfo
**transactionState** string  
State of the transaction in the Avalara systems. Available values are: ????????

**modifiedDate** string, date in ISO 8601.
The timestamp of the most recent update to the document.

**batchId**
If the document was processed in a batch, this identifies the most recent batch in which it was included. If the document was never part of a batch, this field/value is omitted. 
