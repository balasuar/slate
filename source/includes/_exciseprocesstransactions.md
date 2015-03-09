## ProcessTransactions

### ProcessTransactionsRequest

The ProcessTransactions method uses an array of Transactions to calculate taxes based on scenarios predefined in the Avalara AvaTax Excise application.

**Transactions:** ArrayOfTransaction_5_18_0, *optional*  
Container object to hold an array of Transaction_5_18_0

#### Transaction_5_18_0

```csharp

TaxDetermination taxDetermination = new TaxDetermination();
Transaction_5_18_0[] transactions = new Transaction_5_18_0[1];
Transaction_5_18_0 transactions_0 = new Transaction_5_18_0();
transactions_0.Company = "Determination Company";
transactions_0.EffectiveDate = new DateTime(2014, 2, 11);
transactions_0.InvoiceNumber = "";
transactions_0.InvoiceDate = new DateTime(2014, 2, 11);
transactions_0.FuelUseCode = "";
transactions_0.TransactionType = "BELOW";
transactions_0.TransportationModeCode = "";
transactions_0.TitleTransferCode = "ORIG";
transactions_0.Seller = "";
transactions_0.Buyer = "";
transactions_0.PreviousSeller = "";
transactions_0.NextBuyer = "";
transactions_0. SellerVatNumber = "";
transactions_0. BuyerVatNumber = "";
transactions_0. CustomsStatus = "";
transactions_0. FormAPresentedInd = "";
transactions_0. SimplifiedProcedureInd = "";
transactions_0. Incoterms = "";
transactions_0.UserData = "UserDataINV";
transactions_0.UserTranId = "TRN9001";
transactions_0.SourceSystem = "home";
transactions_0.SaveTransactionInd = "Y";
transactions_0.DebugInd = "N";
transactions_0.CalculationMethod = "NORMAL";
transactions_0.TotalDyedUnits = 1000;
TransactionLine_5_18_0[] transactionLines = new TransactionLine_5_18_0[1];
TransactionLine_5_18_0 transactionLines_0 = new TransactionLine_5_18_0();
transactionLines_0.InvoiceLine = 1000;
transactionLines_0.MovementStartDate = new DateTime(2014, 2, 11);
transactionLines_0.MovementEndDate = new DateTime(2014, 2, 11);
transactionLines_0.ProductCode = "065";
transactionLines_0.BlendToProductCode = "";
transactionLines_0.UnitPrice = 1.29;
transactionLines_0.NetUnits = 500;
transactionLines_0.GrossUnits = 500;
transactionLines_0.BilledUnits = 500;
transactionLines_0.LineAmount = null;
transactionLines_0.FreightLineAmount = null;
transactionLines_0.BillOfLadingNumber = "";
transactionLines_0.BillOfLadingDate = new DateTime(2014, 2, 11);
transactionLines_0.OriginCountryCode = "USA";
transactionLines_0.OriginJurisdiction = "WI";
transactionLines_0.OriginCounty = "Brown";
transactionLines_0.OriginCity = "Green Bay";
transactionLines_0.OriginPostalCode = "54313";
transactionLines_0.OriginType = "";
transactionLines_0.Origin = "";
transactionLines_0.OriginOutCityLimitInd = "";
transactionLines_0.OriginExciseWarehouse = "";
transactionLines_0.OriginSpecialJurisdictionInd = "Y";
transactionLines_0.DestinationCountryCode = "USA";
transactionLines_0.DestinationJurisdiction = "WI";
transactionLines_0.DestinationCounty = "Brown";
transactionLines_0.DestinationCity = "Green Bay";
transactionLines_0.DestinationPostalCode = "54313";
transactionLines_0.DestinationType = "";
transactionLines_0.Destination = "";
transactionLines_0.DestinationOutCityLimitInd = "";
transactionLines_0.DestinationSpecialJurisdictionInd = "N";
transactionLines_0.DestinationExciseWarehouse = "";
transactionLines_0.SaleCountryCode = "USA";
transactionLines_0.SaleJurisdiction = "WI";
transactionLines_0.SaleCounty = "Brown";
transactionLines_0.SaleCity = "Green Bay";
transactionLines_0.SalePostalCode = "54313";
transactionLines_0.SaleType = "";
transactionLines_0.SaleLocation = "";
transactionLines_0.SaleOutCityLimitInd = "";
transactionLines_0.SaleExciseWarehouse = "";
transactionLines_0.SaleSpecialJurisdictionInd = "N";
transactionLines_0.CounterCountryCode = "USA";
transactionLines_0.CounterJurisdiction = "WI";
transactionLines_0.CounterCounty = "Brown";
transactionLines_0.CounterCity = "Green Bay";
transactionLines_0.CounterPostalCode = "54313";
transactionLines_0.CounterType = "";
transactionLines_0.Counter = "";
transactionLines_0.CounterOutCityLimitInd = "";
transactionLines_0.CounterExciseWarehouse = "";
transactionLines_0.CounterSpecialJurisdictionInd = "N";
transactionLines_0.CounterFiscalRepInd = "N";

transactionLines_0.UserData = "UserData0";
transactionLines_0.AlternativeFuelContent = null;
transactionLines_0.BlendToAltFuelContent = null;
transactionLines_0.BlendToInd = "";
transactionLines_0.FreightUnitPrice = 0.0625;
transactionLines_0.FreightType = "NON_ITEMIZED_COMMON_CARRIER";

TransactionLineJurisdiction_5_18_0 transactionLineOrigin_0 = new TransactionLineJurisdiction_5_18_0();
transactionLineOrigin_0.SpecialJurisdictionCode = "SPD1-BROWN";
transactionLineOrigin_0.SpecialJurisdictionType = "COUNTY";
transactionLines_0. OriginSpecialJurisdictions = new TransactionLineJurisdiction_5_18_0[1];
transactionLines_0. OriginSpecialJurisdictions[0] = transactionLineOrigin_0;
transactionLines[0] = transactionLines_0;
transactions_0.TransactionLines = transactionLines;
transactions[0] = transactions_0;
    
TransactionResultSummary_5_18_0 processTransactions_5_18_0Result = taxDetermination.ProcessTransactions_5_18_0(transactions);

```

