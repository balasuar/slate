## CancelTax

Voids or deletes and existing transaction record from the AvaTax system.

##### URL and Method

`POST /1.0/tax/cancel`

Development: https://development.avalara.net/1.0/tax/cancel  
Production:	https://avatax.avalara.net/1.0/tax/cancel
    
<aside class='notice'>
    Note that xml-encoded requests should use the same URL (`POST /1.0/tax/cancel`), but should set the Content-Type header to `text/xml`.
</aside>

##### Headers

**Authorization:** header, *required*  
In the format "Basic [account number]:[license key]" encoded to <a href="http://en.wikipedia.org/wiki/Base64" target="_parent">Base64</a>, as per <a href="http://en.wikipedia.org/wiki/Basic_access_authentication" target="_parent">basic access authentication</a>.  
e.g.: `Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=`

**Content Type:** header, *required*  
Standard content type header, indicating the content type of the request content. Either `text/json` or `text/xml`.

**Content Length:** header, *required*  
Standard content length header, indicating the size of the request content.

### CancelTaxRequest

```shell
curl --user 1234567890:A1B2C3D4E5F6G7H8 \
--header "Content-Type: text/json" \
--data @/Docs/cancelTaxRequest.json \
"https://development.avalara.net/1.0/tax/cancel"

{
"CompanyCode":"APITrialCompany",
"DocType":"SalesInvoice",
"DocCode":"INV001",
"CancelCode":"DocVoided"
}
```

```csharp
var cancelTaxRequest = 
	new CancelTaxRequest{
	  CompanyCode = "APITrialCompany",
	  DocType = DocumentType.SalesInvoice,
	  DocCode = "INV001",
	  CancelCode = CancelCode.DocVoided
};

//Convert the request to XML
XmlSerializerNamespaces namesp = new XmlSerializerNamespaces();
namesp.Add("", ""); 
XmlWriterSettings settings = new XmlWriterSettings();
settings.OmitXmlDeclaration = true;
XmlSerializer x = new XmlSerializer(cancelTaxRequest.GetType());
StringBuilder sb = new StringBuilder();
x.Serialize(XmlTextWriter.Create(sb, settings), cancelTaxRequest, namesp);
XmlDocument doc = new XmlDocument();
doc.LoadXml(sb.ToString());

//Call the service
Uri address = new Uri(serviceURL + "/1.0/tax/cancel");
HttpWebRequest request = WebRequest.Create(address)as HttpWebRequest;

//Add Authorization header
request.Headers.Add(
	HttpRequestHeader.Authorization, 
	"Basic " + Convert.ToBase64String(ASCIIEncoding.ASCII.GetBytes(accountNumber + ":" + licenseKey)));
request.Method = "POST";
request.ContentType = "text/xml";
request.ContentLength = sb.Length;
Stream newStream = request.GetRequestStream();
newStream.Write(ASCIIEncoding.ASCII.GetBytes(sb.ToString()), 0, sb.Length);

WebResponse response = request.GetResponse();
```

```java
CancelTaxRequest cancelTaxRequest = new CancelTaxRequest();
cancelTaxRequest.CompanyCode = "APITrialCompany";
cancelTaxRequest.DocType = TaxSvc.DocType.SalesInvoice;
cancelTaxRequest.DocCode = "INV001";
cancelTaxRequest.CancelCode = CancelCode.DocVoided;

//Create URL
String target = serviceURL + "/1.0/tax/cancel";
URL url;
HttpURLConnection conn;

//Connect to URL with authorization header, request content.
url = new URL(target);
conn = (HttpURLConnection)url.openConnection();
conn.setRequestMethod("POST");
conn.setDoOutput(true);
conn.setDoInput(true);
conn.setUseCaches(false);
conn.setAllowUserInteraction(false);

//Create auth content
String encoded = "Basic " + new String(Base64.encodeBase64((accountNumber + ":" + licenseKey).getBytes()));
//Add authorization header
conn.setRequestProperty("Authorization", encoded);
conn.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");

ObjectMapper mapper = new ObjectMapper();
mapper.setSerializationInclusion(Include.NON_NULL);
//Tells the serializer to only include
//those parameters that are not null
String content = mapper.writeValueAsString(cancelTaxRequest);

//Uncomment to see the content of the
//request object
//System.out.println(content);
conn.setRequestProperty("Content-Length", Integer.toString(content.length()));

DataOutputStream wr = new DataOutputStream(conn.getOutputStream());
wr.writeBytes (content);
wr.flush ();
wr.close ();

conn.disconnect();
CancelTaxResponse res = mapper.readValue(conn.getInputStream(), CancelTaxResponse.class);
```

```php
<?php
$cancelTaxRequest = new CancelTaxRequest();
$cancelTaxRequest->setCompanyCode("APITrialCompany");
$cancelTaxRequest->setDocType(DocumentType::$SalesInvoice);		
$cancelTaxRequest->setDocCode("INV001");		
$cancelTaxRequest->setCancelCode(CancelCode::$DocVoided);

$url = $serviceURL."/1.0/tax/cancel";
$curl = curl_init($url);
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($curl, CURLOPT_USERPWD, $accountNumber.":".$licenseKey);

curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
curl_setopt($curl, CURLOPT_POST, true);
curl_setopt($curl, CURLOPT_POSTFIELDS, json_encode($cancelTaxRequest)); 
$curl_response = curl_exec($curl);
curl_close($curl);

CancelTaxResult::parseResult($curl_response);
?>
```

**CompanyCode:** string [25], *required*  
Client application company reference code.  Not required if the document is identified by DocId.

**DocType:** string, *required*  
Value describing what type of tax document is being cancelled. One of:  

* SalesInvoice
* ReturnInvoice
* PurchaseInvoice  

Not required if the document is identified by DocId.

**DocCode:** string [50], *required*  
Client application identifier describing this tax transaction (i.e. invoice number, sales order number, etc.).  Not required if the document is identified by DocId.

**CancelCode:** string, *required*  
The reason for cancelling the tax record. 

* Unspecified
* PostFailed
* DocDeleted
* DocVoided
* AdjustmentCancelled

For more information, see <a href="http://developer.avalara.com/api-docs/designing-your-integration/canceltax" target="_parent">Voiding Documents</a>.

**DocId:** string, *optional*  
Avatax-assigned unique Document Id, can be used in place of DocCode, DocType, and CompanyCode

### CancelTaxResult

```json
{
"CancelTaxResult": {
"TransactionId": 437966608,
"ResultCode": "Success",
"DocId": "34067366"}
}
```

**TransactionId:** string  
The unique numeric identifier of the API operation assigned by the AvaTax service.

**DocId:** string  
The unique numeric identifier (Document ID) assigned to the tax document in question by the AvaTax Service.

**ResultCode:** enum as string [see below]  
Classifies severity of message. One of:

* Success
* Error
* Warning
* Exception

**Messages:** <a href='#errors'>Message[]</a>
Human-readable description of any warning, error, or exception that occured.
