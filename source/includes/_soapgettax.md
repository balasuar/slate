## GetTax

```shell
curl -X POST --header "Content-Type: text/xml" 
--header "SOAPAction: \"http://avatax.avalara.com/services/GetTax\"" 
--data-binary @getTaxRequest.xml https://development.avalara.net/tax/taxsvc.asmx

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
        <ns1:GetTax>
            <ns1:GetTaxRequest>
                <ns1:CompanyCode>APITrialCompany</ns1:CompanyCode>
                <ns1:DocType>SalesInvoice</ns1:DocType>
                <ns1:DocCode>INV001</ns1:DocCode>
                <ns1:DocDate>2014-01-01</ns1:DocDate>
                <ns1:CustomerCode>ABC4335</ns1:CustomerCode>
                <ns1:Discount>0</ns1:Discount>
                <ns1:OriginCode>0</ns1:OriginCode>
                <ns1:DestinationCode>1</ns1:DestinationCode>
                <ns1:Addresses>
                    <ns1:BaseAddress>
                        <ns1:AddressCode>0</ns1:AddressCode>
                        <ns1:Line1>45 Fremont Street</ns1:Line1>
                        <ns1:Line2/>
                        <ns1:City>San Francisco</ns1:City>
                        <ns1:Region>CA</ns1:Region>
                        <ns1:PostalCode>94105-2204</ns1:PostalCode>
                        <ns1:Country>US</ns1:Country>
                        <ns1:TaxRegionId>0</ns1:TaxRegionId>
                    </ns1:BaseAddress>
                    <ns1:BaseAddress>
                        <ns1:AddressCode>1</ns1:AddressCode>
                        <ns1:Line1>118 N Clark St</ns1:Line1>
                        <ns1:Line2>ATTN Accounts Payable</ns1:Line2>
                        <ns1:City>Chicago</ns1:City>
                        <ns1:Region>IL</ns1:Region>
                        <ns1:PostalCode>60602-1304</ns1:PostalCode>
                        <ns1:Country>US</ns1:Country>
                        <ns1:TaxRegionId>0</ns1:TaxRegionId>
                    </ns1:BaseAddress>
                    <ns1:BaseAddress>
                        <ns1:AddressCode>2</ns1:AddressCode>
                        <ns1:Line1>100 Ravine Lane</ns1:Line1>
                        <ns1:Line2/>
                        <ns1:City>Bainbridge Island</ns1:City>
                        <ns1:Region>WA</ns1:Region>
                        <ns1:PostalCode>98110</ns1:PostalCode>
                        <ns1:Country>US</ns1:Country>
                        <ns1:TaxRegionId>0</ns1:TaxRegionId>
                    </ns1:BaseAddress>
                </ns1:Addresses>
                <ns1:Lines>
                    <ns1:Line>
                        <ns1:No>1</ns1:No>
                        <ns1:OriginCode>0</ns1:OriginCode>
                        <ns1:DestinationCode>1</ns1:DestinationCode>
                        <ns1:ItemCode>N543</ns1:ItemCode>
                        <ns1:TaxCode>NT</ns1:TaxCode>
                        <ns1:Qty>1</ns1:Qty>
                        <ns1:Amount>10</ns1:Amount>
                        <ns1:Discounted>false</ns1:Discounted>
                        <ns1:Description>Red Size 7 Widget</ns1:Description>
                    </ns1:Line>
                    <ns1:Line>
                        <ns1:No>2</ns1:No>
                        <ns1:OriginCode>0</ns1:OriginCode>
                        <ns1:DestinationCode>2</ns1:DestinationCode>
                        <ns1:ItemCode>T345</ns1:ItemCode>
                        <ns1:TaxCode>PC030147</ns1:TaxCode>
                        <ns1:Qty>3</ns1:Qty>
                        <ns1:Amount>150</ns1:Amount>
                        <ns1:Discounted>false</ns1:Discounted>
                        <ns1:Description>Size 10 Green Running Shoe</ns1:Description>
                    </ns1:Line>
                    <ns1:Line>
                        <ns1:No>3</ns1:No>
                        <ns1:OriginCode>0</ns1:OriginCode>
                        <ns1:DestinationCode>2</ns1:DestinationCode>
                        <ns1:ItemCode>FREIGHT</ns1:ItemCode>
                        <ns1:TaxCode>FR</ns1:TaxCode>
                        <ns1:Qty>1</ns1:Qty>
                        <ns1:Amount>15</ns1:Amount>
                        <ns1:Discounted>false</ns1:Discounted>
                        <ns1:Description>Shipping Charge</ns1:Description>
                    </ns1:Line>
                </ns1:Lines>
                <ns1:DetailLevel>Tax</ns1:DetailLevel>
                <ns1:HashCode>0</ns1:HashCode>
                <ns1:Commit>false</ns1:Commit>
                <ns1:ServiceMode>Automatic</ns1:ServiceMode>
                <ns1:PaymentDate>1900-01-01</ns1:PaymentDate>
                <ns1:ExchangeRate>1</ns1:ExchangeRate>
                <ns1:ExchangeRateEffDate>1900-01-01</ns1:ExchangeRateEffDate>
            </ns1:GetTaxRequest>
        </ns1:GetTax>
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

GetTaxRequest getTaxRequest = new GetTaxRequest();

getTaxRequest.CustomerCode = "ABC4335";
getTaxRequest.DocDate = DateTime.Parse("2014-01-01");
getTaxRequest.CompanyCode = "APITrialCompany";
getTaxRequest.DocCode = "INV001";
getTaxRequest.DetailLevel = DetailLevel.Tax;
getTaxRequest.Commit = false;
getTaxRequest.DocType = DocumentType.SalesInvoice;
// getTaxRequest.BusinessIdentificationNo="234243";
// getTaxRequest.CustomerUsageType = "G";
// getTaxRequest.ExemptionNo = "12345";
// getTaxRequest.Discount = 50;
// getTaxRequest.LocationCode = "01";
// getTaxRequest.TaxOverride.TaxOverrideType = TaxOverrideType.TaxDate;
// getTaxRequest.TaxOverride.Reason = "Adjustment for return";
// getTaxRequest.TaxOverride.TaxDate = DateTime.Parse("2013-07-01");
// getTaxRequest.TaxOverride.TaxAmount=0 ;
// getTaxRequest.ServiceMode = ServiceMode.Automatic;
getTaxRequest.PurchaseOrderNo = "PO123456";
getTaxRequest.ReferenceCode = "ref123456";
getTaxRequest.PosLaneCode = "09";
getTaxRequest.CurrencyCode = "USD";
getTaxRequest.ExchangeRate = (decimal)1.0;
getTaxRequest.ExchangeRateEffDate = DateTime.Parse("2013-01-01");
getTaxRequest.SalespersonCode = "Bill Sales";

Address address1 = new Address();
address1.Line1 = "45 Fremont Street";
address1.City = "San Francisco";
address1.Region = "CA";

Address address2 = new Address();
address2.Line1 = "118 N Clark St";
address2.Line2 = "Suite 100";
address2.Line3 = "ATTN Accounts Payable";
address2.City = "Chicago";
address2.Region = "IL";
address2.Country = "US";
address2.PostalCode = "60602";

Address address3 = new Address();
address3.Latitude = "47.627935";
address3.Longitude = "-122.51702";

getTaxRequest.OriginAddress = address1;
getTaxRequest.DestinationAddress = address2;

Line line1 = new Line();
line1.No = "01";
line1.ItemCode = "N543";
line1.Qty = 1;
line1.Amount = 10;
line1.OriginAddress = address1;
line1.DestinationAddress = address2;
line1.Description = "Red Size 7 Widget";
line1.TaxCode = "NT";
// line1.CustomerUsageType = "L";
// line1.ExemptionNo = "12345";
// line1.Discounted = true;
// line1.TaxIncluded = true;
// line1.TaxOverride.TaxOverrideType = TaxOverrideType.TaxDate;
// line1.TaxOverride.Reason = "Adjustment for return";
// line1.TaxOverride.TaxDate = DateTime.Parse("2013-07-01");
// line1.TaxOverride.TaxAmount = 0;
line1.Ref1 = "ref123";
line1.Ref2 = "ref456";
getTaxRequest.Lines.Add(line1);

Line line2 = new Line();
line2.No = "02";
line2.ItemCode = "T345";
line2.Qty = 3;
line2.Amount = 150;
line2.OriginAddress = address1;
line2.DestinationAddress = address3;
line2.Description = "Size 10 Green Running Shoe";
line2.TaxCode = "PC030147";
getTaxRequest.Lines.Add(line2);

Line line3 = new Line();
line3.No = "02-FR";
line3.ItemCode = "FREIGHT";
line3.Qty = 1;
line3.Amount = 15;
line3.OriginAddress = address1;
line3.DestinationAddress = address3;
line3.Description = "Shipping Charge";
line3.TaxCode = "FR";
getTaxRequest.Lines.Add(line3);

GetTaxResult getTaxResult = taxSvc.GetTax(getTaxRequest);
```

