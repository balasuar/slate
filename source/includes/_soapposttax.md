## PostTax

The PostTax method can be used to modify the state of a document saved to the AvaTax database via SalesInvoice, ReturnInvoice or PurchaseInvoice methods.

**Note:** PostTax can be used to Commit a document and/or change the Document Code (invoice number).

See <a href="http://developer.avalara.com/api-docs/designing-your-integration/posttax-and-committax" target="_parent">Committing Documents</a> for more details.

### PostTax Request

```shell
curl -X POST --header "Content-Type: text/xml" 
--header "SOAPAction: \"http://avatax.avalara.com/services/PostTax\"" 
--data-binary @validateRequest.xml https://development.avalara.net/tax/taxsvc.asmx

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
        <ns1:PostTax>
            <ns1:PostTaxRequest>
                <ns1:CompanyCode>APITrialCompany</ns1:CompanyCode>
                <ns1:DocType>SalesInvoice</ns1:DocType>
                <ns1:DocCode>INV001</ns1:DocCode>
                <ns1:DocDate>2014-01-01</ns1:DocDate>
                <ns1:TotalAmount>175</ns1:TotalAmount>
                <ns1:TotalTax>14.27</ns1:TotalTax>
                <ns1:HashCode>0</ns1:HashCode>
                <ns1:Commit>false</ns1:Commit>
            </ns1:PostTaxRequest>
        </ns1:PostTax>
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

PostTaxRequest postTaxRequest = new PostTaxRequest();

postTaxRequest.CompanyCode = "APITrialCompany";
postTaxRequest.DocType = DocumentType.SalesInvoice;
postTaxRequest.DocCode = "INV001";
postTaxRequest.Commit = false;
postTaxRequest.DocDate = DateTime.Parse("2014-01-01");
postTaxRequest.TotalTax = (decimal)14.27;
postTaxRequest.TotalAmount = 175;
postTaxRequest.NewDocCode = "INV001-1";

PostTaxResult postTaxResult = taxSvc.PostTax(postTaxRequest);
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

$postTaxRequest = new PostTaxRequest();
$postTaxRequest->setCompanyCode("APITrialCompany");
$postTaxRequest->setDocType("SalesInvoice");
$postTaxRequest->setDocCode("INV001");
$postTaxRequest->setDocDate("2014-01-01");
$postTaxRequest->setTotalAmount(175.00);
$postTaxRequest->setTotalTax(14.27);
$postTaxRequest->setCommit(false);

$postTaxResult = $taxSvc->postTax($postTaxRequest);
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

PostTaxRequest postTaxRequest = new PostTaxRequest();
Format formatter = new SimpleDateFormat("yyyy-MM-dd");
postTaxRequest.setDocCode("INV001");
postTaxRequest.setCompanyCode("APITrialCompany");
postTaxRequest.setDocType(DocumentType.SalesInvoice);
Date docDate = (Date)formatter.parseObject("2014-01-01");
postTaxRequest.setDocDate(docDate);
postTaxRequest.setTotalAmount(new BigDecimal("175.00"));
postTaxRequest.setTotalTax(new BigDecimal("14.27"));
postTaxRequest.setCommit(false);

PostTaxResult postTaxResult = taxSvc.postTax(postTaxRequest);
```

Input for PostTax for posting or committing a previously saved document.

**Commit:** bool, *optional*  
If set to True, AvaTax will Post and Commit the document in one call.

**CompanyCode:** string [25], *required*  
The client application company reference code.

**DocCode:** string [50], *required*  
The internal reference code (invoice number) used by the client application.

**DocDate:** date, *required*  
The Document Date, i.e. the date on the invoice, purchase order, etc.

**DocType:** DocumentType, *required*  
The original document's type, such as Sales Invoice or Purchase Invoice

**NewDocCode:** string [50], *optional*  
New Document Code for the document if desired.

**TotalAmount:** decimal, *required*  
The total amount (not including tax) for the document.

**TotalTax:** decimal, *required*  
The total tax for the document.

### PostTax Result

```xml
<PostTaxResult>
    <TransactionId>0</TransactionId>
    <ResultCode>Success</ResultCode>
    <DocId>48769272</DocId>
</PostTaxResult>
```

Result data returned from PostTax.

**DocId:** bigint as string  
The unique document ID assigned by AvaTax to the document modified. This value need only be retained for troubleshooting.

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