```shell
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <soap:Body>
         <ProcessTransactions_5_18_0 xmlns="http://taxes.services.fuelquest.com/">
              <transactions>
                  <Transaction_5_18_0>
                     <TransactionLines>
                         <TransactionLine_5_18_0>
                             <InvoiceLine>1</InvoiceLine>
                             <MovementStartDate>2014-01-11T00:02:00</MovementStartDate>
                             <MovementEndDate>2014-01-11T00:02:00</MovementEndDate>
                             <ProductCode>065</ProductCode>
                             <BlendToProductCode>124</BlendToProductCode>
                             <UnitPrice>3.123</UnitPrice>
                             <NetUnits>7887</NetUnits>
                             <GrossUnits>7743</GrossUnits>
                             <BilledUnits>7743</BilledUnits>
                             <LineAmount>0</LineAmount>
                             <BillOfLadingNumber>6012345</BillOfLadingNumber>
                             <BillOfLadingDate>2014-01-11T00:02:00</BillOfLadingDate>
                             <OriginCountryCode>USA</OriginCountryCode>
                             <OriginJurisdiction>MO</OriginJurisdiction>
                             <OriginCounty>PHELPS</OriginCounty>
                             <OriginCity>ROLLA</OriginCity>
                             <OriginPostalCode>55113</OriginPostalCode>
                             <OriginType>TERMINAL</OriginType>
                             <OriginOutCityLimitInd>N</OriginOutCityLimitInd>
                             <OriginSpecialJurisdictionInd>N</OriginSpecialJurisdictionInd>
                             <DestinationCountryCode>USA</DestinationCountryCode>
                             <DestinationJurisdiction>IL</DestinationJurisdiction>
                             <DestinationCounty>LASALLE</DestinationCounty>
                             <DestinationCity>OTTAWA</DestinationCity>
                             <DestinationOutCityLimitInd>N</DestinationOutCityLimitInd>
                             <DestinationSpecialJurisdictionInd>N</DestinationSpecialJurisdictionInd>
                             <SaleSpecialJurisdictionInd>N</SaleSpecialJurisdictionInd>
                             <AlternativeFuelContent xsi:nil="true" />
                             <BlendToAltFuelContent xsi:nil="true" />
                             <Currency>USD</Currency>
                             <UnitOfMeasure>GLL</UnitOfMeasure>
                             <FreightUnitPrice>0</FreightUnitPrice>
                             <FreightType>NONE</FreightType>
                             <FreightLineAmount>0</FreightLineAmount>
                             <CustomNumeric1 xsi:nil="true" />
                             <CustomNumeric2 xsi:nil="true" />
                             <CustomNumeric3 xsi:nil="true" />
                             <NthTimeSale xsi:nil="true" />
                         </TransactionLine_5_18_0>
                         <TransactionLine_5_18_0>
                             <InvoiceLine>2</InvoiceLine>
                             <MovementStartDate>2014-01-11T00:02:00</MovementStartDate>
                             <MovementEndDate>2014-01-11T00:02:00</MovementEndDate>
                             <ProductCode>227</ProductCode>
                             <BlendToProductCode>B10</BlendToProductCode>
                             <UnitPrice>3.1</UnitPrice>
                             <NetUnits>860</NetUnits>
                             <GrossUnits>860</GrossUnits>
                             <BilledUnits>860</BilledUnits>
                             <LineAmount>0</LineAmount>
                             <BillOfLadingDate xsi:nil="true" />
                             <OriginCountryCode>USA</OriginCountryCode>
                             <OriginJurisdiction>MO</OriginJurisdiction>
                             <OriginCounty>PHELPS</OriginCounty>
                             <OriginCity>ROLLA</OriginCity>
                             <OriginPostalCode>55934</OriginPostalCode>
                             <OriginType />
                             <OriginOutCityLimitInd>N</OriginOutCityLimitInd>
                             <OriginSpecialJurisdictionInd>N</OriginSpecialJurisdictionInd>
                             <DestinationCountryCode>USA</DestinationCountryCode>
                             <DestinationJurisdiction>MO</DestinationJurisdiction>
                             <DestinationCounty>BOONE</DestinationCounty>
                             <DestinationCity>COLUMBIA</DestinationCity>
                             <DestinationOutCityLimitInd>N</DestinationOutCityLimitInd>
                             <DestinationSpecialJurisdictionInd>N</DestinationSpecialJurisdictionInd>
                             <SaleSpecialJurisdictionInd>N</SaleSpecialJurisdictionInd>
                             <AlternativeFuelContent xsi:nil="true" />
                             <BlendToAltFuelContent xsi:nil="true" />
                             <UnitOfMeasure>GLL</UnitOfMeasure>
                             <FreightUnitPrice>0</FreightUnitPrice>
                             <FreightType>NONE</FreightType>
                             <FreightLineAmount>0</FreightLineAmount>
                             <CustomNumeric1 xsi:nil="true" />
                             <CustomNumeric2 xsi:nil="true" />
                             <CustomNumeric3 xsi:nil="true" />
                             <NthTimeSale xsi:nil="true" />
                         </TransactionLine_5_18_0>
                     </TransactionLines>
                     <Company>rod Oil company</Company>
                     <EffectiveDate>2014-01-11T00:02:00</EffectiveDate>
                     <InvoiceDate>2014-01-11T00:02:00</InvoiceDate>
                     <InvoiceNumber>S03123456</InvoiceNumber>
                     <TitleTransferCode>DEST</TitleTransferCode>
                     <TransactionType>RACK</TransactionType>
                     <TransportationModeCode>J</TransportationModeCode>
                     <Seller>4375601</Seller>
                     <Buyer>1</Buyer>
                     <TotalDyedUnits xsi:nil="true" />
                     <TotalReportingTaxes xsi:nil="true" />
                     <SourceSystem>DEMO</SourceSystem>
                     <CustomNumeric1 xsi:nil="true" />
                     <CustomNumeric2 xsi:nil="true" />
                     <CustomNumeric3 xsi:nil="true" />
                </Transaction_5_18_0>
            </transactions>
        </ProcessTransactions_5_18_0>
    </soap:Body>
</soap:Envelope>
```

