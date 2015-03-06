## Authentication

The Excise Platform Authentication Web Service is a SOAP/XML web service that is the external programmatic interface for authentication against the Excise Platform.   It provides for a platform independent mechanism to obtain an authorization token which can be used when calling other web services.  This document defines the object structure, and an introduction on how to consume the web service for use in customer programs.  

Web service authentication in the Excise platform has 3 basic forms:

- Anonymous: no authentication required to call a web service
- Forms: require a forms authentication cookie to be passed with each web service call
- NTLM: use the built in windows authentication to restrict access to the web service

### Forms Authentication
Forms authentication requires calling the AuthenticationService.asmx before calling other web services.  This function returns an ASP.Net Forms authentication cookie with the response which needs to be passed along with each future web service call.


**URLs**

- Development Authentication Service:  <a href='https://psd.avalara.net/authenticationservice.asmx?WSDL' target="_blank">https://psd.avalara.net/authenticationservice.asmx?WSDL </a>
- User Acceptance Authentication Service:  <a href='https://exciseua.avalara.net/authenticationservice.asmx?WSDL' target="_blank">https://exciseua.avalara.net/authenticationservice.asmx?WSDL</a>
- Production Authentication Service:  <a href='https://excise.avalara.net/authenticationservice.asmx?WSDL' target="_blank">https://excise.avalara.net/authenticationservice.asmx?WSDL</a>

#### Login Request

```csharp

if (_authCookies != null)
{   //Already connected, try to reuse connection.  
}
else
{
    AuthenticationService auth = new AuthenticationService();
    auth.CookieContainer = new System.Net.CookieContainer();   //Connecting...
    if (auth.Login("username", "password", "Determination Oil Company"))
    {
        _authCookies = auth.CookieContainer;         //Connected.
    }
    else
    {
        _ authCookies = null;         //failed!
    }
}
```

```shell
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <Login xmlns="http://taxes.services.fuelquest.com/">
      <userName>username</userName>
      <password>password</password>
      <companyName>Determination Oil Company</companyName>
    </Login>
  </soap:Body>
</soap:Envelope>
```

> The above command returns XML structured like this:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <LoginResponse xmlns="http://taxes.services.fuelquest.com/">
      <LoginResult>true</LoginResult>
    </LoginResponse>
  </soap:Body>
</soap:Envelope>
```

Authenticates the user against the configured membership provider and verifies they have access to the specified company.  If successful, an authentication token is return as a cookie.

**userName:** string, *required*
The user's login

**password:** string, *required*
The user's password

**companyName:** string, *required*
The name of the company to use for the remainder of the session.

#### Login Response

**LoginResult:** boolean

### Logout

> Logging out calls the same endpoint with the 'Logout' SOAP method, and an empty request body.

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <Logout xmlns="http://taxes.services.fuelquest.com/" />
  </soap:Body>
</soap:Envelope>
```

> The above command returns XML structured like this:

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <LogoutResponse xmlns="http://taxes.services.fuelquest.com/" />
  </soap:Body>
</soap:Envelope>
```

Logs the current user out of the system and clears their authentication cookie.

### NTLM Authentication
NTLM authentication does not require calling the AuthenticationService.asmx before calling other web services.  At the beginning of the call to the web service, the user is authenticated, and if successful, the call is processed normally.  The web service will attach a Forms Authentication cookie to the response to improve performance in subsequent calls, but it is not required to use the cookie (the caller can be re-authenticated each time).  The client must keep the TCP connection alive in between calls in order to re-use the cookie while configured to use NTLM.  Each new TCP connection will require re-authentication.

## Load Locations?
```csharp
    public static void InvokeLocationsImport()
    {
        Login();

        if (_authCookies != null)
        {
            _mi.CookieContainer = _authCookies;

            List<Location_2_0_031> locations = new List<Location_2_0_031>();

            Location_2_0_031 location = new Location_2_0_031();
            location.Description = "ZZ Oil";
            location.EffectiveDate = new DateTime(2009, 1, 1);
            location.Address1 = "123 Main St.";
            location.Address2 = "Suite B.";
            location.City = "Green Bay";
            location.Jurisdiction = "WI";
            location.CountryCode = "USA";
            location.PostalCode = "54313";
            location.OutsideCityLimitInd = YesNo.No;

            locations.Add(location);

            LocationImportResultSummary_2_0_031 result =
                _mi.ImportLocations(locations.ToArray(), "Determination Oil Company", 100, 100, 100, true);

            Dumper.Dump("result", result);
        }
    }
```