```php
<?php
require('../../AvaTax4PHP/AvaTax.php');

new ATConfig('Development', array(
    'url' => 'https://development.avalara.net',
    'account' => '1234567890',
    'license' => 'A1B2C3D4E5F6G7H8',
    'client'=>'AvaTaxSample',
    'name'=>'Development')
);

$taxSvc = new TaxServiceSoap('Development');

$getTaxRequest = new GetTaxRequest();

$getTaxRequest->setCompanyCode("APITrialCompany");
$getTaxRequest->setDocType("SalesInvoice");
$getTaxRequest->setDocCode("INV001");
$getTaxRequest->setDocDate("2014-01-01");
$getTaxRequest->setCustomerCode("ABC4335");
$getTaxRequest->setDetailLevel(DetailLevel::$Tax);
//$getTaxRequest->setSalespersonCode("Bill Sales");
//$getTaxRequest->setCustomerUsageType("G");
//$getTaxRequest->setDiscount(5.00);
//$getTaxRequest->setPurchaseOrderNo("PO123456");
//$getTaxRequest->setExemptionNo("12345");
//$getTaxRequest->setReferenceCode("ref123456");
//$getTaxRequest->setLocationCode("01");
//$getTaxRequest->setCommit(false);
//$getTaxRequest->setDiscount(5.00);
//$getTaxRequest->setCurrencyCode("USD");
//$getTaxRequest->setServiceMode("Automatic");
//$getTaxRequest->setExchangeRate("1.0");
//$getTaxRequest->setExchangeRateEffDate("2013-01-01");
//$getTaxRequest->setPosLaneCode("09");
//$getTaxRequest->setBusinessIdentificationNo(234243);
//$taxOverride = new TaxOverride();
//$getTaxRequest->setTaxOverride($taxOverride); 
//$taxOverride->setTaxOverrideType(TaxOverrideType::$TaxDate);
//$taxOverride->setTaxAmount(0.00);
//$taxOverride->setReason("Adjustment for return");
//$taxOverride->setTaxDate("2013-07-01");

$line1 = new Line();
$line1->setNo(1);
$line1->setItemCode("N543");
$line1->setDescription("Red Size 7 Widget");
$line1->setQty(1);
$line1->setAmount(10);
$line1->setTaxCode("NT");
//$line1->setDiscounted(true);
//$line->setTaxIncluded(true);
//$line1->setRevAcct("");
//$line1->setRef1("ref123");
//$line1->setRef2("ref456");
//$line1->setExemptionNo("12345");
//$line1->setCustomerUsageType("L");
//$taxOverride = new TaxOverride();
//$line1->setTaxOverride($taxOverride);
//$taxOverride->setTaxOverrideType(TaxOverrideType::$TaxDate);
//$taxOverride->setTaxAmount(0.00);
//$taxOverride->setReason("Adjustment for return");
//$taxOverride->setTaxDate("2013-07-01");

$line2 = new Line();
$line2->setNo(2);
$line2->setOriginAddress($OrigAddress);
$line2->setDestinationAddress($thirdaddress);
$line2->setItemCode("T345");
$line2->setDescription("Size 10 Green Running Shoe");
$line2->setQty(3);
$line2->setAmount(150);
$line2->setTaxCode("PC030147");

$line3 = new Line();
$line3->setOriginAddress($OrigAddress);
$line3->setDestinationAddress($thirdaddress);
$line3->setNo(3);
$line3->setItemCode("FREIGHT");
$line3->setDescription("Shipping Charge");
$line3->setQty(1);
$line3->setAmount(15);
$line3->setTaxCode("FR");

$getTaxRequest->setLines(array($line1, $line2, $line3));

$origin = new Address();
$origin->setLine1("45 Fremont Street");
$origin->setCity("San Francisco");
$origin->setRegion("CA");
$origin->setCountry("US");
$getTaxRequest->setOriginAddress($origin);

$destination = new Address();
$destination->setLine1("118 N Clark St");
$destination->setLine2("Suite 100");
$destination->setLine3("ATTN Accounts Payable");
$destination->setCity("Chicago");
$destination->setRegion("IL");
$destination->setPostalCode("60602-1304");
$destination->setCountry("US");
$getTaxRequest->setDestinationAddress($destination);

$thirdaddress = new Address();
$thirdaddress->setLine1("100 Ravine Lane");
$thirdaddress->setLine2("Suite 100");
$thirdaddress->setLine3("");
$thirdaddress->setCity("Bainbridge Island");
$thirdaddress->setRegion("WA");
$thirdaddress->setPostalCode("98110");
$thirdaddress->setCountry("US");
$getTaxRequest->setAddressCode($thirdaddress);

$getTaxResult = $taxSvc->getTax($getTaxRequest);
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

GetTaxRequest getTaxRequest = new GetTaxRequest();
Format formatter = new SimpleDateFormat("yyyy-MM-dd");

getTaxRequest.setCompanyCode("APITrialCompany");
getTaxRequest.setDocType(DocumentType.SalesInvoice);
getTaxRequest.setDocCode("INV001");
Date docDate = (Date)formatter.parseObject("2014-01-01");
getTaxRequest.setDocDate(docDate);
getTaxRequest.setCustomerCode("ABC4335");
getTaxRequest.setDetailLevel(DetailLevel.Tax);
getTaxRequest.setOriginCode("01");
getTaxRequest.setDestinationCode("02");

// getTaxRequest.setSalespersonCode("Bill Sales");
// getTaxRequest.setCustomerUsageType("G");
// getTaxRequest.setDiscount(new BigDecimal(50.00));
// getTaxRequest.setPurchaseOrderNo("PO123456");
// getTaxRequest.setExemptionNo("12345");
// getTaxRequest.setReferenceCode("ref123456");
// getTaxRequest.setLocationCode("01");
// getTaxRequest.setCommit(true);
// getTaxRequest.setCurrencyCode("USD");
// getTaxRequest.setServiceMode(ServiceMode.Automatic);
// getTaxRequest.setExchangeRate(new BigDecimal(9.00));
// Date ExchangeRateEffDate = (Date)formatter.parseObject("2013-01-01");
// getTaxRequest.setExchangeRateEffDate(ExchangeRateEffDate);
// getTaxRequest.setPosLaneCode("09");
// getTaxRequest.setBusinessIdentificationNo("234243");
//  
// TaxOverride taxOverride = new TaxOverride();
// taxOverride.setReason("Adjustment for return");
// taxOverride.setTaxOverrideType(TaxOverrideType.TaxDate);
// taxOverride.setTaxAmount(new BigDecimal(0.00));
// Date taxOverrideDate = (Date)formatter.parseObject("2013-07-01");
// taxOverride.setTaxDate(taxOverrideDate);
// getTaxRequest.setTaxOverride(taxOverride);

ArrayOfLine lines = new ArrayOfLine(3);
Line line;

line = new Line();
line.setNo("01");
line.setItemCode("N543");
line.setDescription("Red Size 7 Widget");
line.setTaxCode("PC030147");
line.setQty(new BigDecimal(1.00));
line.setAmount(new BigDecimal(10.00));
line.setTaxCode("NT");

//    line.setCustomerUsageType("L");
//    line.setExemptionNo("12345");
//    line.setDiscounted(true);
//    line.setTaxIncluded(true);
//    line.setRef1("123");
//    line.setRef2("456");

lines.add(line);

line = new Line();
line.setNo("02");
line.setOriginCode("01");
line.setDestinationCode("03");
line.setItemCode("T345");
line.setDescription("Size 10 Green Running Shoe");
line.setQty(new BigDecimal(3.00));
line.setAmount(new BigDecimal(150.00));
line.setTaxCode("PC030147");
lines.add(line);

line = new Line();
line.setOriginCode("01");
line.setDestinationCode("03");
line.setNo("03");
line.setItemCode("FREIGHT");
line.setDescription("Shipping Charge");
line.setQty(new BigDecimal(1.00));
line.setAmount(new BigDecimal(15.00));
line.setTaxCode("FR");
lines.add(line);

getTaxRequest.setLines(lines);

ArrayOfBaseAddress addresses = new ArrayOfBaseAddress(3);

BaseAddress address1 = new BaseAddress();
address1.setAddressCode("01");
address1.setLine1("45 Fremont Street");
address1.setLine2("");
address1.setLine3("");
address1.setCity("San Francisco");
address1.setRegion("CA");
address1.setPostalCode("94105");
address1.setCountry("US");
addresses.add(address1);

BaseAddress address2 = new BaseAddress();
address2.setAddressCode("02");
address2.setLine3("ATTN Accounts Payable");
address2.setLine1("118 N Clark St");
address2.setLine2("Suite 100");
address2.setCity("Chicago");
address2.setRegion("IL");
address2.setPostalCode("60602");
address2.setCountry("US");
addresses.add(address2);

BaseAddress address3 = new BaseAddress();
address3.setAddressCode("03");
address3.setLatitude("47.627935");
address3.setLongitude("-122.51702");
addresses.add(address3);

getTaxRequest.setAddresses(addresses);

GetTaxResult getTaxResult = taxSvc.getTax(getTaxRequest);
```

