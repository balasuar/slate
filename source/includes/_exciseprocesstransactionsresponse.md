### ProcessTransactions Response

**ProcessTransactions_5_18_0Response:** TransactionResultSummary_5_18_0, *optional*  
Container to hold the results of the call to ProcessTransactions_5_18_0

**TransactionResult_5_18_0Response:** TransactionResult_5_18_0, *optional*  
Container object that defines the result of a single transaction

#### TransactionResultSummary_5_18_0

**NumberProcessed** int[10], *required*  
Number of transactions processed during the call to ProcessTransactions_5_18_0

**NumberSuccess** int[10], *required*  
Number of transactions processed that did not contain errors and returned a valid result

**NumberFailed** int[10], *required*  
Number of transactions processed that did contain errors

**TransactionResults** <a href='#transactionresult_5_18_0'>TransactionResult_5_18_0[]</a>, *optional*  
An array of actual transaction results returned from the call to ProcessTransactions_5_18_0


#### TransactionResult_5_18_0

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <soap:Body>
        <ProcessTransactions_5_18_0Response xmlns="http://taxes.services.fuelquest.com/">
            <ProcessTransactions_5_18_0Result>
                <TransactionResults>
                    <TransactionResult_5_18_0>
                        <UserTranId />
                        <TranId>2988728</TranId>
                        <Status>Success</Status>
                        <ReturnCode>0</ReturnCode>
                        <TotalTaxAmount>4726.33</TotalTaxAmount>
