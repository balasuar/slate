## Tax Document Response
### header
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

**vendorCode** string  
Alias of customerCode, offered to improve readability on Purchase Invoice type transactions. A unique identifier of the transactee determined and maintained by the client application. For a purchase, this would uniquely identify the vendor.

**transactionDate** string: date in ISO 8601 format  
The reporting date of the transaction. Note that this may differ from the date the transaction is recorded and/or the date the effective tax date of the calculation.

**currencyCode:** string: currency in ISO 4217:2008 format  
Not currently supported.

**totalTaxOverrideAmount:** decimal, *optional*
Not currently supported. An optional input tax amount to override the total tax amount calculated for the document. This may be used for imported transactions, returns, and layaways where the tax has already been calculated (either by AvaTax or by an external system). If provided at the TaxDocument.header level, this amount is pro rated across all taxable line items. To specify a tax override amount at the individual line level, see line.taxOverrideAmount.

**taxCalculationDate:** string: date in ISO 8601 format  
The date that should be used to determine the appropriate tax rates, rules, and jurisdictions, independent of transaction's reporting date. If not provided, this will default to the transactionDate. Useful for layaways, credit memos, and other deferred transactions.

**defaultAvalaraGoodsAndServicesModifierType:** string  
Not currently supported. The default product subcategory (goods and services modifier) to be used for all lines that do not override this value. The Avalara goods and services type determines the specific type of goods or services associated with a particular line in the transaction. The Avalara goods and services modifier determines variations on the goods and services type. For example, if the goods were a type of food, the modifier might be "dine in" or "take out". If the goods and services were a "bicycle" the modifier might be "rental" versus "title".

**defaultLocations:** dictionary of locations, *required, unless specified at the line level*  
This element contains a dictionary of locations such as the origin and destination addresses to be associated with this transaction. These locations may be overridden within each line item. The key for each location in the dictionary is the location "purpose". Valid locations purposes are "ShipFrom", "ShipTo", "POS", "POM", "POO", "BillingLocation", "CallPlaced", "CallReceived", "ServiceRendered", "POA" and "FirstUse". There can only be one location of a given purpose in the dictionary.

**defaultTaxPayerCode:** string  
Not currently supported. An identifier issued by a tax authority that identifies the transacting party (typically the customer associated with the customerCodefiled) as tax exempt for this transaction type. If set, will apply to all lines in this transaction that do not override it.

**defaultEntityUseType:** string, *optional*
The type of customer or type of use. Used to apply particular customer group taxability behavior. If set, will apply to all lines in the transaction that do not override it. Valid values are:

- A - Federal Government,
- B - State/Local Govt.
- C - Tribal Government
- D - Foreign Diplomat
- E - Charitable Organization
- F - Religious/Education
- G - Resale
- H - Agricultural Production
- I - Industrial Prod/Mfg.
- J - Direct Pay Permit
- K - Direct Mail
- L - Other
- N - Local Government
- P - Commercial Aquaculture (Canada)
- Q - Commercial Fishery (Canada)
- R - Non-resident (Canada)

**purchaseOrderNumber:** string  
A purchase order number which might be used to look up a single use tax exemption certification

**metadata** metadataItem  
A collection of MetadataItems (string pairs) which exists to allow callers of the API to set arbitrary information that will be returned in the tax calculation response and which can be used during reporting.

### line
**lineCode** string  
A unique identifier for this line in the transaction.

**itemCode** string  
A code maintained by the client application to uniquely identify a product or service. Usually SKU or similar. Required for SST states.

**avalaraGoodsAndServicesType** string  
Identifies a category of products for tax purposes. It will likely be one of Avalara's standard avalaraGoodsAndServicesTypes, but may be a custom type configured in the Customer Portal. If not specified, itemCode to avalaraGoodsAndServicesType mapping will happen during tax calculation. Currently only "P0000000" (Tangible Personal Property) is supported.

**avalaraGoodsAndServicesModifierType** string  
Not currently supported. A goods and services modifier to be used for this line. The Avalara goods and services type determines the specific type of goods or services associated with a particular line in the transaction. The Avalara goods and services modifier determines variations on the goods and services type. For example, if the goods were a type of food, the modifier might be "dine in" or "take out". If the goods and services were a "bicycle" the modifier might be "rental" versus "title".

**quantity** decimal  
The number of individual units represented by this line. Digits after the decimal point are optional.

**extendedAmount** decimal  
The total cost of this line. In its simplest form extendedAmount = unit price * quantity.

**itemDescription** string  
Description of the item represented by this line

**unitOfMeasure** string  
Not currently supported. The unit of measure associated with this line item. The default unit is "Each" if this field is not specified.