```php
# A PHP sample is not available for this resource at this time.

```

```java
// A Java sample is not available for this resource at this time.

```

**Company:** string[100], *required*  
The Name of a company that matches to the name field in the companies table within the Avalara AvaTax Excise application Control Database (eg. Determination Sample)

**EffectiveDate:** Datetime, *required*  
The date of the physical product movement (eg. 3/27/2009)

**InvoiceNumber:** string[12], *optional*  
An identifying number of the invoice to be taxed (eg. INV1011)

**InvoiceDate:** Datetime, *optional*  
The date of the invoice to be taxed (eg. 3/27/2009)

**FuelUseCode:** string[3], *optional*  
A code to describe the fuel use.  Currently not used but included for future taxation scenarios

**TransactionType:** string[20], *required*  
Type of transactions on this invoice (eg, Above, Below, Rack)

**TransportationModeCode:** string[3], *optional*  
Type of transportation mode used to transport fuel between locations (eg, J, PL, R)

**TitleTransferCode:** string[4], *required*  
Definition of where the title transfer takes place  (eg, ORIG, DEST)

**Seller:** string[35], *optional*  
Unique ID for the seller which must match the custom_id field on the business_entities table in the Avalara AvaTax Excise application client database   (eg, Sel321, 7, sel345)

**Buyer:** string[35], *optional*  
Unique ID for the buyer which must match the custom_id on the business_ entities table in the Avalara AvaTax Excise application client database (eg, Buy784, 24324, buy97887)

