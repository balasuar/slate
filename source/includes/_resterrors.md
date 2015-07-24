## Errors

### Message

> Error messages are presented in the following format:

```json
{
"ResultCode": "Error",
"Messages": [
{
"Summary": "Company not found.  Verify the CompanyCode.",
"Details": "APITrialCompany",
"RefersTo": "CompanyCode",
"Severity": "Error",
"Source": "Avalara.AvaTax.Services.Tax"}
]
}
```

Generic format for error messages in output objects. Errors are returned in the Message class. <a href="http://developer.avalara.com/api-docs/designing-your-integration/errors-and-outages/common-errors" target="_parent">See Error Lists</a>.

**Summary:** string [255]  
The message summary in short form.

**Details:** string [255]  
Description of the error or warning.

**RefersTo:** string [255]  
The data used during the request that caused the message to be generated.

**Severity:** enum as string [see below]  
Classifies severity of message. One of:

* Success
* Error
* Warning
* Exception

**Source:** string [255]  
The internal location that generated the message.