**locations** enum, *required if not specified at the header*  
A dictionary of locations such as the ShipFrom and ShipTo addresses to be associated with this line. These locations may override those specified in a transaction header. The key for each location in the dictionary is the location "purpose". Valid location purposes are:

- "ShipFrom"
- "ShipTo"
- "POS"
- "POM"
- "POO"
- "BillingLocation"
- "CallPlaced"
- "CallReceived"
- "ServiceRendered"
- "POA"
- "FirstUse". 

There can only be one location of a given purpose in the dictionary.

**taxPayerCode** string  
Not currently supported. a code issued by a tax authority to identify a party (typically the customer associated with the customerId field) that is exempt from tax for this type of transaction. This value will override any value set at the transaction level.

**entityUseType** string  
Not currently supported. This string captures the type of customer or type of use associated with this line in the transaction. Valid values are:

- A - Federal Government
- B - State/Local Govt. 
- C - Tribal Government
- D - Foreign Diplomat 
- E - Charitable Organization 
- F - Religious/Education 
- G - Resale
- H - Agricultural Production 
- I - Industrial Prod/Mfg. 
- J - Direct Pay Permit 
- K - Direct Mail 
- L - Other 
- N - Local Government 
- P - Commercial Aquaculture (Canada) 
- Q - Commercial Fishery (Canada) 
- R - Non-resident (Canada)

**taxOverrideAmount** decimal  
Not currently supported. A Tax Override Amount which overrides the tax for the line. This may used for imported transactions, returns, and layaways where the tax has already been calculated either by AvaTax or another means.

**taxIncluded** boolean  
Not currently supported. Indicates whether the extendedPrice includes tax or not. It must be either "true" or "false" if present.

**metadata** metadataItem  
A collection of MetadataItems (string pairs) which exists to allow callers of the API to set arbitrary information that will be returned in the tax calculation response and which can be used during reporting

**calculatedTax** calculatedTax   
Contains the calculated tax information for this line item. This element is created by the tax service and overwritten if it exists in a request.

### calculatedTaxSummary
**numberOfTaxableLines** integer   
Number of lines that were determined to have tax due on them

**numberOfExemptLines**	integer   
Number of lines that were determined to not have any tax due on them

**numberOfLines** integer  
Number of lines in the transaction

**subtotal** decimal  
Subtotal for this transaction

**subtotalTaxable**	decimal  
Amount that had tax applied to it

**subtotalExempt** decimal  
Amount of this transaction that was not taxed.

**tax** decimal  
Amount of tax due for this transaction.

**grandTotal** decimal  
Total due to be paid by the purchaser to the seller including tax.

### processingInfo

**transactionState** string  
The state of the transaction in the Avalara systems. It will have a value equal to the name of one of the possible transaction states:

- Calculated
- Recorded
- Cancelled

**versionId** string  
Server-assigned unique identifier for the tax calculation.

**formatId** integer  
The format of this transaction, which may be useful for support queries.

**duration** decimal  
The number of seconds taken to process the tax calculation.

**modifiedDate** string  
The date, in ISO 8601 format, on which the most recent update to this document was posted

**batchId** string  
If the document was processed in a batch, this identifies the most recent batch in which it was included. If the document was never part of a batch, this field/value is omitted. 

**documentId** string  
Avalara versionId of the original transaction that created the entry.

**message** string  
Allows Avalara to pass information back to the caller. e.g. "Warning: format 3 as used in this transaction is deprecated by format 4 and may not be supported in the future."

### feedback
**latencyData** latencyInfo  
The feedback element allows clients to inform Avalara of the total roundtrip latency of calls, allowing Avalara support to better understand how well we're serving our customers.

#### latencyInfo
**latency** integer  
The latency in miliseconds for a previous call from the client perspective.

**versionId** string  
The versionId (returned to the client in the processingInfo.versionId field) of the transaction for which latency is being passed.


### location
Locations capture the physical locations associated with a transaction, identifying each point with a locationType enumerated in the table below.
To calculate tax for a line in a transaction, the tax calculation engine may need to know about the "origin" and the "destination" of the transaction. Sometimes determining these locations is straight forward, as in the case of an item purchased in person at a retail store for immediate consumption (a single POS address would suffice to indicate the origin and destination of the transaction). Other cases are only slightly more complicated, such as when a product is purchased over the phone and shipped from a warehouse to the customer's house. In this second case, a Ship-from location would serve as the origin, and a Ship-to location would serve as the destination.
Exactly which locations are required for a given transaction depends on the context of transaction. Specifically, such things as the transactionType, avalaraGoodsAndServicesType, and applicable jurisdictions may influence what location information is required in order to calculate tax. In the case where more than one location of a given category (origin/destination) is associated with a line, the jurisdiction will determine which location is used, and this will be indicated in the calculation response. The locations can be associated at the line level or the line can inherit the location from the header.

