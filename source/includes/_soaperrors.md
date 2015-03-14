## Errors

###Message

```xml
<ResultCode>Error</ResultCode>
<Messages>
    <Message Name="CompanyNotFoundError">
        <Summary>Company not found.  Verify the CompanyCode.</Summary>
        <Details>APITrialCompany</Details>
        <HelpLink>http://www.avalara.com</HelpLink>
        <RefersTo>CompanyCode</RefersTo>
        <Severity>Error</Severity>
        <Source>Avalara.AvaTax.Services.Tax</Source>
    </Message>
</Messages>
```

Generic format for error messages in output objects. Errors are returned in the Message class. <a href="http://developer.avalara.com/api-docs/designing-your-integration/errors-and-outages/common-errors" target="_parent">See Error Lists</a>.

**Summary:** string [int MAX_VALUE]  
The message summary in short form.

**Details:** string [int MAX_VALUE]  
Description of the error or warning.

**RefersTo:** string [int MAX_VALUE]  
The data used during the request that caused the message to be generated.

**HelpLink:** string [int MAX_VALUE]  
Always "http://www.avalara.com"

**Severity:** enum as string [see below]  
Classifies severity of message. One of:

* Success
* Error
* Warning
* Exception

**Source:** string [int MAX_VALUE]  
The internal location that generated the message.