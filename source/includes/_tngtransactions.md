## Transactions


To calculate tax but not include that calculation on a future filing (e.g. to present tax on a quote or pre-sale order), use the `Calculations` resource. When you want to record that sale for filing and reporting, you should call the `Transactions` resource.

The request and response formats for both resources is the same, and the response simply adds tax calculation and resolution information to the request format. All formats are documented in the TaxDocument Format section.

### Create a Transaction

`POST https://tax.api.avalara.com/calculations`

To create a transaction, AvaTax requires a TaxDocument request body.
Making multiple POSTs to the /transactions service with the same companyCode and documentCode will result in the creation of a calculation record on the first call and then updates to that transaction record on subsequent calls.

#### Request

```csharp
TBD
```
```java
TBD
```
``php
TBD
```
```shell
curl --include \
     --request POST \
     --header "Content-Type: application/json" \
     --header "Accept: application/json; tax-version=1" \
     --header "User-Agent: Agent X Connector v12" \
     --header "Authorization: AvalaraAuth : MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \
     --@/Docs/taxDocument.json
     'https://tax.api.avalara.com/transactions'
```

> See <a href="#tax-document-response">TaxDocument Request</a> for an example JSON payload.

Creating a transaction uses the standard <a href="#tax-document-request">TaxDocument request</a> format.

#### Response

```plaintext
Content-Type: application/json
Location: https://tax.api.avalara.com/transactions/account/2ead98c1-ecbf-4708-8d86-b01af8bc13e5/company/MyCo2/Sale/%3A12345
```

> See <a href="#tax-document-response">TaxDocument Response</a> for an example JSON payload.

Creating a transaction uses the standard <a href="#tax-document-response">TaxDocument response</a> format.



### Create a Transaction from a Calculation

`POST https://tax.api.avalara.com/calculations/account/<accountId>/company/<companyCode>/<transactionType>/<documentCode>/transactions`

It may sometimes be convenient to create a tax transaction record directly from a previous tax calculation record, e.g. an unchanged order is now to be invoiced. Tax transaction records can be created from tax calculation records either with a recalculation of the tax (this should be the most common situation) or without recalculation of the tax (this is unusual).

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
     --@/Docs/taxTransactionSummary.json
 'https://tax.api.avalara.com/calculations/account/98723878-2323-8742-2387-639826739098/company/Argosy%20Cruises/Sale/1233122/transactions'
```

```json
{
  "documentCode": "Invoice123",
  "recalculate": true,
  "comment": "Government Contract ABC"
}
```

**recalculate** boolean, *optional*  
Determines if the document will recalculate tax upon transition. Must contain one of the following values: true, false. If this parameter is omitted, tax will be recalculated.

**documentCode** string, *required*  
The documentCode for the new tax transaction record. Should not be confused with the documentCode in the URI, which identifies the source calculation record.

**comment** string, *optional*  
Will be recorded along with the event for audit purposes.

#### Response

```plaintext
Content-Type: application/json
Location: https://tax.api.avalara.com/transactions/account/2ead98c1-ecbf-4708-8d86-b01af8bc13e5/company/MyCo2/Sale/%3A12345
```

> See <a href="#tax-document-response">TaxDocument Response</a> for an example JSON payload.

The location header in the response contains the address of the new tax trasaction record. Note that the companyCode will always be the same for the existing tax calculation record and the new tax transaction record. The response format itself is the same as the standard <a href="#tax-document-response">TaxDocument response</a> format.


### Get a Transaction

```plaintext
GET https://tax.api.avalara.com/transactions/account/<accountId>/company/<companycode>/<transactionType>/<documentCode>
```
Retrieves the most recent version of a single transaction record.

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
  'https://tax.api.avalara.com/transactions/account/98723878-2323-8742-2387-639826739098/company/Default/Sale/1233122'
```

**accountId:** URL encoded string, *required*  
This string is a UUID issued by Avalara to identify the Avalara account that owns the company identified by the companyCode.