**taxLocationPurpose** enum  
The type of location identified by the element. Each distinct type can be used as a destination or origin address depending on the sale type, as outlined in the table below:

taxLocationPurpose | Category | Description
-----|-----|-----
ShipFrom | origin | shipping origin of the transaction or line item
CallPlaced | origin | point of origin of a phone call
POM | origin | point of manufacture of an item
POA | origin | point of access to an item
Dropship | origin | drop shipment location of an item
POS | origin & destination | point of sale of an item
ShipTo | destination | ship to location of an item
POO | destination | point of order origin of an item
BillingLocation | destination | billing location of an item
CallReceived | destination |  destination of a phone call
ServiceRendered | destination | location a service item was rendered
FirstUse | destination | location of first use of an item


**address**	address  
This element contains a street or shipping address. The tax calculation service will convert this to a lat/long. See address format below.

**latlong**	latlong  
This element contains a latitude and longitude.	See latlong format below.

**locationCode** string  
Not currently supported. The identity of a pre-configured location unique to the company.	

**IpAddress** string  
Not currently supported. An IP address for digital distribution. This field is not currently supported.

**addressTaxPayerCode** string  
Not currently supported. This taxPayerCode overrides any taxPayerCode that may have been specified in the header or line item if this address is determined to govern the selection of tax rules (i.e.: if the transaction is sourced to this address).

**addressEntityUseType** string  
Not currently supported. This entityUseType overrides any entityUseType that may have been specified in the header or line item if this address is determined to govern the selection of tax rules (i.e.: if the transaction is sourced to this address). Valid values are:

- A - Federal Government
- B - State/Local Govt. 
- C - Tribal Government
- D - Foreign Diplomat 
- E - Charitable Organization 
- F - Religious/Education 
- G - Resale
- H - Agricultural Production 
- I - Industrial Prod/Mfg. 
- J - Direct Pay Permit 
- K - Direct Mail 
- L - Other 
- N - Local Government 
- P - Commercial Aquaculture (Canada) 
- Q - Commercial Fishery (Canada) 
- R - Non-resident (Canada)

#### latlong

**latitude** decimal  
The latitude of the transaction

**longitude** decimal  
The longitude of the transaction

#### address

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

### metadataItem

Each MetadataItem in the list is a name / value pair, which can be used in reporting and for reference information.
For example:
`"customerRef":"12345",`
`"comment":"this was done to compensate for a previous customer satisfaction issue",`
`"PurchaseOrder":"PO1232", "SalesPersonCode":"21123"`

### calculatedTax

**appliedTax** decimal  
The total tax applicable for this line.

**subtotalTaxable** decimal  
How much of the extendedAmount was taxable. The subtotal taxable may vary from jurisdiction to jurisdiction and from tax to tax, and this number represents the highest amount taxed from any tax in any jurisdiction.

**subtotalExempt** decimal  
How much of the extendedAmount was non-taxed. This is simply the extended amount minus the subtotal taxed.

**taxAuthorities** taxAuthorities  
A list of elements breaking out the tax authorities that apply to this line.

#### taxAuthorities

**jurisdictionName** string  
The name of the taxing jurisdiction.

**jurisdictionType** string  
The type of taxing jurisdiction.

**details** details  
A list of elements capturing the types and amounts of tax imposed by this jurisdiction.

##### details

Note that sometimes a single tax may be banded, meaning that it applies at different rates depending on the extendedAmount (or individual amount) of the item. Each band will have its own detail in the list.

**taxType**	string 
The type of the tax, e.g. "sales"

**rateType** string  
The type of the rate used

**subtotalTaxable**	decimal  
How much of the extendedAmount was taxable by this tax

**subtotalExempt** decimal  
How much of the extendedAmount was non-taxed. This is simply the extended amount minus the subtotal taxed.

**rate** decimal  
The tax rate for this tax.

**tax** decimal  
The product of subtotalTaxable and rate.

**exempt** boolean  
Used to indicate that this customer is exempt from this tax for this transaction.

**exemptionReason** string  
A required reason if the exempt flag is present and set to true.

**originLocation** location  
This element captures the location determined to be the "origin" for this tax detail based on the locations associated with this line. One of "ShipFrom", "CallPlaced", "POM", "POA", "DropShip", "POS"	"ShipFrom".

**destinationLocation** location  
This element captures the location determined to be the "destination" for this tax detail based on the locations associated with this line. One of "POS", "ShipTo", "POO", "BillingLocation", "CallReceived", "ServiceRendered", "FirstUse"	"ShipTo".