**PreviousSeller:** string[35], *optional*  
ID of the Previous Seller (eg, Sel321, 7, sel345)

**NextBuyer:** string[35], *optional*  
ID of the Next Buyer (eg, Buy784, 24324, buy97887)

**SellerVATNumber:** string[20], *optional*  
Seller VAT Registration Number  (eg, 1234567890123456790)

**BuyerVATNumber:** string[20], *optional*  
Buyer VAT Registration Number  (eg, 1234567890123456790)

**CustomStatus:** string[30], *optional*  
Indicates the Customs status for VAT (eg, EUY,EUN)

**FormAPresentedInd:** string[1], *optional*  
Indicates if Form A is Presented for VAT (eg, Y,N)

**SimplifiedProcedureInd:** string[1], *optional*  
Indicates if the simplified procedure is used for VAT (eg, Y,N)

**Incoterms:** string[3], *optional*  
International Chamber of Commerce (ICC) rules for the use of domestic and international trade terms (eg, EXW, FCA, FAS, FOB, CFR, CIF, CPT, CIP, DAF, DES, DEQ, DDU, DDP)

**UserData:** string[255], *optional*  
String to hold any data you may want to pass into a transaction and potentially receive back untouched.  May also be used for customizing calculations based on business rules

**UserTranId:** string[50], *optional*  
A unique Id for the transaction as defined by the calling application (eg, 678, 23823982, 32324)

**SourceSystem:** string[100], *optional*  
Hard coded string to identify which system is calling the application with this transaction.  Useful when more than a single system is using the application or to separate GUI calls from web service calls (eg, SAAS, iLynx, etc)

**CustomString1:** string[128], *optional*  
String to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.    (eg, TEST, Purple, 111)

**CustomString2:** string[128], *optional*  
String to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.    (eg, TEST, Purple, 111)

**CustomString3:** string[128], *optional*  
String to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.    (eg, TEST, Purple, 111)

**CustomNumeric1:** decimal[28,6], *optional*  
Decimal to hold data you want to pass into a transaction to be used for customizing calculations based on business rules. (eg, 100, 0.0125, 500000000)

**CustomNumeric2:** decimal[28,6], *optional*  
Decimal to hold data you want to pass into a transaction to be used for customizing calculations based on business rules. (eg, 100, 0.0125, 500000000)

**CustomNumeric3:** decimal[28,6], *optional*  
Decimal to hold data you want to pass into a transaction to be used for customizing calculations based on business rules. (eg, 100, 0.0125, 500000000)

**OrderType:** string[50], *optional*  
A code to describe the order type.  Currently not used but included for future taxation scenarios.

**TransactionLines:** <a href=#transactionline_5_18_0>TransactionLine_5_18_0[]</a>, *optional*  
An array of transaction lines which are invoice line items that contain the product and origin and destination information for a transaction

**TransactionExchangeRates:** <a href=#exchangerate_5_18_0>ExchangeRate_5_18_0[]</a>, *optional*  
An array of transaction Exchange Rates which are exchange rate definitions to be used to calculate the taxes and return tax amounts.

**SaveTransactionInd:** string[1], *optional*  
Indicates if the transaction should be saved to the database.  Not saving can have a significant performance improvement. If this value is not defined in the transaction the Saving of Transactions is controlled by the Company Setting in the GUI.  (eg, Y,N, <Not set>) 

**DebugInd:** string[1], *optional*  
Indicates if the transaction should be calculated with debugging enabled.   (eg, Y,N)