> The above command returns XML structured like this:

```xml
<GetTaxResult>
    <TransactionId>0</TransactionId>
    <ResultCode>Success</ResultCode>
    <DocId>48769271</DocId>
    <DocType>SalesInvoice</DocType>
    <DocCode>INV001</DocCode>
    <DocDate>2014-01-01</DocDate>
    <DocStatus>Saved</DocStatus>
    <Reconciled>false</Reconciled>
    <Timestamp>2014-03-25T23:20:34.55</Timestamp>
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
                    <TaxAuthorityType>45</TaxAuthorityType>
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
                    <TaxAuthorityType>45</TaxAuthorityType>
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
                    <TaxAuthorityType>45</TaxAuthorityType>
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
                    <TaxAuthorityType>45</TaxAuthorityType>
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
                    <TaxAuthorityType>45</TaxAuthorityType>
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
                    <TaxAuthorityType>45</TaxAuthorityType>
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
                    <TaxAuthorityType>45</TaxAuthorityType>
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
                    <TaxAuthorityType>45</TaxAuthorityType>
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
    <TaxAddresses>
        <TaxAddress>
            <Address>45 Fremont St</Address>
            <AddressCode>41744153</AddressCode>
            <BoundaryLevel>0</BoundaryLevel>
            <City>San Francisco</City>
            <Country>US</Country>
            <PostalCode>94105-2204</PostalCode>
            <Region>CA</Region>
            <TaxRegionId>2113460</TaxRegionId>
            <JurisCode/>
            <Latitude>37.791119</Latitude>
            <Longitude>-122.397366</Longitude>
            <GeocodeType>StreetLevel</GeocodeType>
            <ValidateStatus>NormalHit</ValidateStatus>
            <DistanceToBoundary>0</DistanceToBoundary>
        </TaxAddress>
        <TaxAddress>
            <Address>45 Fremont St</Address>
            <AddressCode>41744153</AddressCode>
            <BoundaryLevel>0</BoundaryLevel>
            <City>San Francisco</City>
            <Country>US</Country>
            <PostalCode>94105-2204</PostalCode>
            <Region>CA</Region>
            <TaxRegionId>2113460</TaxRegionId>
            <JurisCode/>
            <Latitude>37.791119</Latitude>
            <Longitude>-122.397366</Longitude>
            <GeocodeType>StreetLevel</GeocodeType>
            <ValidateStatus>NormalHit</ValidateStatus>
            <DistanceToBoundary>0</DistanceToBoundary>
        </TaxAddress>
        <TaxAddress>
            <Address>45 Fremont St</Address>
            <AddressCode>41744153</AddressCode>
            <BoundaryLevel>0</BoundaryLevel>
            <City>San Francisco</City>
            <Country>US</Country>
            <PostalCode>94105-2204</PostalCode>
            <Region>CA</Region>
            <TaxRegionId>2113460</TaxRegionId>
            <JurisCode>0607500000</JurisCode>
            <Latitude>37.791119</Latitude>
            <Longitude>-122.397366</Longitude>
            <GeocodeType>StreetLevel</GeocodeType>
            <ValidateStatus>NormalHit</ValidateStatus>
            <DistanceToBoundary>0</DistanceToBoundary>
        </TaxAddress>
        <TaxAddress>
            <Address>118 N Clark St Ste 100</Address>
            <AddressCode>66547563</AddressCode>
            <BoundaryLevel>0</BoundaryLevel>
            <City>Chicago</City>
            <Country>US</Country>
            <PostalCode>60602-1304</PostalCode>
            <Region>IL</Region>
            <TaxRegionId>2062953</TaxRegionId>
            <JurisCode>1703114000</JurisCode>
            <Latitude>41.884132</Latitude>
            <Longitude>-87.631048</Longitude>
            <GeocodeType>StreetLevel</GeocodeType>
            <ValidateStatus>NormalHit</ValidateStatus>
            <DistanceToBoundary>0</DistanceToBoundary>
        </TaxAddress>
        <TaxAddress>
            <Address/>
            <AddressCode>41850334</AddressCode>
            <BoundaryLevel>2</BoundaryLevel>
            <City/>
            <Country>US</Country>
            <PostalCode/>
            <Region>WA</Region>
            <TaxRegionId>2109716</TaxRegionId>
            <JurisCode/>
            <Latitude>47.627935</Latitude>
            <Longitude>-122.51702</Longitude>
            <GeocodeType/>
            <ValidateStatus>Not Validated</ValidateStatus>
            <DistanceToBoundary>2392</DistanceToBoundary>
        </TaxAddress>
        <TaxAddress>
            <Address/>
            <AddressCode>41850334</AddressCode>
            <BoundaryLevel>2</BoundaryLevel>
            <City/>
            <Country>US</Country>
            <PostalCode/>
            <Region>WA</Region>
            <TaxRegionId>2109716</TaxRegionId>
            <JurisCode>5303503736</JurisCode>
            <Latitude>47.627935</Latitude>
            <Longitude>-122.51702</Longitude>
            <GeocodeType/>
            <ValidateStatus>Not Validated</ValidateStatus>
            <DistanceToBoundary>2392</DistanceToBoundary>
        </TaxAddress>
    </TaxAddresses>
    <Locked>false</Locked>
    <AdjustmentReason>0</AdjustmentReason>
    <AdjustmentDescription/>
    <Version>1</Version>
    <TaxDate>2014-01-01</TaxDate>
    <TaxSummary/>
    <VolatileTaxRates>false</VolatileTaxRates>
</GetTaxResult>

```

