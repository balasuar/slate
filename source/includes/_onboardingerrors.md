## Errors
```plaintext
400 (Bad Request)
Content-Type: application/json
```

```json
{
    "Message": "Cannot fetch location.",
    "Result": "Location could not be fetched.",
    "Status": "Error"
}
```
```xml
<ErrorResponse>
    <Message type="string">Cannot fetch location.</Message>
    <Result type="string">Location could not be fetched.</Result>
    <Status type="string">Error</Status>
</ErrorResponse>
```

The Onboarding API uses the following error codes and messages:

Error Code | Message 
---------- | ------- 
401 | Invalid credentials
400 | Invalid content type.
404 | Resource not found.
401 | Access denied: User does not have permission to use OnBoarding API
400 | User already exists in AvaTax. Please try again with a different Email value.
400 | PhoneNumber length must be between 1 and 25 characters.
400 | CompanyCode length must be between 1 and 25 characters.
400 | The CompanyName field is required.
400 | State length must be between 2 and 2 characters.
400 | Zip length must be between 5 and 10 characters.
405 | Invalid operation
400 | Encountered unexpected character '<'.
400 | Error while creating company. Details: This is a duplicate of an existing CompanyCode and cannot be saved.


If an error is encountered during processing, an error message is included in the response. If an array of items is being processed and any element causes an error, the response status code will be 400. In this case, some elements may still have processed successfully.


```json
{
    "Message": "Atleast one of the locations could not be created.",
    "Result": {
        "__type": "AvaTaxCompanyLocation:#AvaTaxSelfProcLib.Models",
        "CompanyLocations": [
            {
                "City": "Bainbridge Island",
                "Country": "US",
                "Line1": "9, Winslow way",
                "Line2": "",
                "Line3": "",
                "State": "WA",
                "Zip": "98110",
                "AddressCategory": "MAINOFFICE",
                "AddressType": "LOCATION",
                "Description": "Testing",
                "EndDate": "05-31-2016",
                "ErrorIfAny": "",
                "IsDefault": "true",
                "LocationCode": "Loc11",
                "LocationId": "87630",
                "StartDate": "05-31-2014"
            },
            {
                "City": "Seattle",
                "Country": "US",
                "Line1": "15, Main Road",
                "Line2": "",
                "Line3": "",
                "State": "WA",
                "Zip": "98110",
                "AddressCategory": "WAREHOUSE",
                "AddressType": "LOCATION",
                "Description": "Testing",
                "EndDate": "05-31-2017",
                "ErrorIfAny": "This is a duplicate of an existing CompanyLocation and cannot be saved.",
                "IsDefault": "false",
                "LocationCode": "Loc2",
                "LocationId": "",
                "StartDate": "05-31-2014"
            }
        ]
    },
    "Status": "Error"
}

```

```xml
<CreateNexusResponse 
    xmlns="https://onboardingapi.avalara.com/DATA/V1" 
    xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <Message>Atleast one of the Nexuses could not be created.</Message>
    <Result i:type="a:AvaTaxNexusInformation" 
        xmlns:a="http://schemas.datacontract.org/2004/07/AvaTaxSelfProcLib.Models">
        <a:CreatedNexus>
            <a:Nexus>
                <a:CompanyId>253105</a:CompanyId>
                <a:Country>US</a:Country>
                <a:EffDate i:nil="true"></a:EffDate>
                <a:EndDate i:nil="true"></a:EndDate>
                <a:ErrorIfAny>
&#xD;Error: Nexus NOT saved for: CALIFORNIA Details: This is a duplicate of an existing Nexus and cannot be saved.</a:ErrorIfAny>
                <a:JurisName i:nil="true"></a:JurisName>
                <a:JurisType i:nil="true"></a:JurisType>
                <a:LocalNexusType i:nil="true"></a:LocalNexusType>
                <a:NexusId>0</a:NexusId>
                <a:NexusType i:nil="true"></a:NexusType>
                <a:State>CA</a:State>
            </a:Nexus>
            <a:Nexus>
                <a:CompanyId>253105</a:CompanyId>
                <a:Country>US</a:Country>
                <a:EffDate>2014-06-30</a:EffDate>
                <a:EndDate>9999-12-31</a:EndDate>
                <a:ErrorIfAny i:nil="true"></a:ErrorIfAny>
                <a:JurisName>MAINE</a:JurisName>
                <a:JurisType>STA</a:JurisType>
                <a:LocalNexusType>Selected</a:LocalNexusType>
                <a:NexusId>10686317</a:NexusId>
                <a:NexusType>NonVolunteer</a:NexusType>
                <a:State>ME</a:State>
            </a:Nexus>
        </a:CreatedNexus>
    </Result>
    <Status>Error</Status>
</CreateNexusResponse>
```