**CalculationMethod:** string[20], *optional*  
Indicates which company specific configuration should be used when calculating the transaction.     (eg, NORMAL, WITHOUT_COMPANY, PROFILES_ONLY, LICENSES_ONLY)

**TotalDyedUnits:** decimal[28,6], *optional*  
The total amount of dyed product purchased by the customer for the month of the transaction.    (eg, 100, 345.3, 4005)

**TotalReportingTaxes:** decimal[28,6], *optional*  
Sum of all resulting taxes from the reporting_tax_amount field  (eg, 2.00, 0.82)

**ReportingCurrency:** string[10], *optional*  
Currency the taxes need to be reported in which may differ from the currency of tax rate    (eg, USD, GBP, EUR)

#### TransactionLine_5_18_0

**InvoiceLine** int, *required*  
A unique identifier within the transaction for the invoice line item    (eg, 1, 2, 3)

**MovementStartDate** datetime, *optional*  
The date that the product on the line item begins to be transported from the origin (eg, 3/27/2009)

*MovementEndDate** datetime, *optional*  
The date that the product on the line item reaches its destination  (eg, 3/27/2009)

**ProductCode** string[10], *required*  
Identifying code of the product being transported in the line item which needs to match either a product code or an alternate product code in the Avalara AvaTax Excise application client database (eg, 065, E00, 241)

**BlendToProductCode** string[10], *optional*  
If used in blending the product code of the final product which needs to match a product code or an alternate product code in the Avalara AvaTax Excise application client database (eg, B10, E10)

**UnitPrice** decimal[28,6], *optional*  
The price per unit of the product   (eg, 1.37, 2.29, 44.34)

**NetUnits** decimal[28,6], *optional*  
The net units of product    (eg, 100, 345.3, 4005)

**GrossUnits** decimal[28,6], *optional*  
The gross units of product  (eg, 100, 345.3, 4005)

**BilledUnits** decimal[28,6], *optional*  
The billed units of product (eg, 100, 345.3, 4005)

**LineAmount** decimal[28,10], *optional*  
The total amount of value of product on the line item calculated by BilledUnits * UnitPrice, If left blank the Avalara AvaTax Excise application calculate  (eg, 137.00, 456.58, 5213.47)

**BillOfLadingNumber**, string[50], *optional*  
Bill of lading or Manifest number of the load   (eg, Bol4585, 100458)

**BillOfLadingDate** datetime, *optional*  
Bill of lading or Manifest Date of the load (eg, 3/27/2009)

**OriginCountryCode** string[3], *optional*  
ISO standard 3 character country code of the origin location    (eg, USA, CAN)

**OriginJurisdiction** string[10], *optional*  
State or Region code of the originating location of the load    (eg, WI, TX, ID)

**OriginCounty** string[30], *optional*  
County name of the origin location that must match a GNIS defined County name in the local_jurisdictions table of the Avalara AvaTax Excise application Client database;  or a cross reference entry in the common_codes    (eg, Brown, Ada, Marathon)

**OriginCity** string[30], *optional*  
City name of the origin location that must match a GNIS defined City name in the local_jurisdictions table of the Avalara AvaTax Excise application client database; or a cross reference entry in the common_codes (eg, Boise, Houston, Milwaukee)

**OriginPostalCode**  string[11], *optional*     
Postal Code of the origin location that is available here for information purposes only.  Not used in calculation of taxes at this time.    54126, 70012, 80013

**OriginType**  string[10], *optional*  
Type of facility that the product originates from   PIPELINE, REFINERY, TERMINAL, TRUCK

**Origin**  string[35], *optional*  
A unique id for the origin location that should match to a custom_id from the locations table in the Avalara AvaTax Excise application client database  Loc4528

**OriginOutCityLimitInd**   string[1], *optional*  
Single character that specifies if the origin location resides within or outside of the city limits Y, N

**OriginExciseWarehouse**  string[20], *optional*  
Excise Warehouse Number of the Origin   Free-form

**OriginSpecialJurisdictionInd**   string[1], *optional*  
Indicates if the origin has special jurisdictions.  Y, N

**OriginSpecialJurisdictions**   string[1], *optional*  
Array of special jurisdictions for the origin.  N/A

**DestinationCountryCode**   string[3], *optional*  
ISO standard 3 character country code of the destination location   USA, CAN

**DestinationJurisdiction**  string[10], *optional*  
State or Region code of the destination location of the load    WI, TX, ID