**companyCode:** URL encoded string, *required*  
Identifies the company profile/legal entity with which the calculation is associated. This is set when the company is created in the AvaTax system, and is an original parameter of the `POST /transactions` call used to create the calculation record. It is unique within the context of an Account.

**transactionType:** URL encoded string, *required*  
Indicates the type of transaction. Must be one of "Sale", "Purchase" or "Transfer", as identified on the original `POST /transactions` call used to create the transaction record.

**documentCode:** URL encoded string, *required*  
Typically an invoice number, receipt number, returned merchandise authorization number, etc. maintained by the client application to uniquely identify the transaction. Determined by the value passed on the original `POST /transactions` call used to create the calculation record.

#### Response

```plaintext
Content-Type: application/json
```

> See <a href="#tax-document-response">TaxDocument Response</a> for an example JSON payload.

Retrieving a single transaction results in a response that is identical to that created when generating a transaction. See <a href="#tax-document-response">that format</a> for more detail.


### Get a List of Transactions
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
     --header "Authorization: AvalaraAuth : MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \ 'https://tax.api.avalara.com/transactions/account/98723878-2323-8742-2387-639826739098/company/Argosy%20Cruises/Sale?limit=100&startCode=Invoice123&startDate=2014-06-10&endDate=2014-06-12'
```

`GET https://tax.api.avalara.com/transactions/account/<accountId>/company/<companyCode>/<transactionType>?<filterCriteria>`

Retrieves a set of transaction records that fall within the specified filter criteria.

**accountId:** URL encoded string, *required*  
This string is a UUID issued by Avalara to identify the Avalara account that owns the company identified by the companyCode.

**companyCode:** URL encoded string, *required*  
Identifies the company profile/legal entity with which the calculation is associated. This is set when the company is created in the AvaTax system, and is an original parameter of the `POST /transactions` call used to create the calculation record. It is unique within the context of an Account.

**transactionType:** URL encoded string, *required*  
Indicates the type of transaction. Must be one of "Sale", "Purchase" or "Transfer", as identified on the original `POST /transactions` call used to create the calculation record.

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

Transaction records are returned as an array of TaxDocuments with summary information only, as listed below.

##### header
**accountId:** string 
This string is a UUID issued by Avalara to identify the Avalara account that owns the company identified by the companyCode.

**companyCode:** string  
Identifies the company profile/legal entity with which the transaction is associated. This is set when the company is created in the AvaTax system, and is an original parameter of the `POST /transactions` call used to create the transaction record. It is unique within the context of an Account.

**transactionType:** string 
Indicates the type of transaction. Must be one of "Sale", "Purchase" or "Transfer", as identified on the original `POST /calculations` call used to create the transaction record.

**documentCode:** string 
Typically an invoice number, receipt number, returned merchandise authorization number, etc. maintained by the client application to uniquely identify the transaction. Determined by the value passed on the original `POST /transactions` call used to create the transaction record.

**customerCode** string  
A unique identifier of the transactee determined and maintained by the client application. For a sale, this would uniquely identify the customer.

**transactionDate** string: date in ISO 8601 format  
The reporting date of the transaction. Note that this may differ from the date the transaction is recorded and/or the date the effective tax date of the transaction.

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

### Get a Transaction Input

```plaintext
GET https://tax.api.avalara.com//transactions/account/<accountId>/company/<companyCode>/<transactionType>/<documentCode>/source
```
It may be necessary to retrieve a record of the original, unaltered inputs that resulted in a transaction record. This resource allows for retrieval of such input, which will reflect the original user input. The most recent version of the transaction request is retrieved.

#### Request

**accountId:** URL encoded string, *required*  
This string is a UUID issued by Avalara to identify the Avalara account that owns the company identified by the companyCode.

**companyCode:** URL encoded string, *required*  
Identifies the company profile/legal entity with which the calculation is associated. This is set when the company is created in the AvaTax system, and is an original parameter of the `POST /transactions` call used to create the calculation record. It is unique within the context of an Account.

**transactionType:** URL encoded string, *required*  
Indicates the type of transaction. Must be one of "Sale", "Purchase" or "Transfer", as identified on the original `POST /transactions` call used to create the transaction record.