```

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

**TransactionTaxes** <a href='#transactiontax_5_18_0'>TransactionTax_5_18_0[]</a>, *optional*  
Object defining the individual taxes returned from the transaction

**TrasactionErrors** <a href='#transactionerror_5_18_0'>TransactionError_5_18_0[]</a>, *optional*  
Object defining the individual errors returned from the transaction

**UserReturnValue** string[512], *optional*  
String that returns the UserData field passed into the Transactions_5_18_0 object

#### TransactionTax_5_18_0 

```xml
                        <TransactionTaxes>
                            <TransactionTax_5_18_0>
                                <TransactionTaxAmounts />
                                <SequenceId>1</SequenceId>
                                <TransactionLine>1</TransactionLine>
                                <InvoiceLine>1</InvoiceLine>
                                <CountryCode>USA</CountryCode>
                                <Jurisdiction>US</Jurisdiction>
                                <LocalJurisdiction>NONE</LocalJurisdiction>
                                <ProductCategory>1</ProductCategory>
                                <TaxingLevel>FEDERAL</TaxingLevel>
                                <TaxType>FUEL</TaxType>
                                <RateType>TAX</RateType>
                                <RateSubtype>NONE</RateSubtype>
                                <CalculationTypeInd>C</CalculationTypeInd>
                                <TaxRate>0.1840000000</TaxRate>
                                <TaxQuantity>7743</TaxQuantity>
                                <TaxAmount>1424.71</TaxAmount>
                                <TaxExemptionInd>N</TaxExemptionInd>
                                <DeferredInd>N</DeferredInd>
                                <SalesTaxBaseAmount>0</SalesTaxBaseAmount>
                                <LicenseNumber />
                                <UserReturnedValue />
                                <ScenarioId>199375</ScenarioId>
                                <ScenarioTaxGroupId>1279</ScenarioTaxGroupId>
                                <ScenarioSequence>1</ScenarioSequence>
                                <RateDescription>Federal Excise Tax - Gasoline</RateDescription>
                                <Currency>USD</Currency>
                                <UnitOfMeasure>GLL</UnitOfMeasure>
                                <SubtotalInd>U</SubtotalInd>
                                <StatusCode>ACTIVE</StatusCode>
                                <QuantityInd>B</QuantityInd>
                                <ReportingTaxAmount xsi:nil="true" />
                            </TransactionTax_5_18_0>
                            <TransactionTax_5_18_0>
                                <TransactionTaxAmounts />
                                <SequenceId>2</SequenceId>
                                <TransactionLine>1</TransactionLine>
                                <InvoiceLine>1</InvoiceLine>
                                <CountryCode>USA</CountryCode>
                                <Jurisdiction>IL</Jurisdiction>
                                <LocalJurisdiction>NONE</LocalJurisdiction>
                                <ProductCategory>1</ProductCategory>
                                <TaxingLevel>STATE</TaxingLevel>
                                <TaxType>FUEL</TaxType>
                                <RateType>TAX</RateType>
                                <RateSubtype>NONE</RateSubtype>
                                <CalculationTypeInd>C</CalculationTypeInd>
                                <TaxRate>0.1900000000</TaxRate>
                                <TaxQuantity>7743</TaxQuantity>
                                <TaxAmount>1471.17</TaxAmount>
                                <TaxExemptionInd>N</TaxExemptionInd>
                                <DeferredInd>N</DeferredInd>
                                <SalesTaxBaseAmount>0</SalesTaxBaseAmount>
                                <LicenseNumber />
                                <UserReturnedValue />
                                <ScenarioId>2904</ScenarioId>
                                <ScenarioTaxGroupId>435</ScenarioTaxGroupId>
                                <ScenarioSequence>1</ScenarioSequence>
                                <RateDescription>Illinois State Gasoline Tax</RateDescription>
                                <Currency>USD</Currency>
                                <UnitOfMeasure>GLL</UnitOfMeasure>
                                <SubtotalInd>U</SubtotalInd>
                                <StatusCode>ACTIVE</StatusCode>
                                <QuantityInd>B</QuantityInd>
                                <ReportingTaxAmount xsi:nil="true" />
                            </TransactionTax_5_18_0>
                            <TransactionTax_5_18_0>
                                <TransactionTaxAmounts />
                                <SequenceId>10</SequenceId>
                                <TransactionLine>2</TransactionLine>
                                <InvoiceLine>2</InvoiceLine>
                                <CountryCode>USA</CountryCode>
                                <Jurisdiction>MO</Jurisdiction>
                                <LocalJurisdiction>PHELPS</LocalJurisdiction>
                                <ProductCategory>0</ProductCategory>
                                <TaxingLevel>COUNTY</TaxingLevel>
                                <TaxType>SALESUSE</TaxType>
                                <RateType>TAX</RateType>
                                <RateSubtype>NONE</RateSubtype>
                                <CalculationTypeInd>P</CalculationTypeInd>
                                <TaxRate>0.0087500000</TaxRate>
                                <TaxQuantity>860</TaxQuantity>
                                <TaxAmount>23.36</TaxAmount>
                                <TaxExemptionInd>N</TaxExemptionInd>
                                <DeferredInd>N</DeferredInd>
                                <SalesTaxBaseAmount>2669.44</SalesTaxBaseAmount>
                                <LicenseNumber />
                                <UserReturnedValue />
                                <ScenarioId>38724</ScenarioId>
                                <ScenarioTaxGroupId>727</ScenarioTaxGroupId>
                                <ScenarioSequence>2</ScenarioSequence>
                                <RateDescription>Phelps Co. MO Sales/Use Tax</RateDescription>
                                <Currency>USD</Currency>
                                <UnitOfMeasure>GLL</UnitOfMeasure>
                                <SubtotalInd>U</SubtotalInd>
                                <StatusCode>ACTIVE</StatusCode>
                                <QuantityInd>B</QuantityInd>
                                <ReportingTaxAmount xsi:nil="true" />
                            </TransactionTax_5_18_0>
                            <TransactionTax_5_18_0>
                                <TransactionTaxAmounts />
                                <SequenceId>11</SequenceId>
                                <TransactionLine>2</TransactionLine>
                                <InvoiceLine>2</InvoiceLine>
                                <CountryCode>USA</CountryCode>
                                <Jurisdiction>MO</Jurisdiction>
                                <LocalJurisdiction>ROLLA</LocalJurisdiction>
                                <ProductCategory>0</ProductCategory>
                                <TaxingLevel>CITY</TaxingLevel>
                                <TaxType>SALESUSE</TaxType>
                                <RateType>TAX</RateType>
                                <RateSubtype>NONE</RateSubtype>
                                <CalculationTypeInd>P</CalculationTypeInd>
                                <TaxRate>0.0000000000</TaxRate>
                                <TaxQuantity>860</TaxQuantity>
                                <TaxAmount>0.00</TaxAmount>
                                <TaxExemptionInd>N</TaxExemptionInd>
                                <DeferredInd>N</DeferredInd>
                                <SalesTaxBaseAmount>2669.44</SalesTaxBaseAmount>
                                <LicenseNumber />
                                <UserReturnedValue />
                                <ScenarioId>38724</ScenarioId>
                                <ScenarioTaxGroupId>727</ScenarioTaxGroupId>
                                <ScenarioSequence>5</ScenarioSequence>
                                <RateDescription>Rolla MO City Sales/Use Tax</RateDescription>
                                <Currency>USD</Currency>
                                <UnitOfMeasure>GLL</UnitOfMeasure>
                                <SubtotalInd>U</SubtotalInd>
                                <StatusCode>ACTIVE</StatusCode>
                                <QuantityInd>B</QuantityInd>
                                <ReportingTaxAmount xsi:nil="true" />
                            </TransactionTax_5_18_0>
                        </TransactionTaxes>