**DestinationCounty**  string[30], *optional*  
County name of the destination location that must match a GNIS defined County name in the local_jurisdictions table of the Avalara AvaTax Excise application Client database;  or a cross reference entry in the common_codes   Brown, Ada, Marathon

**DestinationCity**  string[30], *optional*  
City name of the destination location that must match a GNIS defined City name in the local_jurisdictions table of the Avalara AvaTax Excise application client database; or a cross reference entry in the common_codes    Boise, Houston, Milwaukee

**DestinationPostalCode**  string[11], *optional*   
Postal Code of the destination location that is available here for information purposes only.  Not used in calculation of taxes at this time.   54126, 70012, 80013

**DestinationType**  string[10], *optional*  
Type of receiving facility for the product  PIPELINE, REFINERY, TERMINAL, TRUCK

**Destination**  string[35], *optional*  
A unique id for the destination location that should match to a custom_id from the locations table in the Avalara AvaTax Excise application client database Loc4528

**DestinationOutCityLimitInd**   string[1], *optional*  
Single character that specifies if the destination location resides within or outside of the city limits    Y, N

**DestinationSpecialJurisdicitonInd**    string[1], *optional*  
Indicates if the destination has special jurisdictions. Y, N

**DestinationSpecialJurisdictions** <a href=#transactionlinejurisdiction_5_18_0>TransactionLineJurisdiction_5_18_0[]</a>, *optional*  
Array of special jurisdictions for the destination. N/A

**DestinationExciseWarehouse**  string[20], *optional*  
 Excise Warehouse Number of the Destination  Free-form

**SaleCountryCode**  string[3], *optional*  
ISO standard 3 character country code of the Sale location  USA, CAN

**SaleJurisdiction**    string[10], *optional*  
State or Region code of the Sale location of the load   WI, TX, ID

**SaleCounty**   string[30], *optional*  
County name of the Sale location that must match a GNIS defined County name in the local_jurisdictions table of the Avalara AvaTax Excise application Client database;  or a cross reference entry in the common_codes  Brown, Ada, Marathon

**SaleCity**    string[30], *optional*  
 City name of the Sale location that must match a GNIS defined City name in the local_jurisdictions table of the Avalara AvaTax Excise application client database; or a cross reference entry in the common_codes   Boise, Houston, Milwaukee

**SalePostalCode**  string[11], *optional*  
 Postal Code of the Sale location that is available here for information purposes only.  Not used in calculation of taxes at this time.  54126, 70012, 80013

**SaleType**   string[10], *optional*  
Type of receiving facility for the product  PIPELINE, REFINERY, TERMINAL, TRUCK

**SaleLocation**    string[35], *optional*  
A unique id for the Sale location that should match to a custom_id from the locations table in the Avalara AvaTax Excise application client database    Loc4528

**SaleOutCityLimitInd**  string[1], *optional*  
Single character that specifies if the Sale location resides within or outside of the city limits   Y, N

**SaleExciseWarehouse**  string[20], *optional*  
Excise Warehouse Number of the Sale Location    Free-form

**SaleSpecialJurisdictionInd**  string[1], *optional*  
Indicates if the sale locaiton has special jurisdictions.   Y, N

**SaleSpecialJurisdictions** <a href=#transactionlinejurisdictions_5_18_0>TransactionLineJurisdiction_5_18_0[]</a>, *optional*  
Array of special jurisdictions for the sale location.   N/A

**CounterCountryCode**   string[3], *optional*  
ISO standard 3 character country code of the Counter location   USA, CAN

**CounterJurisdiction**  string[10], *optional*  
State or Region code of the Counter location of the load    WI, TX, ID

**CounterCounty**    string[30], *optional*  
County name of the Counter location that must match a GNIS defined County name in the local_jurisdictions table of the Avalara AvaTax Excise application Client database;  or a cross reference entry in the common_codes   Brown, Ada, Marathon

**CounterCity**  string[30], *optional*  
City name of the Counter location that must match a GNIS defined City name in the local_jurisdictions table of the Avalara AvaTax Excise application client database; or a cross reference entry in the common_codes    Boise, Houston, Milwaukee

**CounterPostalCode**   string[11], *optional*  
 Postal Code of the Counter location that is available here for information purposes only.  Not used in calculation of taxes at this time.   54126, 70012, 80013

