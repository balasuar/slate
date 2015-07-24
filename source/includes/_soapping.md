## Ping

```shell
curl -X POST --header "Content-Type: text/xml" 
--header "SOAPAction: \"http://avatax.avalara.com/services/Ping\"" 
--data-binary @pingRequest.xml https://development.avalara.net/tax/taxsvc.asmx

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
        <ns1:Ping>
            <ns1:Message/>
        </ns1:Ping>
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

PingResult pingResult = taxSvc.Ping("");
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

$pingResult = $taxSvc->ping("");
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

PingResult pingResult = taxSvc.Ping("");

```

Ping allows you to check the availability of our web service at any given time. This is merely a call to the Ping method with an empty string as the data along with account or user credentials.

### Ping Result

```xml
<PingResult>
    <ResultCode>Success</ResultCode>
    <Version>14.5.0.46</Version>	
</PingResult>
```

Result data returned from Ping.

**Version:** string [15]  
The service version of the AvaTax service.

**Messages:** <a href="#errors79">Message[]</a>  
If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request.

**ResultCode:** SeverityLevel  
Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**TransactionId:** string [19]  
The unique transaction ID assigned by AvaTax to this request/response set. This value need only be retained for troubleshooting.
