### ProcessTransactionsResponse_5_18_0

**ProcessTransactions_5_18_0Response:** TransactionResultSummary_5_18_0, *optional*

Container to hold the results of the call to ProcessTransactions_5_18_0

**TransactionResult_5_18_0Response:** TransactionResult_5_18_0, *optional*

Container object that defines the result of a single transaction


#### TRANSACTIONRESULTSUMMARY_5_18_0

**NumberProcessed** int[10], *required*

Number of transactions processed during the call to ProcessTransactions_5_18_0

**NumberSuccess** int[10], *required*

Number of transactions processed that did not contain errors and returned a valid result

**NumberFailed** int[10], *required*

Number of transactions processed that did contain errors

**TransactionResults** **ArrayOfTransactionResult_5_18_0**, *optional*

An array of actual transaction results returned from the call to ProcessTransactions_2_0


#### TRANSACTIONRESULT_5_18_0 FIELDS 

**UserTranId** string[50], *optional*

A unique Id for the transaction as defined by the calling application which was passed in by the calling application in the Transaction_5_18_0 object

**TranId** int[10], *required*

Unique Id assigned to the Transaction by the Avalara AvaTax Excise application

**Status** string[20], *optional*

String defining the status of the transaction in the Tax Determination System

**ReturnCode** int[10], *required*

A numeric representation of the success or failure of the transaction

**TotalTaxAmount** decimal[28,6], *required*

Sum of all taxes on all line items and on the invoice itself

**TransactionTaxes** **ArrayofTransactionTax_5_18_0**, *optional*

Object defining the individual taxes returned from the transaction

**TrasactionErrors** **ArrayOfTransactionError_5_18_0**, *optional*

Object defining the individual errors returned from the transaction

**UserReturnValue** string[512], *optional*

String that returns the UserData field passed into the Transactions_5_18_0 object

---

**TransactionTax_5_18_0Response:** **TransactionTax_5_18_0**, *optional*

Container object that defines the result of a single transaction


**---TRANSACTIONTAX_5_18_0 FIELDS---:** 

**SequenceId** int[10], *required*

Avalara AvaTax Excise application calculated value that uniquely identifies the tax item within the transaction results 1, 2, 3

**TransactionLine** int[10], *optional*

The Transaction Line number passed in from the customer in the TransactionLine_2_0 object   1, 2, 3

**InvoiceLine** int[10], *optional*

The numeric invoice line passed in the calling application  1, 2, 3

**CountryCode** string[3], *optional*

3 Character ISO country code    USA, CAN

**Jurisdiction** string[10], *optional*

2 Character code for the taxing jurisdiction    ID, US, TX

**LocalJurisdiction** string[30], *optional*

GNIS standard name for a local jurisdiction such as a city or county.  If a tax is not a result of a local jurisdiction it’s set to NONE    Boise, NONE, Ada

*ProductCategory** decimal[2], *required*

Numeric representation of the type of fuel being taxed defined in the product_categories table in the Avalara AvaTax Excise application 1, 4, 22

**TaxingLevel** string[20], *optional*

Government level of taxation for the current tax item from the rates table in the Avalara AvaTax Excise application FEDERAL, STATE, LOCAL

**TaxType** string[30], *optional*

Type of tax for the current tax item from the rates table in the Avalara AvaTax Excise application  FUEL, SALESUSE

**RateType** string[30], *optional*

Type of rate for the current tax item from the rates table in the Avalara AvaTax Excise application TAX, FEE

**RateSubtype** string[30], *optional*

Further definition of the rate for the current tax item from the rates table in the Avalara AvaTax Excise application   NONE, REFUND, HIGH

**CalculationTypeInd**  string[1], *optional*

Type of calculation for the rate as defined in the rates table in the Avalara AvaTax Excise application C (currency per unit), P (percentage), F (fixed)

**TaxRate** decimal[28,6], *optional*

The tax rate for the current tax item   .025, .05

