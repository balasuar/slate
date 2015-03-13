## CommitTax

```shell
curl -X POST --header "Content-Type: text/xml" 
--header "SOAPAction: \"http://avatax.avalara.com/services/CommitTax\"" 
--data-binary @commitTaxRequest.xml https://development.avalara.net/tax/taxsvc.asmx

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
        <ns1:CommitTax>
            <ns1:CommitTaxRequest>
                <ns1:CompanyCode>APITrialCompany</ns1:CompanyCode>
                <ns1:DocType>SalesInvoice</ns1:DocType>
                <ns1:DocCode>INV001</ns1:DocCode>
                <ns1:NewDocCode>INV001-1</ns1:NewDocCode>
            </ns1:CommitTaxRequest>
        </ns1:CommitTax>
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

CommitTaxRequest commitTaxRequest = new CommitTaxRequest();

commitTaxRequest.DocCode = "INV001";
commitTaxRequest.DocType = DocumentType.SalesInvoice;
commitTaxRequest.CompanyCode = "APITrialCompany";
commitTaxRequest.NewDocCode = "INV001-1";

CommitTaxResult commitTaxResult = taxSvc.CommitTax(commitTaxRequest);
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

$request = new CommitTaxRequest();
$request->setDocCode('INV001');
$request->setDocType('SalesInvoice');
$request->setCompanyCode("APITrialCompany");
$request->setNewDocCode('INV001-1');

$commitTaxResult = $taxSvc->commitTax($request);
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

CommitTaxRequest request = new CommitTaxRequest();

request.setDocCode("INV001");
request.setDocType(DocumentType.SalesInvoice);
request.setCompanyCode("APITrialCompany");
commitTaxRequest.setNewDocCode("INV001-1");

CommitTaxResult commitTaxResult = taxSvc.commitTax(request);
```

> The above command returns XML structured like this:

```xml
<CommitTaxResult>
    <TransactionId>0</TransactionId>
    <ResultCode>Success</ResultCode>
    <DocId>48769272</DocId>
</CommitTaxResult>
```

CommitTax is only necessary if you need to temporarily store your documents in the Avalara database in a Posted state and later commit the documents. This will require successive calls to GetTax, PostTax and CommitTax. See <a href="http://developer.avalara.com/api-docs/designing-your-integration/posttax-and-committax" target="_parent">Committing Documents</a> for more details.

### CommitTax Request

Input for CommitTax indicating the document that should be committed. You may use just the DocId to locate and commit the document (5.8 adapter and earlier, or 14.2 and later), or you may use all three of CompanyCode, DocType and DocCode.

#### Properties

**CompanyCode:** string [25], *required**

Client application company reference code.  

*Not required if the document is identified by DocId.

**DocType:** enum as string [see below], *required**

Value describing what type of tax document is being committed. One of:

* SalesInvoice
* ReturnInvoice
* PurchaseInvoice

*Not required if the document is identified by DocId.*

**DocCode:** string [50], *required*

Client application identifier describing this tax transaction (i.e. invoice number, sales order number, etc.).  

*Not required if the document is identified by DocId.*

**DocId:** bigint as string, *optional*

Avatax-assigned unique Document Id, can be used in place of CompanyCode, DocType and DocCode.

### CommitTax Result

Output for CommitTax indicating the success of the operation, or any errors encountered.

#### Properties

**Messages:** Message[]

If ResultCode is Success, Messages is null. Otherwise, it describes any warnings, errors, or exceptions encountered while processing the request.

**ResultCode:** SeverityLevel

Indicates success or failure. One of:

* Success
* Warning
* Error
* Exception

**TransactionId:** bigint as string

The unique transaction ID assigned by AvaTax to this request/response set. This value need only be retained for troubleshooting.