Calculates taxes on a document such as a sales order, sales invoice, purchase order, purchase invoice, or credit memo.

### GetTax Request

Input for GetTax describing the document on which tax should be calculated.

#### Properties

**BusinessIdentificationNo:** string [25], *optional, unless the user needs VAT calculated*

The buyer's VAT id. Using this value will force VAT rules to be considered for the transaction. 
This may be set on the document or the line.

**Commit:** bool, *optional*

Default is false. Setting this property to True will prevent any further document state changes except CancelTax which changes the state to Voided.

**CompanyCode:** string [25], *required*

The code that identifies the company in the AvaTax account in which the document should be posted. This code is declared during the company setup in the 
<a href="https://admin-development.avalara.net/" target="_parent">AvaTax Admin Console</a>. If no value is passed, the document will be assigned to the default company.

**CurrencyCode:** string [3], *optional*

3 character ISO 4217 compliant currency code

**CustomerCode:** string [50], *required*

The client application customer reference code. This is required since it is the key to the Exemption Certificate Management Service in the Admin Console.

**CustomerUsageType:** string [25], *optional*

The client customer or usage type (or Entity Use Code). 

Standard options:

* A - Federal Government
* B - State/Local Govt.
* C - Tribal Government
* D - Foreign Diplomat
* E - Charitable Organization
* F - Religious/Education
* G - Resale
* H - Agricultural Production
* I - Industrial Prod/Mfg.
* J - Direct Pay Permit
* K - Direct Mail
* L - Other
* N - Local Government
* P - Commercial Aquaculture (Canada)
* Q - Commercial Fishery (Canada)
* R - Non-resident (Canada)
* MED1 - US MDET with exempt sales tax
* MED2 - US MDET with taxable sales tax