**TaxQuantity** decimal[28,6], *optional*

Number of units of product being taxed in this tax item 100, 4000, 3214

**TaxAmount** decimal[28,6], *optional*

Calculated tax amount for the tax line  2.50, 50.00

**TaxExemptionInd**  string[1], *optional*

Indication of whether a tax is exempt or not    Y, N

**DeferredInd**  string[1], *optional*

Indication of whether a tax is deferred or not  Y, N

**PayableToCode** string[50], *optional*

  (eg, R,S)

**SalesTaxBaseAmount**   decimal[28,6], *optional*

Amount of Sales tax for the current tax item    234.00, 554.00

**LicenseNumber**  string[40], *optional*

 The tax jurisdiction license number that applies for this transaction.  200984235, 894234567

**UserReturnedValue**  string[512], *optional*

String to hold any data you may want to pass into a transaction and potentially receive back untouched.  May also be used for customizing calculations based on business rules  

**ScenarioId** int[10], *optional*

A definition of the scenario that was applied in this tax item  100123, 119123

**ScenarioTaxGroupId** int[10], *optional*

A definition of the scenario tax group that was applied in this tax item    8245,321

**ScenarioSequence** int[10], *optional*

Sequence Id of the scenario_taxes table record used for this tax item   1, 2, 3, 4

**Rate Description** string[256], *optional*

A short text description (pulled from the comments field of the rate table) of the rate that is being applied with this tax item    Texas Delivery Fee

**Currency** string[10], *optional*

Type of Currency the line item Unit Price and Tax Amount are defined in USD, EUR, GBP

**Unit of Measure** string[10], *optional*

The Unit of Measure the tax quantity isdefined in   BRL, GAL, LTR 

**SubtotalInd** string[2], *optional*

Indication of which field(s) to use for the sales tax base of the tax.  (Freight Only, Unit Price Only, Combined).  C, F, U

**TransactionTaxAmounts** **ArrayOfTransactionTaxAmount_5_18_0**, *optional*

An Array of Tax Amounts in requested Currencies N/A

**StatusCode** string[30], *optional*

The calculation status of the tax.  ACTIVE, INACTIVE, EXCLUDED

**QuantityInd** string[1], *optional*

Type of Quantity used to calculate the tax referencing Billed, Net or Gross Value   B, N, G

**ReportingTaxAmount** decimal[28,6]

Tax Amount Converted to the Reporting Currency specified on the header  0.82, 2.90

**ReportingTaxCurrency** string[10], *optional*

Currency requested in the reporting currency field on the header    USD, EUR, GBP

---

**ArrayOfTransactionTaxAmount_5_18_0:** **TransactionTaxAmount_5_18_0**, *optional*

Container object that defines tax amounts in requested currencies

**---TRANSACTIONTAXAMOUNT_5_18_0 FIELDS---:** 

**SequenceId** int[10], *required*

Ordinal id for the Tax Amount

**Currency** string[10], *optional*

Currency type of the tax amount

**TaxAmount** decimal[28,6], *required*

Amount of tax in the defined currency

---

**ArrayOfTransactionError_5_18_0:** **TransactionError_5_18_0**, *optional*

Container object that defines an error for a transaction

#### TRANSACTIONERROR_5_18_0 FIELDS 

**SequenceId** int[10], *required*

Ordinal id for the error    1, 2, 3

**ErrorCode** string[10], *optional*

Numeric code representing an error in the Avalara AvaTax Excise application.    -890,  -892

**ErrorMessage** string[2000], *optional*

String description of the error Rate for CountryCode: USA,Jurisdiction: ID,LocalJurisdiction: NONE,EffectiveDate: 3/27/2009 12:00:00 AM TaxingLevel: STATE TaxType: SALESUSE RateType: TAX,RateSubtype: NONE,ProductCategory: 0 was not found.

**ErrorLevelInd** string[1], *optional*

Text describing the severity of the error.  C - Critical, W - Warning