**documentCode:** URL encoded string, *required*  
Typically an invoice number, receipt number, returned merchandise authorization number, etc. maintained by the client application to uniquely identify the transaction. Determined by the value passed on the original `POST /transactions` call used to create the calculation record.


#### Response
```plaintext
Content-Type: application/json
```

> See <a href="#tax-document-response">TaxDocument Request</a> for an example JSON payload.

Retrieving a trsanction input responds with the standard <a href="#tax-document-request">TaxDocument request</a> format.


### Transition a Transaction State

```plaintext
POST https://tax.api.avalara.com/transactions/account/<accountId>/company/<companyCode>/<transactionType>/<documentCode>/stateTransitions
```

Tax transaction record states are managed by the Avalara services. Certain events may cause transitions between the states. 

The stateTransistions is used to record significant events associated with state transitions of the tax transaction record. Supported events are:

Event | Description | Starting state | End state
----|----|----|----
Voided | Send this event to a Recorded tax transaction record to mark it as voided. | Recorded | Voided
UnVoided | Send this event to a Voided tax transaction record to mark it as recorded. | Voided | Recorded
Reconciled | Send this event to a Recorded tax transaction record to indicate that it has been reconciled with client systems and to prevent it from being edited prior to filing. This is useful when a transaction will be filed and you do not want it to change again to facilitate auditing and reconciliation. | Recorded | Reconciled
UnReconciled | Send this event to a Reconciled tax transaction record to indicate that it has not been reconciled and may need to be edited. This is useful when a Tax transaction was erroniously put into the reconciled state. | Reconciled | Recorded
Filed | Send this event to a Reconciled transaction to indicate that it has been part of a tax filing by the client system. | Reconciled | Filed
UnFiled | Send this event to a Filed transaction to indicate that it has NOT been part of a tax filing by the client system. | Filed | Reconciled
FiledByAvalara | This event can only be sent by Avalara Systems | Reconciled | FiledByAvalara

The state of a tax transaction record affects whether it is included in tax filing and whether it can be modified. Transactions can be in one of five states:

State | Description
---|---
Recorded | Transactions in this state have been recorded in the Avalara system. They can be edited. They should be included in an upcoming tax filing.
Voided | Transactions in this state have been recorded in the Avalara system. They cannot be edited. They will not be included in tax filing.
Reconciled | Transactions in this state have been recorded in the Avalara system. They cannot be edited. They are likely to be included in a tax filing shortly.
Filed | Transactions in this state have been recorded in the Avalara system. They cannot be edited. They are likely to have been included in a tax filing by the client systems.
FiledByAvalara | Transactions in this state have been recorded in the Avalara system. They cannot be edited. They have been included in a tax filing by Avalara systems.

#### Request

```shell
curl --include \
     --request POST \
     --header "Content-Type: application/json" \
     --header "Accept: application/json; tax-version=1" \
     --header "User-Agent: 2ead98c1-ecbf-4708-8d86-b01af8bc13e5" \
     --header "Authorization: AvalaraAuth : MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1" \
     --@/Docs/stateTransition.json
'https://tax.api.avalara.com/transactions/account/98723878-2323-8742-2387-639826739098/company/Default/Sale/1233122/stateTransitions'
```
```json
{
  "type": "voided",
  "comment": "SR123: corrected fat finger"
}
```

**type** string, *required*  
Must be one of: "Voided", "UnVoided", "Reconciled", "UnReconciled", "Filed", "UnFiled"

**comment** string, *required*  
A message that will be recorded along with the event for audit purposes.

#### Response

```plaintext
Location: https://tax.api.avalara.com/transactions/account/2ead98c1-ecbf-4708-8d86-b01af8bc13e5/company/MyCo2/Sale/%3A12345
```

A successful request will return a HTTP Status of 201, the location of transaction record in a Location header, and no additional payload information.https://f8ad03296218c1f358e05fb8588c090f2f9d502d.googledrive.com/host/0B7DZjLT2LZrwQVpGNWx2Y1Uwc0U/TNG%20Document%20Flow.jpg