**DestinationAddress:** Address, *required*

Address in the collection that will be used as destination or "Ship To" location in the tax calculation.

**DetailLevel:** DetailLevel, *optional*

Specifies the level of tax detail returned in the GetTaxResult.


* Summary: Summarizes document and jurisdiction detail with no line breakout
* Document: Only document detail
* Line: Document and line detail
* Tax: Document, line and jurisdiction detail
* Diagnostic: In addition to Tax level details, indicates that the server should return information about how the tax was calculated. Intended for use only while the SDK is in a development environment. 

**Discount:** decimal, *optional*

The total discount to be applied to the line or lines identified by the Lines.Discounted property.

**DocCode:** string [50], *optional*

While this is an optional field, serious consideration should be given to using it. If no value is sent, AvaTax assigns a GUID value to keep the document unique. This can make reconciliation a challenge.

**DocDate:** date, *required*

The date on the invoice, purchase order, etc. Format YYYY-MM-DD.

**DocType:** DocumentType, *required*

The document type specifies the category of the document and affects how the document is treated after a tax calculation.

* SalesOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
* SalesInvoice: The document is a permanent invoice; document and tax calculation results are saved in the tax history. GetTaxResult will return with a DocStatus of Saved.
* PurchaseOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
* PurchaseInvoice: The document is a permanent invoice; document and tax calculation results are saved in the tax history. GetTaxResult will return with a DocStatus of Saved.
* ReturnOrder: This is a temporary document type and is not saved in tax history. GetTaxResult will return with a DocStatus of Temporary.
* ReturnInvoice: The document is a permanent sales return invoice; document and tax calculation results are saved in the tax history GetTaxResult will return with a DocStatus of Saved.

