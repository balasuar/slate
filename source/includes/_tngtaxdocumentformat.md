## TaxDocument Format
### header
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

**currencyCode:** string: currency in ISO 4217:2008 format, *optional*  
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

**purchaseOrderNumber:** string, *optional*  
A purchase order number which might be used to look up a single use tax exemption certification

**metadata** metadataItem, *optional*
A collection of MetadataItems (string pairs) which exists to allow callers of the API to set arbitrary information that will be returned in the tax calculation response and which can be used during reporting

### line
### calculatedTax
### processingInfo
### feedback
### LatencyInfo
### Location
### Location Content
### LatLong
### Address
### MetadataItem
### calculatedTax
#### taxAuthorities
##### details
