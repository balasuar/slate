## GetTaxHistory

GetTaxHistory allows you to query our service to retrieve details for previously saved documents.

### GetTaxHistory Request

```shell
curl -X POST --header "Content-Type: text/xml" 
--header "SOAPAction: \"http://avatax.avalara.com/services/GetTaxHistory\"" 
--data-binary @getTaxHistoryRequest.xml https://development.avalara.net/tax/taxsvc.asmx

<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://avatax.avalara.com/services">
<SOAP-ENV:Header>
<wsse:Security xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" SOAP-ENV:mustUnderstand="1">
<wsse:UsernameToken>
<wsse:Username>1234567890</wsse:Username>
<wsse:Password Type="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0#PasswordText">A1B2C3D4E5F6G7H8</wsse:Password>
</wsse:UsernameToken>
</wsse:Security>
<Profile xmlns="http://avatax.avalara.com/services" SOAP-ENV:actor="http://schemas.xmlsoap.org/soap/actor/next" SOAP-ENV:mustUnderstand="0">
<Client>AvaTaxSample</Client>
<Adapter>customAdapter</Adapter>
<Name>Development</Name>
</Profile>
</SOAP-ENV:Header>
<SOAP-ENV:Body>
<ns1:GetTaxHistory>
<ns1:GetTaxHistoryRequest>
<ns1:CompanyCode>APITrialCompany</ns1:CompanyCode>
<ns1:DocType>SalesInvoice</ns1:DocType>
<ns1:DocCode>INV001</ns1:DocCode>
<ns1:DetailLevel>Tax</ns1:DetailLevel>
</ns1:GetTaxHistoryRequest>
</ns1:GetTaxHistory>
</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

```csharp
TaxSvc taxSvc = new TaxSvc();

taxSvc.Configuration.Security.Account ="1234567890";
taxSvc.Configuration.Security.License = "A1B2C3D4E5F6G7H8";
taxSvc.Configuration.Url = "https://development.avalara.net";
taxSvc.Configuration.ViaUrl = "https://development.avalara.net";
taxSvc.Profile.Client = "AvaTaxSample";
taxSvc.Profile.Name = "Development";

GetTaxHistoryRequest getTaxHistoryRequest = new GetTaxHistoryRequest();

getTaxHistoryRequest.CompanyCode = "APITrialCompany";
getTaxHistoryRequest.DocType = DocumentType.SalesInvoice;
getTaxHistoryRequest.DocCode = "INV001";
getTaxHistoryRequest.DetailLevel = DetailLevel.Tax;

GetTaxHistoryResult getTaxHistoryResult = taxSvc.GetTaxHistory(getTaxHistoryRequest);

```

```php
<?php
require('../../AvaTax4PHP/AvaTax.php');

new ATConfig('Development', array(
    'url' => 'https://development.avalara.net',
    'account' => '1234567890',
    'license' => 'A1B2C3D4E5F6G7H8')
);

$taxSvc = new TaxServiceSoap('Development');

$getTaxHistoryRequest = new GetTaxHistoryRequest();
$getTaxHistoryRequest->setCompanyCode("APITrialCompany");
$getTaxHistoryRequest->setDocType(DocumentType::$SalesInvoice);
$getTaxHistoryRequest->setDocCode("INV001");
$getTaxHistoryRequest->setDetailLevel(DetailLevel::$Tax);

$getTaxHistoryResult = $taxSvc->getTaxHistory($getTaxHistoryRequest);
?>
```

```java
TaxSvcLocator taxSvcLocator = new TaxSvcLocator();
String url = "https://development.avalara.net";
TaxSvcSoap taxSvc = taxSvcLocator.getTaxSvcSoap(new URL(url));
Profile profile = new Profile();
profile.setClient("AvaTaxSample");
taxSvc.setProfile(profile);
Security security = new Security();
security.setAccount("1234567890");
security.setLicense("A1B2C3D4E5F6G7H8");
taxSvc.setSecurity(security);

GetTaxHistoryRequest getTaxHistoryRequest = new GetTaxHistoryRequest();
getTaxHistoryRequest.setDocCode("INV001");
getTaxHistoryRequest.setCompanyCode("APITrialCompany");
getTaxHistoryRequest.setDocType(DocumentType.SalesInvoice);
getTaxHistoryRequest.setDetailLevel(DetailLevel.Tax);