**ExchangeRate:** decimal, *optional*

Exchange Rate indicates the currency exchange rate from the transaction currency (indicated by CurrencyCode) to the company's base currency. 
Note: ExchangeRate need only be set if the transaction currency is different that of the company's base currency. Default is 1.0

**ExchangeRateEffDate:** date, *optional*

ExchangeRateEffDate indicates the effective date of the exchange rate and works in tandem with ExchangeRate. 
Default is the DocDate if null.

**ExemptionNo:** string [25], *optional*

Exemption or certificate number for the client customer. 
Note: Any value set in this property will cause the document or line to be exempted from tax calculation.

**Lines:** ArrayOfLine, *required*

Document line array. There is a limit of 1000 lines per document, but there must be at least one.

**LocationCode:** string [50], *required if outlet-based reporting is needed, otherwise optional*

Also referred to as a Store Location, Outlet Id, or Outlet code. 
Location code is a value assigned by some State jurisdictions that identifies a particular store location. 
These States may require tax liabilities to be broken out separately for each store Location

**OriginAddress:** Address, *optional*

The Address that will be used as the origin or "Shipped From" location in the tax calculation. 
If no origin address exists at the document level, the destination address will be used in the calculation. 
Note: if no Origin address is provided at the line level, the Document level origin address will be applied here as well. 

**PaymentDate:** date, *optional*

PaymentDate indicates the date that a payment was received for the document. It is only applicable for cash-basis accounting and does not need to be set. The default value is 1900-01-01 which indicates no payment received.

