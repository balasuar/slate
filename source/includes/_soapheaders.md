# AvaTax SOAP API

The Avalara AvaTax APIs allow you to connect your web cart or accounting software to realtime tax calculation and address validation services. You can just retrieve tax amounts, but your transactions can also be recorded for reporting and tax filing. We have a RESTful API, class wrappers (adapters) for PHP, Java, and .NET compiled from the SOAP API, or you can build your own wrappers directly from the <a href='https://development.avalara.net/address/addresssvc.wsdl' target="_blank">address</a> and <a href='https://development.avalara.net/tax/taxsvc.wsdl' target="_blank">tax service</a> SOAP WSDLs.

The AvaTax SOAP API exposes all methods available for interacting with the AvaTax service, allowing calculation of tax, modification of documents, and validation of addresses - including some functionality not exposed by our REST API.
If you're unsure of which API to use, a full comparison of the differences between the functionality provided by our REST and SOAP interfaces is documented <a href='http://developer.avalara.com/api-docs/designing-your-integration/soap-or-rest' target="_parent">here</a>.

The sample code on this page is intended to give you an idea of how the methods are used, but you can find functioning sample source projects with full class libraries from our <a href='http://github.com/avadev' target="_parent">API Sample Code page</a>.

**Note:** You will not be able to make web service calls until you have received an active account number and license key via email, or a username and password from the <a href='http://developer.avalara.com/getting-started' target="_parent">get-started sandbox registration</a>.

## URL

**Development:** https://development.avalara.net/

**Production:** https://avatax.avalara.net/

## Headers

```shell
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
```

```csharp
TaxSvc taxSvc = new TaxSvc();
taxSvc.Configuration.Security.Account ="1234567890";
taxSvc.Configuration.Security.License = "A1B2C3D4E5F6G7H8";
taxSvc.Configuration.Url = "https://development.avalara.net";
taxSvc.Configuration.ViaUrl = "https://development.avalara.net";
taxSvc.Profile.Client = "AvaTaxSample";
taxSvc.Profile.Name = "Development";

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

```

The SOAP API uses standard WSS (Web Service Security) token to authenticate the account or user. These security tokens are supported by most SOAP tools and SDKs. The security token is not actually defined in the WSDL and must be added as a custom SOAP header. We recommend using this version if it is supported by your development environment because it provides more security options and is supported by many web service tools.

Alternate security WSDLs are also available for <a href='https://development.avalara.net/tax/taxsvcaltsec.wsdl' targest=_blank>tax</a> and <a href='https://development.avalara.net/address/addresssvcaltsec.wsdl' targest=_blank>address validation</a> services. These WSDLs use an alternate SOAP header security token for development environments that are unable to generate the standard WSS security token. The token is specified in the WSDL and should be recognized by most WSDL code generation tools. It is easier to use, but provides less security options. The service URL is also slightly different for the alternate security service, requiring a '/altsec' extensoin to be added to the standard service URL (e.g. `https://avatax.avalara.net/tax/taxsvc.asmx/altsec`)


#### Configuration

**Account:** int as string [10], *required*  
The unique account number provided by Avalara for verification against the service. 
If you are on a free trial and don't have a license key, use **Username**.

**License Key:** string [16], *required*  
The unique alpha-numeric key provided by Avalara for verification against the service. 
If you are on a free trial and don't have a license key, use **Password**.

**Username:** string [50], optional - using Account and License is preferred  
Your AvaTax Admin Console username. Usually an email address.

**Password:** string [50], optional - using Account and License is preferred\  
Your AvaTax Admin Console password.

#### Profile

**Name:** string [50], *required*  
Reference to a named profile

**Client:** string [50], *required*  
Client application name and version

**Adapter:** string [50], *required*  
Name and version of the adapter. 
This is set automatically by the .NET, PHP, and Java adapters.

**Machine:** string [50], *required*  
The NetBIOS name of the local computer. 
This is set automatically by the .NET, PHP, and Java adapters.