```

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

**TransactionTaxAmounts** <a href='#transactiontaxamount_5_18_0'>TransactionTaxAmount_5_18_0[]</a>, *optional*  
An Array of Tax Amounts in requested Currencies N/A

**StatusCode** string[30], *optional*  
The calculation status of the tax.  ACTIVE, INACTIVE, EXCLUDED

**QuantityInd** string[1], *optional*  
Type of Quantity used to calculate the tax referencing Billed, Net or Gross Value   B, N, G

**ReportingTaxAmount** decimal[28,6]  
Tax Amount Converted to the Reporting Currency specified on the header  0.82, 2.90

**ReportingTaxCurrency** string[10], *optional*  
Currency requested in the reporting currency field on the header    USD, EUR, GBP

#### TransactionTaxAmount_5_18_0

**SequenceId** int[10], *required*  
Ordinal id for the Tax Amount

**Currency** string[10], *optional*  
Currency type of the tax amount

**TaxAmount** decimal[28,6], *required*  
Amount of tax in the defined currency

#### TransactionError_5_18_0

```xml
                        <TransactionErrors>
                            <TransactionError_5_18_0>
                                <SequenceId>1</SequenceId>
                                <ErrorCode>-897</ErrorCode>
                                <ErrorMessage>Buyer "1" does not exist or is not active for 1/11/2014.</ErrorMessage>
                                <ErrorLevelInd>Warning</ErrorLevelInd>
                            </TransactionError_5_18_0>
                            <TransactionError_5_18_0>
                                <SequenceId>2</SequenceId>
                                <ErrorCode>-898</ErrorCode>
                                <ErrorMessage>Seller "4375601" does not exist or is not active for 1/11/2014.</ErrorMessage>
                                <ErrorLevelInd>Warning</ErrorLevelInd>
                            </TransactionError_5_18_0>
                            <TransactionError_5_18_0>
                                <SequenceId>3</SequenceId>
                                <ErrorCode>-891</ErrorCode>
                                <ErrorMessage>LASALLE is not a valid county in IL, USA.  Please update the Destination on transaction line 1.</ErrorMessage>
                                <ErrorLevelInd>Warning</ErrorLevelInd>
                            </TransactionError_5_18_0>
                            <TransactionError_5_18_0>
                                <SequenceId>4</SequenceId>
                                <ErrorCode>-881</ErrorCode>
                                <ErrorMessage>No county was provided on the Sale Location for transaction line 1.</ErrorMessage>
                                <ErrorLevelInd>Warning</ErrorLevelInd>
                            </TransactionError_5_18_0>
                            <TransactionError_5_18_0>
                                <SequenceId>5</SequenceId>
                                <ErrorCode>-880</ErrorCode>
                                <ErrorMessage>No city was provided on the Sale Location for transaction line 1.</ErrorMessage>
                                <ErrorLevelInd>Warning</ErrorLevelInd>
                            </TransactionError_5_18_0>
                        </TransactionErrors>
                        <UserReturnValue />
                    </TransactionResult_5_18_0>
                </TransactionResults>
                <NumberProcessed>1</NumberProcessed>
                <NumberSuccess>1</NumberSuccess>
                <NumberFailed>0</NumberFailed>
            </ProcessTransactions_5_18_0Result>
        </ProcessTransactions_5_18_0Response>
    </soap:Body>
</soap:Envelope>
```

**SequenceId** int[10], *required*  
Ordinal id for the error    1, 2, 3

**ErrorCode** string[10], *optional*  
Numeric code representing an error in the Avalara AvaTax Excise application.    -890,  -892

**ErrorMessage** string[2000], *optional*  
String description of the error Rate for CountryCode: USA,Jurisdiction: ID,LocalJurisdiction: NONE,EffectiveDate: 3/27/2009 12:00:00 AM TaxingLevel: STATE TaxType: SALESUSE RateType: TAX,RateSubtype: NONE,ProductCategory: 0 was not found.

**ErrorLevelInd** string[1], *optional*  
Text describing the severity of the error.  C - Critical, W - Warning