**PurchaseOrderNo:** string [50], *optional*

Purchase Order Number used to create the current document

**ReferenceCode:** string [50], *optional*

Essentially a data field to record the original DocCode of an document if the current document is a ReturnInvoice Document Type

**SalespersonCode:** string [25], *optional*

The client application's salesperson reference code. May also be used to identify a cash register.

**ServiceMode:** enum as string [see below], *optional*

AvaTaxLocal function - provides the ability to control whether a tax is calculated locally or AvaTax web service. The default is Automatic which calculates locally unless a remote connection is necessary for "send sales" not configured at the local server level.

* Automatic
* Local
* Remote

**TaxOverride:** TaxOverride, *optional*

TaxOverride for the document - can be used to manually override components of the tax calculation. See TaxOverride for more information.

### Line

Input property of the GetTaxRequest describing item lines.

#### Properties

**No:** string [50], *required*

Uniquely identifies the line item row.

**OriginCode** string [int MAX_VALUE], *at least one of OriginCode or DestinationCode must be declared either here or at document-level*

The line-level code that refers to the origin address. Line-level address codes will take precedence over document-level address codes if both are present.

**DestinationCode** string [int MAX_VALUE], *at least one of OriginCode or DestinationCode must be declared either here or at document-level*

The line-level code that refers to the destination address. Line-level address codes will take precedence over document-level address codes if both are present.

**ItemCode** string [50], *optional*

Your item identifier, SKU, or UPC.

**TaxCode** string [25], *optional*

AvaTax system tax code or custom tax code

**CustomerUsageType** string [25], *optional*

Same as document-level CustomerUsageType. See code options above in the GetTaxRequest elements.

**ExemptionNo:** string [25], *optional*

Exemption or certificate number for the client customer. 
Note: Any value set in this property will cause the document or line to be exempted from tax calculation.

**Description** string [255], *optional, unless you are bound by Streamlined Sales Tax requirements*

Item description

**Qty** decimal, *optional*

Item quantity. The tax engine does NOT use this as a multiplier with price to get the Amount.

**Amount** decimal, *required*

Total amount of item line (extended amount, qty * unit price)

**Discounted** boolean, *optional*

True if the document level discount is applied to this line item

**TaxIncluded** boolean, *optional*

True if the tax is already included.

**Ref1** string [250], *optional*

Text reference. Use as needed.

**Ref2** string [250], *optional*

Text reference. Use as needed.

**TaxOverride** TaxOverride, *optional*

Same as document-level TaxOverride. Use this if you only need to override individual lines.

### Address

Input property of GetTaxRequest representing addresses needed for tax calculations.

#### Properties

**AddressCode:** string [int MAX_VALUE], *required*

Reference code uniquely identifying this address instance.

**Line1:** string [50], *required*

Address line 1, required if Latitude and Longitude are not provided.

**Line2:** string [50], *optional*

Address line 2

**Line3:** string [50], *optional*

Address line 3

**City:** string [50], *optional*

City name, required unless PostalCode is specified and/or Latitude and Longitude are provided.

**Region:** string [3], *optional*

State, province, or region name. Required unless City is specified and/or Latitude and Longitude are provided.

**Country:** string [2], *optional*

Country code. If not provided, will default to "US".

**PostalCode:** string [11], *optional unless City and Region are not specified*

Postal or ZIP code, Required unless City and Region are specified, and/or Latitude and Longitude are provided.

**Latitude:** decimal, *optional*

Geographic latitude. If Latitude is defined, it is expected that the longitude field will also be provided. Failure to do so will result in operation error.

**Longitude:** decimal, *optional*

Geographic longitude. If Longitude is defined, it is expected that the latitude field will also be provided. Fail to do so will result in operation error.

**TaxRegionId:** int, *optional*

AvaTax tax region identifier. If a non-zero value is entered into TaxRegionId, other fields will be ignored.

### GetTax Result

Document-level tax calculation information.

#### Properties

**DocCode:** string [50]

The document code, if not supplied in the request the returned value is a GUID.

**DocDate:** date

Date of invoice, sales order, purchase order, etc.

**DocStatus:** enum as string [see below]

The document's status after the tax calculation. One of:

* Temporary: GetTaxRequest, DocType = SalesOrder
* Saved: GetTaxRequest, DocType = SalesInvoice
* Posted: PostTaxRequest, Commit = false
* Committed: PostTaxRequest, Commit = true or CommitTaxRequest on document in Posted state
* Cancelled: CancelTaxRequest, CancelCode = DocVoided
* Adjusted: AdjustTaxRequest

**DocType:** DocumentType

The DocumentType used in the GetTaxRequest

**Locked:** boolean

