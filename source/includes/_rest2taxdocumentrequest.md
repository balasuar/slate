## Tax Document Request
### header
```json
{
    "header": {
        "accountId": "2ead98c1-ecbf-4708-8d86-b01af8bc13e5",
        "companyCode": "MyCo2",
        "transactionType": "Sale",
        "documentCode": "#12345",
        "vendorCode": "VENDOR",
        "currency": "USD",
        "customerCode": "FishermansWharf",
        "transactionDate": "2014-11-11",
        "purchaseOrderNumber": "32323",
        "metadata": {
            "Ref1": "ABC",
            "Ref2": "DEF"
        },
        "defaultLocations": {
            "ShipTo": {
                "address": {
                    "line1": "2601 West Marina Place",
                    "line2": "",
                    "line3": "",
                    "city": "Seattle",
                    "state": "WA",
                    "zipcode": "98199",
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
            "itemCode": "CK0001",
            "numberOfItems": 500,
            "lineAmount": 2500,
            "itemDescription": "Personalized 8oz coke bottle",
            "taxIncluded": "false",
            "metadata": {
                "Ref1": "ABC",
                "Ref2": "DEF"
            }
        },
        {
            "lineCode": "2",
            "locations": {
                "ShipTo": {
                    "address": {
                        "line1": "611 Avenida Victoria",
                        "line2": "",
                        "line3": "",
                        "city": "San Clemente",
                        "state": "CA",
                        "zipcode": "92672",
                        "country": "USA"
                    }
                }
            }
            "itemCode": "CK0001",
            "numberOfItems": 100,
            "lineAmount": 500,
            "itemDescription": "Personalized 8oz coke bottle",
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

**accountId:** string, *required*  
This string is a UUID issued by Avalara to identify the Avalara account that owns the company identified by the companyCode.

**companyCode:** string, *required*  
Identifies the company profile/legal entity with which the calculation is associated. This is set when the company is created in the AvaTax system, and is an original parameter of the `POST /calculations` call used to create the calculation record. It is unique within the context of an Account.

**transactionType:** string, *required*  
Indicates the type of transaction. Must be one of "Sale", "Purchase" or "Transfer", as identified on the original `POST /calculations` call used to create the calculation record.

**documentCode:** string, *required*  
Typically an invoice number, receipt number, returned merchandise authorization number, etc. maintained by the client application to uniquely identify the transaction. Determined by the value passed on the original `POST /calculations` call used to create the calculation record.

**customerCode** string, *required*  
A unique identifier of the transactee determined and maintained by the client application. For a sale, this would uniquely identify the customer.

**vendorCode** string, *required*  
Alias of customerCode, offered to improve readability on Purchase Invoice type transactions. A unique identifier of the transactee determined and maintained by the client application. For a purchase, this would uniquely identify the vendor.

**transactionDate** string: date in ISO 8601 format, *required*  
The reporting date of the transaction. Note that this may differ from the date the transaction is recorded and/or the date the effective tax date of the calculation.

**currency:** string: currency in ISO 4217:2008 format, *optional*  
Not currently supported.

**totalTaxOverrideAmount:** decimal, *optional*
Not currently supported. An optional input tax amount to override the total tax amount calculated for the document. This may be used for imported transactions, returns, and layaways where the tax has already been calculated (either by AvaTax or by an external system). If provided at the TaxDocument.header level, this amount is pro rated across all taxable line items. To specify a tax override amount at the individual line level, see line.taxOverrideAmount.

**taxCalculationDate:** string: date in ISO 8601 format, *optional*  
The date that should be used to determine the appropriate tax rates, rules, and jurisdictions, independent of transaction's reporting date. If not provided, this will default to the transactionDate. Useful for layaways, credit memos, and other deferred transactions.

**defaultAvalaraGoodsAndServicesModifierType:** string, *optional*  
Not currently supported. The default product subcategory (goods and services modifier) to be used for all lines that do not override this value. The Avalara goods and services type determines the specific type of goods or services associated with a particular line in the transaction. The Avalara goods and services modifier determines variations on the goods and services type. For example, if the goods were a type of food, the modifier might be "dine in" or "take out". If the goods and services were a "bicycle" the modifier might be "rental" versus "title".

**defaultLocations:** dictionary of locations, *required, unless specified at the line level*  
This element contains a dictionary of locations such as the origin and destination addresses to be associated with this transaction. These locations may be overridden within each line item. The key for each location in the dictionary is the location "purpose". Valid locations purposes are "ShipFrom", "ShipTo", "POS", "POM", "POO", "BillingLocation", "CallPlaced", "CallReceived", "ServiceRendered", "POA" and "FirstUse". There can only be one location of a given purpose in the dictionary.

**defaultTaxPayerCode:** string, *optional*  
Not currently supported. An identifier issued by a tax authority that identifies the transacting party (typically the customer associated with the customerCodefiled) as tax exempt for this transaction type. If set, will apply to all lines in this transaction that do not override it.

**defaultBuyerType:** string, *optional*  
The type of buyer. Used to apply particular customer group taxability behavior. If set, will apply to all lines in the transaction that do not override it. Valid values are:

- A - Federal Government
- B - State/Local Govt.
- C - Tribal Government
- D - Foreign Diplomat
- E - Charitable Organization
- F - Religious/Education
- L - Other
- N - Local Government
- R - Non-resident (Canada)

**defaultUseType:** string, *optional*  
The type of use. Used to apply particular use type taxability behavior. If set, will apply to all lines in the transaction that do not override it. Valid values are:

- G - Resale
- H - Agricultural Production
- I - Industrial Prod/Mfg.
- J - Direct Pay Permit
- K - Direct Mail
- L - Other
- P - Commercial Aquaculture (Canada)
- Q - Commercial Fishery (Canada)


**purchaseOrderNumber:** string, *optional*  
A purchase order number which might be used to look up a single use tax exemption certification

**metadata** metadataItem, *optional*  
A collection of MetadataItems (string pairs) which exists to allow callers of the API to set arbitrary information that will be returned in the tax calculation response and which can be used during reporting.

### line
**lineCode** string, *required*  
A unique identifier for this line in the transaction.

**itemCode** string, *optional*  
A code maintained by the client application to uniquely identify a product or service. Usually SKU or similar. Required for SST states.

**avalaraGoodsAndServicesType** string, *optional*  
Identifies a category of products for tax purposes. It will likely be one of Avalara's standard avalaraGoodsAndServicesTypes, but may be a custom type configured in the Customer Portal. If not specified, itemCode to avalaraGoodsAndServicesType mapping will happen during tax calculation. Currently only "P0000000" (Tangible Personal Property) is supported.

**avalaraGoodsAndServicesModifierType** string, *optional*  
Not currently supported. A goods and services modifier to be used for this line. The Avalara goods and services type determines the specific type of goods or services associated with a particular line in the transaction. The Avalara goods and services modifier determines variations on the goods and services type. For example, if the goods were a type of food, the modifier might be "dine in" or "take out". If the goods and services were a "bicycle" the modifier might be "rental" versus "title".

**numberOfItems** decimal, *optional*  
The number of individual units represented by this line. Digits after the decimal point are optional.

**lineAmount** decimal, *required*  
The total cost of this line. In its simplest form lineAmount = unit price * numberOfItems.

**itemDescription** string, *optional*  
Description of the item represented by this line

**unitOfMeasure** string, *optional*  
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

**taxPayerCode** string, *optional*  
Not currently supported. a code issued by a tax authority to identify a party (typically the customer associated with the customerId field) that is exempt from tax for this type of transaction. This value will override any value set at the transaction level.

**buyerType:** string, *optional*  
The type of buyer. Used to apply particular customer group taxability behavior. If set, will apply to this line only, and will override any defaultBuyerType. Valid values are:

- A - Federal Government
- B - State/Local Govt.
- C - Tribal Government
- D - Foreign Diplomat
- E - Charitable Organization
- F - Religious/Education
- L - Other
- N - Local Government
- R - Non-resident (Canada)

**useType:** string, *optional*  
The type of use. Used to apply particular use type taxability behavior. If set, will apply to this line only, and will override any defaultUseType. Valid values are:

- G - Resale
- H - Agricultural Production
- I - Industrial Prod/Mfg.
- J - Direct Pay Permit
- K - Direct Mail
- L - Other
- P - Commercial Aquaculture (Canada)
- Q - Commercial Fishery (Canada)

**taxOverrideAmount** decimal, *optional*  
Not currently supported. A Tax Override Amount which overrides the tax for the line. This may used for imported transactions, returns, and layaways where the tax has already been calculated either by AvaTax or another means.

**taxIncluded** boolean, *optional*  
Not currently supported. Indicates whether the extendedPrice includes tax or not. It must be either "true" or "false" if present.

**metadata** metadataItem, *optional*  
A collection of MetadataItems (string pairs) which exists to allow callers of the API to set arbitrary information that will be returned in the tax calculation response and which can be used during reporting

**calculatedTax** calculatedTax, *output only*  
Contains the calculated tax information for this line item. This element is created by the tax service and overwritten if it exists in a request.

### feedback
**latencyData** latencyInfo, *optional*  
The feedback element allows clients to inform Avalara of the total roundtrip latency of calls, allowing Avalara support to better understand how well we're serving our customers.

#### latencyInfo
**latency** integer, *optional*  
The latency in miliseconds for a previous call from the client perspective.

**versionId** string, *optional*  
The versionId (returned to the client in the processingInfo.versionId field) of the transaction for which latency is being passed.


### location
Locations capture the physical locations associated with a transaction, identifying each point with a locationType enumerated in the table below.
To calculate tax for a line in a transaction, the tax calculation engine may need to know about the "origin" and the "destination" of the transaction. Sometimes determining these locations is straight forward, as in the case of an item purchased in person at a retail store for immediate consumption (a single POS address would suffice to indicate the origin and destination of the transaction). Other cases are only slightly more complicated, such as when a product is purchased over the phone and shipped from a warehouse to the customer's house. In this second case, a Ship-from location would serve as the origin, and a Ship-to location would serve as the destination.
Exactly which locations are required for a given transaction depends on the context of transaction. Specifically, such things as the transactionType, avalaraGoodsAndServicesType, and applicable jurisdictions may influence what location information is required in order to calculate tax. In the case where more than one location of a given category (origin/destination) is associated with a line, the jurisdiction will determine which location is used, and this will be indicated in the calculation response. The locations can be associated at the line level or the line can inherit the location from the header.

**taxLocationPurpose** enum, *required*  
The type of location identified by the element. Each distinct type can be used as a destination or origin address depending on the sale type, as outlined in the table below:

axLocationPurpose | Category | Description
-----|-----|-----
`ShipFrom` | origin | shipping origin of the transaction or line item
`CallPlaced` | origin | point of origin of a phone call
`POM` | origin | point of manufacture of an item
`POA`| origin | point of access to an item
`Dropship` | origin | drop shipment location of an item
`POS` | origin & destination | point of sale of an item
`ShipTo` | destination | ship to location of an item
`POO` | destination | point of order origin of an item
`BillingLocation` | destination | billing location of an item
`CallReceived` | destination |  destination of a phone call
`ServiceRendered` | destination | location a service item was rendered
`FirstUse` | destination | location of first use of an item
`PointOfOrderAcceptance` | origin | point of access to an item 
`PointOfSale`     | origin & destination | point of sale of an item 
`PointOfOrderOrigin` | destination | point of order origin of an item 
`Assumed Possession` | destination | assumed location of possession of an item 


**address**	address, *optional*  
This element contains a street or shipping address. The tax calculation service will convert this to a lat/long. See address format below.

**latlong**	latlong, *optional*  
This element contains a latitude and longitude.	See latlong format below.

**locationCode** string, *optional*  
Not currently supported. The identity of a pre-configured location unique to the company.	

**IpAddress** string, *optional*  
Not currently supported. An IP address for digital distribution. This field is not currently supported.

**addressTaxPayerCode** string, *optional*  
Not currently supported. This taxPayerCode overrides any taxPayerCode that may have been specified in the header or line item if this address is determined to govern the selection of tax rules (i.e.: if the transaction is sourced to this address).

**addressBuyerType:** string, *optional*  
The type of buyer. Used to apply particular customer group taxability behavior. If set, will apply to this address only, and will override any defaultBuyerType. Valid values are:

- A - Federal Government
- B - State/Local Govt.
- C - Tribal Government
- D - Foreign Diplomat
- E - Charitable Organization
- F - Religious/Education
- L - Other
- N - Local Government
- R - Non-resident (Canada)

**addressUseType:** string, *optional*
The type of use. Used to apply particular use type taxability behavior. If set, will apply to this address only, and will override any defaultUseType. Valid values are:

- G - Resale
- H - Agricultural Production
- I - Industrial Prod/Mfg.
- J - Direct Pay Permit
- K - Direct Mail
- L - Other
- P - Commercial Aquaculture (Canada)
- Q - Commercial Fishery (Canada)

#### latlong

**latitude** decimal, *required*  
The latitude of the transaction

**longitude** decimal, *required*  
The longitude of the transaction

#### address

**line1** string *required*  
The first line of the address.

**line2** string *optional*  
The second line of the address.

**line3** string *optional*  
The third line of the address.

**city, municipality, town** string *optional*  
The city of the address. Synonyms are provided to allow for regional terminology, but only one of the three should be included in a given location.

**state, province** string *optional*  
The state of the address. Synonyms are provided to allow for regional terminology, but only one of the two should be included in a given location.

**country** string *required*  
The country code in ISO 3166-1 alpha-2 or alpha-3 format.

**zipcode, postalCode, postCode** string *required*  
The zip code of the address. Synonyms are provided to allow for regional terminology, but only one of the three should be included in a given location.

### metadataItem

Each MetadataItem in the list is a name / value pair, which can be used in reporting and for reference information.
For example:
`"customerRef":"12345",`
`"comment":"this was done to compensate for a previous customer satisfaction issue",`
`"PurchaseOrder":"PO1232", "SalesPersonCode":"21123"`