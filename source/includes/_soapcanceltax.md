## CancelTax

Voids or deletes and existing transaction record from the AvaTax system.

### CancelTax Request

```shell
curl -X POST --header "Content-Type: text/xml" 
--header "SOAPAction: \"http://avatax.avalara.com/services/CancelTax\"" 
--data-binary @cancelTaxRequest.xml https://development.avalara.net/tax/taxsvc.asmx

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
        <ns1:CancelTax>
            <ns1:CancelTaxRequest>
                <ns1:CompanyCode>APITrialCompany</ns1:CompanyCode>
                <ns1:DocType>SalesInvoice</ns1:DocType>
                <ns1:DocCode>INV001</ns1:DocCode>
                <ns1:CancelCode>DocVoided</ns1:CancelCode>
            </ns1:CancelTaxRequest>
        </ns1:CancelTax>
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

CancelTaxRequest cancelTaxRequest = new CancelTaxRequest();

cancelTaxRequest.CompanyCode = "APITrialCompany";
cancelTaxRequest.DocType = DocumentType.SalesInvoice;
cancelTaxRequest.DocCode = "INV001";
cancelTaxRequest.CancelCode = CancelCode.DocVoided;

CancelTaxResult cancelTaxResult = taxSvc.CancelTax(cancelTaxRequest);
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

$cancelTaxRequest = new CancelTaxRequest();
$cancelTaxRequest->setDocCode('INV001');
$cancelTaxRequest->setDocType('SalesInvoice');
$cancelTaxRequest->setCompanyCode("APITrialCompany");
$cancelTaxRequest->setCancelCode('DocVoided');

$cancelTaxResult = $taxSvc->cancelTax($cancelTaxRequest);

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

CancelTaxRequest cancelTaxRequest = new CancelTaxRequest();

cancelTaxRequest.setDocCode("INV001");
cancelTaxRequest.setCompanyCode("APITrialCompany");
cancelTaxRequest.setDocType(DocumentType.SalesInvoice);
cancelTaxRequest.setCancelCode(CancelCode.DocVoided);
cancelTaxRequest.setDocId("INV001-1");

CancelTaxResult cancelTaxResult = taxSvc.cancelTax(cancelTaxRequest);
```

Input for CancelTax indicating the document that should be cancelled and the reason for the operation.

**CompanyCode:** string [25], *required*  
Client application company reference code.  Not required if the document is identified by DocId.

**DocType:** enum as string [see below], *required*  
Value describing what type of tax document is being cancelled. One of:

* SalesInvoice
* ReturnInvoice
* PurchaseInvoice

Not required if the document is identified by DocId.

**DocCode:** string [50], *required*  
Client application identifier describing this tax transaction (i.e. invoice number, sales order number, etc.).  Not required if the document is identified by DocId.

**CancelCode:** enum as string [see below], *required*  
The reason for cancelling the tax record. One of:

* Unspecified
* PostFailed
* DocDeleted
* DocVoided
* AdjustmentCancelled

For more information, see the <a title="CancelTax" href="/api-docs/api-reference/canceltax" target="_blank">CancelTax article</a>.

**DocId:** bigint as string, *optional*  
Avatax-assigned unique Document Id, can be used in place of DocCode, DocType, and CompanyCode

### CancelTax Result

```xml
<CancelTaxResult>
    <TransactionId>0</TransactionId>
    <ResultCode>Success</ResultCode>
    <DocId>48769272</DocId>
</CancelTaxResult>
```

Output for CancelTax indicating the success of the cancellation, or any errors encountered.

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

**DocId:** bigint as string  
The unique numeric identifier (Document ID) assigned to the tax document in question by the AvaTax Service.