Flag indicating if a Document has been locked by Avalara's Managed Returns Service process. Locked documents can not be modified and can not be cancelled because they have been reported on Tax Return.

**TaxDate:** DateTime

Tax Date is the date used to calculate tax on the Document.

**TaxLines:** TaxLine[]

Tax broken down by individual TaxLine.

**TaxSummary:** TaxDetail[]

Summary of the jurisdiction details for all item lines (returned for detail levels Summary and Line).

**Timestamp:** DateTime

Server timestamp of the request.

**TotalAmount:** decimal

Sum of all line Amount values.

**TotalDiscount:** decimal

Sum of all TaxLine discount amounts.

**TotalTax:** decimal

Sum of all TaxLine tax amounts.

**TotalTaxable:** decimal

Total taxable amount.

**TotalTaxCalculated:** decimal

TotalTaxCalculated indicates the total tax calculated by AvaTax. This is usually the same as the TotalTax, except when a tax override amount is specified. This is for informational purposes. The TotalTax will still be used for reporting.

**TransactionId:** bigint as string

A unique Transaction ID identifying a specific request/response set.

**Version:** int

Current version of the document.

**VolatileTaxRated:** boolean

Deprecated.

**TaxAddresses:** TaxAddress[]

Array of resolved addresses used in the tax calculation.

**ResultCode:** SeverityLevel

Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**Messages:** Message[]

If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request.

### TaxLine

Taxes for a specific document Line.

#### Properties

**AccountingMethod:** AccountingMethod

This is the accounting applied to the line. Since only Accrual accounting is currently supported, it is always Accrual.

**BoundaryLevel:** BoundaryLevel

The level of jurisdiction boundary precision used for the tax calculation.

**Discount:** decimal

Discount amount applied to this line

**ExemptCertId:** int

Applied ExemptionCertificateId for the Line.

**No:** string [50]

Line Number

**Tax:** decimal

The tax amount, either the calculated amount or an override amount

**Taxability:** boolean

Is the item taxable?

**TaxCalculated:** decimal

TaxCalculated indicates the tax calculated by AvaTax. This will normally be the same as the Tax property unless it has been overridden by a TaxAmount.

**TaxCode:** string [25]

System Tax Code

**TaxDetails:** TaxDetail[]

Tax by jurisdiction. See TaxDetail properties below.

**TaxIncluded:** boolean

Indicates the value of TaxIncluded sent on the line of the GetTaxRequest.

### TaxDetail

Tax details by jurisdiction. Information returned is dependent on the DetailLevel passed in the request.

#### Properties

**Country:** string [2]

2-character ISO country code

**Exemption:** decimal

The portion of the detail that is exempt from taxes.

**JurisCode:** string [10]

Jurisdiction Code for the taxing jurisdiction

**JurisName:** string [200]

Gets the jurisdiction name.

**JurisType:** JurisdictionType

Jurisdiction Type

**NonTaxable:** decimal

The portion of the detail that is not subject to taxes.

**Rate:** decimal

The tax rate for the jurisdiction.

**RateType:** string [1]

RateType indicates the tax rate type. These currently include: 

* F = Food (US)
* G = General (US)
* S = Standard (VAT)
* R = Reduced (VAT)
* Q = Super Reduced (VAT)
* A = Reduced Rate 1 (VAT)
* B = Reduced Rate 2 (VAT)
* Z = Zero Rate

**Region:** string [3]

State or province code

**StateAssignedNo:** string [50]

StateAssignedNo is the identifier given to the jurisdiction by the state. Not all states have these.

**Tax:** decimal

The tax amount, either the calculated amount or an override amount

**Taxable:** decimal

The amount of the sale that is determined to be taxable.

**TaxAuthorityType:** int

Internal tax authority type identifier used by our returns engine.

**TaxCalculated:** decimal

TaxCalculated indicates the tax calculated by AvaTax. It will usually be the same as the Tax property, unless it has been overridden by a TaxAmount.

**TaxName:** string [75]

It further defines the tax and jurisdiction.

**TaxType:** TaxType

Tax Type - Sales or Seller's Use

### TaxAddress

TaxAddress represents canonical addresses used in tax calculation.

#### Properties

**Address:** string [50]

Canonical street address

**AddressCode:** string

Reference code uniquely identifying this address instance. AddressCode will always correspond to an address code supplied to in the address collection provided in the request.

**City:** string [50]

City name

**Region:** string [3]

State or region name

**Country:** string

Country code, as ISO 3166-1 (Alpha-2) country code (e.g. “US”)

**PostalCode:** string

Postal code

**Latitude:** decimal

Geographic latitude. Latitude is only defined if input address was a geographic point.

**Longitude:** decimal

Geographic longitude. Longitude is only defined if input address was a geographic point.

**TaxRegionId:** string

AvaTax tax region identifier

**JurisCode:** string

Tax jurisdiction code