**CounterType**  string[10], *optional*  
Type of receiving facility for the product  PIPELINE, REFINERY, TERMINAL, TRUCK

**CounterParty**    string[35], *optional*  
 A unique id for the Counter location that should match to a custom_id from the locations table in the Avalara AvaTax Excise application client database Loc4528

**CounterOutCityLimitInd**  string[1], *optional*   
Single character that specifies if the Counter location resides within or outside of the city limits    Y, N

**CounterSpecialJurisdicitonInd**   string[1], *optional*  
 Indicates if the Counter has special jurisdictions. Y, N

**CounterExciseWarehouse**  string[20], *optional*  
 Excise Warehouse Number of the Counter  Free-form

**CounterFiscalRepInd**  string[1], *optional*  
Indicates if the Counter is a fiscal rep.   Y, N

**UserData**   string[255], *optional*  
String to hold any data you may want to pass into a transaction and potentially receive back untouched.  May also be used for customizing calculations based on business rules  

**AlternativeFuelContent** decimal[9,5], *optional*  
Numeric value that represents the percentage of alternative fuel contained in the product   0.10, 0.85

**BlendToAltFuelContent** decimal[9,5], *optional*  
Numeric Value that represents the percentage of alternative fuel found in the blend to product  0.10, 0.85

**BlendToInd**  string[1], *optional*  
 Indicates if this record refers to a blended product    Y, N

**Currency**    string[10], *optional*  
 Type of Currency the line item Unit Price and Line Amount are defined in    USD, EUR, GBP

**Unit of Measure**  string[10], *optional*  
The Unit of Measure the line item Net, Gross, and Billed units are defined in   BRL, GAL, LTR 

**FreightUnitPrice**  decimal[28,6], *optional*  
The price per unit of the freight   1.37, 2.29, 44.34

**FreightType**  string[30], *optional*  
The type of freight.    NONE, ITEMIZED_COMMON_CARRIER, NONITEMIZED_NOT_COMMON_CARRIER

**FreightLineAmount**  decimal[28,10], *optional*  
The total amount of value of product on the line item calculated by BilledUnits * FreightUnitPrice, If left blank the Avalara AvaTax Excise application will calculate  137.00, 456.58, 5213.47

**TransactionLineMeasures** <a href=#transactionlinemeasure_5_18_0>TransactionLineMeasure_5_18_0[]</a>, *optional*  
Array of Measures to convert the input value to for this transaction line element   N/A

**CustomString1**   string[128], *optional*  
String to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.    TEST, Purple, 111

**CustomString2**   string[128], *optional*  
String to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.    TEST, Purple, 111

**CustomString3**   string[128], *optional*  
String to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.    TEST, Purple, 111

**CustomNumeric1**   decimal[28,6], *optional*  
Decimal to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.   100, 0.0125, 500000000

**CustomNumeric2**   decimal[28,6], *optional*  
Decimal to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.   100, 0.0125, 500000000

**CustomNumeric3**   decimal[28,6], *optional*  
 Decimal to hold data you want to pass into a transaction to be used for customizing calculations based on business rules.   100, 0.0125, 500000000

**NthTimeSale**   decimal[2,0], *optional*  
Decimal to tell how many times a product has been sold in the supply chain. 1,2,3

#### TransactionLineMeasure_5_18_0

**QuantityInd** string[1], *optional*  
Type of Quantity for the Line referencing Billed, Net or Gross Value    B, N, G

**UnitOfMeasure** string[10], *optional*  
The Measurement type the Measure Value is defined in    BRL, GAL, LTR

**MeasureValue** decimal[28,10], *required*  
Numeric  Unit of the Quanity indicator type 100, 200, 300

#### TransactionExchangeRate_5_18_0

**FromCurrency** string[10], *optional*  
Currency type Value must start with USD, EUR, GBP

**ToCurrency** string[10], *optional*  
Currency type Value will end up as  USD, EUR, GBP

**EffectiveDate** datetime, *required*  
Date the Conversion Factor is valid for 4/23/2009, 5/17/2009

**ConversionFactor** decimal[15,10], *required*  
Numeric Amount determining the conversion factor between the from and to currencies 0.123234, 4.3245

#### TransactionLineJurisdiction_5_18_0

**SpecialJurisdictionCode** string[30], *required*  
The unique code of the special jurisdiction.

**SpecialJurisdictionType** string[30], *required*  
The local jurisdiction type of the special jurisdiction.