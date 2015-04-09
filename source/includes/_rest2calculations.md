## Calculations

To calculate tax but not include that calculation on a future filing (e.g. to present tax on a quote or pre-sale order), use the `Calculations` resource. When you want to record that sale for filing and reporting, you should call the `Transactions` resource.

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
     --header "Authorization: AvalaraAuth MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \
     --@/Docs/taxDocument.json
     'https://tax.api.avalara.com/calculations'
```

> See <a href="#tax-document-response">TaxDocument Request</a> for an example JSON payload.


Creation of a calculation uses the standard <a href="#tax-document-request">TaxDocument request</a> format.

#### Response

```plaintext
Content-Type: application/json
Location: https://tax.api.avalara.com/calculations/account/2ead98c1-ecbf-4708-8d86-b01af8bc13e5/company/MyCo2/Sale/%3A12345
```

> See <a href="#tax-document-response">TaxDocument Response</a> for an example JSON payload.

Retrieving a single calculation results in a response that is identical to that created when generating a calculation. See <a href="#tax-document-response">that format</a> for more detail.

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
     --header "Authorization:  AvalaraAuth MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \
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

Retrieving a single calculation results in a response that is identical to that created when generating a calculation. See <a href="#tax-document-response">that format</a> for more detail.

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
     --header "Authorization:  AvalaraAuth MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \ 'https://tax.api.avalara.com/calculations/account/98723878-2323-8742-2387-639826739098/company/Argosy%20Cruises/Sale?limit=100&startCode=Invoice123&startDate=2014-06-10&endDate=2014-06-12'
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

Calculation records are returned as an array of TaxDocuments with summary information only, as listed below.

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