GetTaxHistoryResult getTaxHistoryResult = taxSvc.getTaxHistory(getTaxHistoryRequest);

```

Input for GetTaxHistory indicating the document for which history should be retrieved. The request must specify all of CompanyCode, DocCode, and DocType in order to uniquely identify the document.

**CompanyCode:** string [25], *required*  
Gets or sets the client application company reference code.

**DocCode:** string [50], *required*  
Gets or sets the Document Code, i.e. the internal reference code used by the client application.

**DocType:** DocumentType, *required*  
The original document's type, such as Sales Invoice or Purchase Invoice

**DetailLevel:** DetailLevel, *required*  
Specifies the level of detail to return.

### GetTaxHistory Result

```xml
<GetTaxHistoryResult>
    <TransactionId>0</TransactionId>
    <ResultCode>Success</ResultCode>
    <GetTaxRequest>
        <CompanyCode>APITrialCompany</CompanyCode>
        <DocType>SalesInvoice</DocType>
        <DocCode>INV0012014032502</DocCode>
        <DocDate>2014-01-01</DocDate>
        <SalespersonCode>Bill Sales</SalespersonCode>
        <CustomerCode>ABC4335</CustomerCode>
        <CustomerUsageType/>
        <Discount>0</Discount>
        <PurchaseOrderNo>PO123456</PurchaseOrderNo>
        <ExemptionNo/>
        <OriginCode>0</OriginCode>
        <DestinationCode>1</DestinationCode>
        <Addresses>
            <BaseAddress>
                <AddressCode>0</AddressCode>
                <Line1>45 Fremont St</Line1>
                <Line2/>
                <Line3/>
                <City>San Francisco</City>
                <Region>CA</Region>
                <PostalCode>94105-2204</PostalCode>
                <Country>US</Country>
                <TaxRegionId>0</TaxRegionId>
                <Latitude/>
                <Longitude/>
            </BaseAddress>
            <BaseAddress>
                <AddressCode>1</AddressCode>
                <Line1>118 N Clark St Ste 100</Line1>
                <Line2/>
                <Line3/>
                <City>Chicago</City>
                <Region>IL</Region>
                <PostalCode>60602-1304</PostalCode>
                <Country>US</Country>
                <TaxRegionId>0</TaxRegionId>
                <Latitude/>
                <Longitude/>
            </BaseAddress>
            <BaseAddress>
                <AddressCode>2</AddressCode>
                <Line1/>
                <Line2/>
                <Line3/>
                <City/>
                <Region>WA</Region>
                <PostalCode/>
                <Country>US</Country>
                <TaxRegionId>0</TaxRegionId>
                <Latitude/>
                <Longitude/>
            </BaseAddress>
        </Addresses>
        <Lines>
            <Line>
                <No>01</No>
                <OriginCode/>
                <DestinationCode/>
                <ItemCode>N543</ItemCode>
                <TaxCode>NT</TaxCode>
                <Qty>1.0000</Qty>
                <Amount>10</Amount>
                <Discounted>false</Discounted>
                <RevAcct/>
                <Ref1>ref123</Ref1>
                <Ref2>ref456</Ref2>
                <ExemptionNo/>
                <CustomerUsageType/>
                <Description>Red Size 7 Widget</Description>
                <TaxIncluded>false</TaxIncluded>
                <BusinessIdentificationNo/>
            </Line>
            <Line>
                <No>02</No>
                <OriginCode/>
                <DestinationCode>2</DestinationCode>
                <ItemCode>T345</ItemCode>
                <TaxCode>PC030147</TaxCode>
                <Qty>3.0000</Qty>
                <Amount>150</Amount>
                <Discounted>false</Discounted>
                <RevAcct/>
                <Ref1/>
                <Ref2/>
                <ExemptionNo/>
                <CustomerUsageType/>
                <Description>Size 10 Green Running Shoe</Description>
                <TaxIncluded>false</TaxIncluded>
                <BusinessIdentificationNo/>
            </Line>
            <Line>
                <No>02-FR</No>
                <OriginCode/>
                <DestinationCode>2</DestinationCode>
                <ItemCode>FREIGHT</ItemCode>
                <TaxCode>FR</TaxCode>
                <Qty>1.0000</Qty>
                <Amount>15</Amount>
                <Discounted>false</Discounted>
                <RevAcct/>
                <Ref1/>
                <Ref2/>
                <ExemptionNo/>
                <CustomerUsageType/>
                <Description>Shipping Charge</Description>
                <TaxIncluded>false</TaxIncluded>
                <BusinessIdentificationNo/>
            </Line>
        </Lines>
        <DetailLevel>Tax</DetailLevel>
        <ReferenceCode>ref123456</ReferenceCode>
        <HashCode>0</HashCode>
        <LocationCode/>
        <Commit>false</Commit>
        <BatchCode/>
        <CurrencyCode>USD</CurrencyCode>
        <ServiceMode>Automatic</ServiceMode>
        <PaymentDate>1900-01-01</PaymentDate>
        <ExchangeRate>1.0000</ExchangeRate>
        <ExchangeRateEffDate>2013-01-01</ExchangeRateEffDate>
        <PosLaneCode>09</PosLaneCode>
        <BusinessIdentificationNo/>
    </GetTaxRequest>
    <GetTaxResult>
        <TransactionId>0</TransactionId>
        <ResultCode>Success</ResultCode>
        <DocId>48769272</DocId>
        <DocType>SalesInvoice</DocType>
        <DocCode>INV0012014032502</DocCode>
        <DocDate>2014-01-01</DocDate>
        <DocStatus>Cancelled</DocStatus>
        <Reconciled>false</Reconciled>
        <Timestamp>2014-03-25T23:20:35.847</Timestamp>
        <TotalAmount>175</TotalAmount>
        <TotalDiscount>0</TotalDiscount>
        <TotalExemption>10.94</TotalExemption>
        <TotalTaxable>164.06</TotalTaxable>
        <TotalTax>14.27</TotalTax>
        <TotalTaxCalculated>14.27</TotalTaxCalculated>
        <HashCode>0</HashCode>
        <TaxLines>
            <TaxLine>
                <No>01</No>
                <TaxCode>NT</TaxCode>
                <Taxability>false</Taxability>
                <BoundaryLevel>Address</BoundaryLevel>
                <Exemption>10</Exemption>
                <Discount>0</Discount>
                <Taxable>0</Taxable>
                <Rate>0.092500</Rate>
                <Tax>0</Tax>
                <TaxCalculated>0</TaxCalculated>
                <TaxIncluded>false</TaxIncluded>
                <TaxDetails>
                    <TaxDetail>
                        <Country>US</Country>
                        <Region>IL</Region>
                        <JurisType>State</JurisType>
                        <JurisCode>17</JurisCode>
                        <TaxType>Sales</TaxType>
                        <Base>0</Base>
                        <Taxable>0</Taxable>
                        <Rate>0.062500</Rate>
                        <Tax>0</Tax>
                        <TaxCalculated>0</TaxCalculated>
                        <NonTaxable>10</NonTaxable>
                        <Exemption>0</Exemption>
                        <JurisName>ILLINOIS</JurisName>
                        <TaxName>IL STATE TAX</TaxName>
                        <TaxAuthorityType>-1</TaxAuthorityType>
                        <TaxGroup/>
                        <RateType>G</RateType>
                        <StateAssignedNo>016-0001-1 CHICAGO</StateAssignedNo>
                    </TaxDetail>
                    <TaxDetail>
                        <Country>US</Country>
                        <Region>IL</Region>
                        <JurisType>County</JurisType>
                        <JurisCode>031</JurisCode>
                        <TaxType>Sales</TaxType>
                        <Base>0</Base>
                        <Taxable>0</Taxable>
                        <Rate>0.007500</Rate>
                        <Tax>0</Tax>
                        <TaxCalculated>0</TaxCalculated>
                        <NonTaxable>10</NonTaxable>
                        <Exemption>0</Exemption>
                        <JurisName>COOK</JurisName>
                        <TaxName>IL COUNTY TAX</TaxName>
                        <TaxAuthorityType>-1</TaxAuthorityType>
                        <TaxGroup/>
                        <RateType>G</RateType>
                        <StateAssignedNo>016-0001-1 CHICAGO</StateAssignedNo>
                    </TaxDetail>
                    <TaxDetail>
                        <Country>US</Country>
                        <Region>IL</Region>
                        <JurisType>City</JurisType>
                        <JurisCode>14000</JurisCode>
                        <TaxType>Sales</TaxType>
                        <Base>0</Base>
                        <Taxable>0</Taxable>
                        <Rate>0.012500</Rate>
                        <Tax>0</Tax>
                        <TaxCalculated>0</TaxCalculated>
                        <NonTaxable>10</NonTaxable>
                        <Exemption>0</Exemption>
                        <JurisName>CHICAGO</JurisName>
                        <TaxName>IL CITY TAX</TaxName>
                        <TaxAuthorityType>-1</TaxAuthorityType>
                        <TaxGroup/>
                        <RateType>G</RateType>
                        <StateAssignedNo>016-0001-1 CHICAGO</StateAssignedNo>
                    </TaxDetail>
                    <TaxDetail>
                        <Country>US</Country>
                        <Region>IL</Region>
                        <JurisType>Special</JurisType>
                        <JurisCode>AQOF</JurisCode>
                        <TaxType>Sales</TaxType>
                        <Base>0</Base>
                        <Taxable>0</Taxable>
                        <Rate>0.010000</Rate>
                        <Tax>0</Tax>
                        <TaxCalculated>0</TaxCalculated>
                        <NonTaxable>10</NonTaxable>
                        <Exemption>0</Exemption>
                        <JurisName>REGIONAL TRANSPORT. AUTHORITY (RTA)</JurisName>
                        <TaxName>IL SPECIAL TAX</TaxName>
                        <TaxAuthorityType>-1</TaxAuthorityType>
                        <TaxGroup/>
                        <RateType>G</RateType>
                        <StateAssignedNo>016-0001-1 CHICAGO</StateAssignedNo>
                    </TaxDetail>
                </TaxDetails>
                <ExemptCertId>0</ExemptCertId>
                <TaxDate>2014-01-01</TaxDate>
                <ReportingDate>2014-01-01</ReportingDate>
                <AccountingMethod>Accrual</AccountingMethod>
            </TaxLine>
            <TaxLine>
                <No>02</No>
                <TaxCode>PC030147</TaxCode>
                <Taxability>true</Taxability>
                <BoundaryLevel>Zip5</BoundaryLevel>
                <Exemption>0</Exemption>
                <Discount>0</Discount>
                <Taxable>150</Taxable>
                <Rate>0.087000</Rate>
                <Tax>13.05</Tax>
                <TaxCalculated>13.05</TaxCalculated>
                <TaxIncluded>false</TaxIncluded>
                <TaxDetails>
                    <TaxDetail>
                        <Country>US</Country>
                        <Region>WA</Region>
                        <JurisType>State</JurisType>
                        <JurisCode>53</JurisCode>
                        <TaxType>Sales</TaxType>
                        <Base>150</Base>
                        <Taxable>150</Taxable>
                        <Rate>0.065000</Rate>
                        <Tax>9.75</Tax>
                        <TaxCalculated>9.75</TaxCalculated>
                        <NonTaxable>0</NonTaxable>
                        <Exemption>0</Exemption>
                        <JurisName>WASHINGTON</JurisName>
                        <TaxName>WA STATE TAX</TaxName>
                        <TaxAuthorityType>-1</TaxAuthorityType>
                        <TaxGroup/>
                        <RateType>G</RateType>
                        <StateAssignedNo/>
                    </TaxDetail>
                    <TaxDetail>
                        <Country>US</Country>
                        <Region>WA</Region>
                        <JurisType>City</JurisType>
                        <JurisCode>03736</JurisCode>
                        <TaxType>Sales</TaxType>
                        <Base>150</Base>
                        <Taxable>150</Taxable>
                        <Rate>0.022000</Rate>
                        <Tax>3.3</Tax>
                        <TaxCalculated>3.3</TaxCalculated>
                        <NonTaxable>0</NonTaxable>
                        <Exemption>0</Exemption>
                        <JurisName>BAINBRIDGE ISLAND</JurisName>
                        <TaxName>WA CITY TAX</TaxName>
                        <TaxAuthorityType>-1</TaxAuthorityType>
                        <TaxGroup/>
                        <RateType>G</RateType>
                        <StateAssignedNo>1804</StateAssignedNo>
                    </TaxDetail>
                </TaxDetails>
                <ExemptCertId>0</ExemptCertId>
                <TaxDate>2014-01-01</TaxDate>
                <ReportingDate>2014-01-01</ReportingDate>
                <AccountingMethod>Accrual</AccountingMethod>
            </TaxLine>
            <TaxLine>
                <No>02-FR</No>
                <TaxCode>FR</TaxCode>
                <Taxability>true</Taxability>
                <BoundaryLevel>Zip5</BoundaryLevel>
                <Exemption>0.94</Exemption>
                <Discount>0</Discount>
                <Taxable>14.06</Taxable>
                <Rate>0.087000</Rate>
                <Tax>1.22</Tax>
                <TaxCalculated>1.22</TaxCalculated>
                <TaxIncluded>false</TaxIncluded>
                <TaxDetails>
                    <TaxDetail>
                        <Country>US</Country>
                        <Region>WA</Region>
                        <JurisType>State</JurisType>
                        <JurisCode>53</JurisCode>
                        <TaxType>Sales</TaxType>
                        <Base>14.06</Base>
                        <Taxable>14.06</Taxable>
                        <Rate>0.065000</Rate>
                        <Tax>0.91</Tax>
                        <TaxCalculated>0.91</TaxCalculated>
                        <NonTaxable>0.94</NonTaxable>
                        <Exemption>0</Exemption>
                        <JurisName>WASHINGTON</JurisName>
                        <TaxName>WA STATE TAX</TaxName>
                        <TaxAuthorityType>-1</TaxAuthorityType>
                        <TaxGroup/>
                        <RateType>G</RateType>
                        <StateAssignedNo/>
                    </TaxDetail>
                    <TaxDetail>
                        <Country>US</Country>
                        <Region>WA</Region>
                        <JurisType>City</JurisType>
                        <JurisCode>03736</JurisCode>
                        <TaxType>Sales</TaxType>
                        <Base>14.06</Base>
                        <Taxable>14.06</Taxable>
                        <Rate>0.022000</Rate>
                        <Tax>0.31</Tax>
                        <TaxCalculated>0.31</TaxCalculated>
                        <NonTaxable>0.94</NonTaxable>
                        <Exemption>0</Exemption>
                        <JurisName>BAINBRIDGE ISLAND</JurisName>
                        <TaxName>WA CITY TAX</TaxName>
                        <TaxAuthorityType>-1</TaxAuthorityType>
                        <TaxGroup/>
                        <RateType>G</RateType>
                        <StateAssignedNo>1804</StateAssignedNo>
                    </TaxDetail>
                </TaxDetails>
                <ExemptCertId>0</ExemptCertId>
                <TaxDate>2014-01-01</TaxDate>
                <ReportingDate>2014-01-01</ReportingDate>
                <AccountingMethod>Accrual</AccountingMethod>
            </TaxLine>
        </TaxLines>
        <TaxAddresses/>
        <Locked>false</Locked>
        <AdjustmentReason>4</AdjustmentReason>
        <AdjustmentDescription>Transaction Adjusted for Testing</AdjustmentDescription>
        <Version>2</Version>
        <TaxDate>2014-01-01</TaxDate>
        <TaxSummary/>
        <VolatileTaxRates>false</VolatileTaxRates>
    </GetTaxResult>
</GetTaxHistoryResult>
```

Result data returned from GetTaxHistory. You can retrieve any part of the GetTaxRequest or GetTaxResult.

**GetTaxRequest:** <a href='#gettaxrequest'>GetTaxRequest</a>  
The original GetTaxRequest for the document.

**GetTaxResult:** <a href='#gettaxresult'>GetTaxResult</a>  
The original GetTaxResult for the document.

**Messages:** <a href="#errors79">Message[]</a>  
If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request.

**ResultCode:** SeverityLevel  
Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**TransactionId:** bigint as string  
The unique transaction ID assigned by AvaTax to this request/response set. This value need only be retained for troubleshooting.