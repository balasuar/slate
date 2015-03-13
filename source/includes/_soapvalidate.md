## ValidateAddress

```shell
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
        <ns1:Validate>
            <ns1:ValidateRequest>
                <ns1:Address>
                    <ns1:Line1>118 N Clark St</ns1:Line1>
                    <ns1:Line2>Suite 100</ns1:Line2>
                    <ns1:Line3>ATTN Accounts Payable</ns1:Line3>
                    <ns1:City>Chicago</ns1:City>
                    <ns1:Region>IL</ns1:Region>
                    <ns1:PostalCode>60602</ns1:PostalCode>
                </ns1:Address>
                <ns1:Coordinates>true</ns1:Coordinates>
                <ns1:Taxability>true</ns1:Taxability>
                <ns1:TextCase>Upper</ns1:TextCase>
            </ns1:ValidateRequest>
        </ns1:Validate>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>

```

```csharp
AddressSvc addressSvc = new AddressSvc();
addressSvc.Configuration.Security.Account="1234567890";
addressSvc.Configuration.Security.License="A1B2C3D4E5F6G7H8";
addressSvc.Configuration.Url = "https://development.avalara.net";
addressSvc.Configuration.ViaUrl = "https://development.avalara.net";
addressSvc.Profile.Client = "AvaTaxSample";
addressSvc.Profile.Name = "Development";

ValidateRequest validateRequest = new ValidateRequest();
Address address = new Address(); 

address.Line1 = "118 N Clark St";
address.Line2 = "Suite 100";
address.Line3 = "ATTN Accounts Payable";
address.City = "Chicago";
address.Region = "IL";
address.Country = "US";
address.PostalCode = "60602"

validateRequest.Address = address;
validateRequest.Coordinates = true;
validateRequest.Taxability = true;
validateRequest.TextCase = TextCase.Upper;

ValidateResult validateResult = addressSvc.Validate(validateRequest);
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
$addressSvc = new AddressServiceSoap('Development');

$address = new Address();
$address->setLine1("118 N Clark St");
$address->setLine2("");
$address->setLine3("");
$address->setCity("Chicago");
$address->setRegion("IL");
$address->setPostalCode("60602");
$textCase = TextCase::$Mixed;
$coordinates = 1;

$validateRequest = new ValidateRequest($address, $textCase, $coordinates);

$validateResult = $addressSvc->Validate($validateRequest);

?>

```

```java
AddressSvcLocator AddressSvc = new AddressSvcLocator();
String url = "https://development.avalara.net";
AddressSvcSoap addressSvc = AddressSvc.getAddressSvcSoap(new URL(url));
Profile profile = new Profile();
profile.setClient("AvaTaxSample");
addressSvc.setProfile(profile);
Security security = new Security();
security.setAccount("1234567890");
security.setLicense("A1B2C3D4E5F6G7H8");
addressSvc.setSecurity(security);

ValidateRequest validateRequest = new ValidateRequest();
Address address = new Address();

address.setLine3("ATTN Accounts Payable");
address.setLine1("118 N Clark St");
address.setLine2("Suite 100");
address.setCity("Chicago");
address.setRegion("IL");
address.setPostalCode("");
validateRequest.setTextCase(TextCase.Default);
validateRequest.setCoordinates(true);

validateRequest.setAddress(address);

ValidateResult validateResult = addressSvc.validate(validateRequest);

```

> The above command returns XML structured like this:

```xml
<ValidateResult>
    <TransactionId>0</TransactionId>
    <ResultCode>Success</ResultCode>
    <ValidAddresses>
        <ValidAddress>
            <AddressCode/>
            <Line1>ATTN ACCOUNTS PAYABLE</Line1>
            <Line2>118 N CLARK ST STE 100</Line2>
            <Line3/>
            <City>CHICAGO</City>
            <Region>IL</Region>
            <PostalCode>60602-1304</PostalCode>
            <Country>US</Country>
            <TaxRegionId>2062953</TaxRegionId>
            <Latitude>41.883739</Latitude>
            <Longitude>-87.630989</Longitude>
            <Line4>CHICAGO IL 60602-1304</Line4>
            <County>COOK</County>
            <FipsCode>1703100000</FipsCode>
            <CarrierRoute>C012</CarrierRoute>
            <PostNet>606021304990</PostNet>
            <AddressType>H</AddressType>
            <ValidateStatus/>
            <GeocodeType/>
        </ValidAddress>
    </ValidAddresses>
    <Taxable>true</Taxable>
</ValidateResult>
```

Normalizes a single US or Canadian address, providing a non-ambiguous address match.

### Validate Request

Input to normalize a single US or Canadian address, providing a non-ambiguous address match.

#### Properties

**Line1:** string [50], *required*

Address line 1

**Line2:** string [50], *optional*

Address line 2

**Line3:** string [50], *optional*

Address line 3

**City:** string [50], *optional unless PostalCode is not specified*

City name

**Region:** string [3], *optional unless PostalCode is not specified*

State, province, or region name

**Country:** string [2], *optional*

Country code

**PostalCode:** string [11], *optional unless City and Region are not specified*

Postal or ZIP code

**Coordinates:** boolean, *optional*

Indicates whether latitude and longitude values should be returned in the ValidateResult object. Default is false.

**Taxability:** boolean, *optional*

Indicates whether the AvaTax TaxRegionId should be returned in the ValidateResult object. Default is false.

**TextCase:** enum as string [see below], *optional*

The casing to apply to the valid address(es) returned in the validation result. Default is Mixed Case.

Values:

* Default
* Mixed
* Upper

### Validate Result
Output for address/validate showing the validated address match or address validation errors.

#### Properties

**Line1:** string [50]

Address line 1

**Line2:** string [50]

Address line 2

**Line3:** string [50]

Address line 3

**City:** string [50]

City name

**Region:** string [3]

State, province or region name

**Country:** string [2]

Country code as ISO 3166-1 (Alpha-2) country code (e.g. “US”)

**AddressType:** string [1]

Address type code.

* F - Firm or company address
* G - General Delivery address
* H - High-rise or business complex
* P - PO Box address
* R - Rural route address
* S - Street or residential address

**PostalCode:** string [11]

Postal or ZIP code

**County:** string [50]

County name

**FipsCode:** string [10]

FIPSCode is a unique 10-digit code representing each geographic combination of state, county, and city. The code is made up of the Federal Information Processing Code (FIPS) that uniquely identifies each state, county, and city in the U.S. Returned for US addresses only.

Digits represent jurisdiction codes:

* 1-2 State code
* 3-5 County code
* 6-10 City code

**CarrierRoute:** string [4]

CarrierRoute is a four-character string representing a US postal carrier route. The first character of this property, the term, is always alphabetic, and the last three numeric. For example, "R001" or "C027" would be typical carrier routes. The alphabetic letter indicates the type of delivery associated with this address. Returned for US addresses only.

* B - PO Box
* C - City delivery
* G - General delivery
* H - Highway contract
* R - Rural route

**TaxRegionId:** int

AvaTax tax region identifier

**PostNet:** string [12]

POSTNet is a 12-digit barcode containing the ZIP Code, ZIP+4 Code, and the delivery point code, used by the USPS to direct mail. Returned for US addresses only digits represent delivery information:

* 1-5 ZIP code
* 6-9 Plus4 code
* 10-11 Delivery point
* 12 Check digit

**ResultCode:** SeverityLevel

Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**Messages:** Message[]

If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request.