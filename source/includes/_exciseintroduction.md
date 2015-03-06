# Excise API

The Avalara AvaTax Excise Web Service is a SOAP web service that is the external programmatic interface into the Avalara AvaTax Excise application.   It provides for a platform independent mechanism to obtain tax calculation information.  This document defines the object structure, and an introduction on how to consume the web service for use in customer programs.

At this time, Excise sample code/libraries are available in .NET only.

Please note the application name changes effective 7/31/2014:

 - Avalara Returns Excise replaces Zytax Compliance
 - Avalara AvaTax Excise replaces Zytax Determination
 - Avalara Government replaces Zytax Government

URLs

 - Development Authentication Service: <a href='https://psd.avalara.net/authenticationservice.asmx?wsdl' target="_blank">https://psd.avalara.net/authenticationservice.asmx?wsdl</a>
 - Development Tax Determination:  <a href='https://psd.avalara.net/determination/taxdetermination.asmx?wsdl' target="_blank">https://psd.avalara.net/determination/taxdetermination.asmx?wsdl</a>
 - User Acceptance Authentication Service: <a href='https://exciseua.avalara.net/authenticationservice.asmx?wsdl' target="_blank">https://exciseua.avalara.net/authenticationservice.asmx?wsdl</a>
 - User Acceptance Tax Determination: <a href='https://exciseua.avalara.net/determination/taxdetermination.asmx?wsdl' target="_blank">https://exciseua.avalara.net/determination/taxdetermination.asmx?wsdl</a>
 - Production Authentication Service: <a href='ttps://excise.avalara.net/authenticationservice.asmx?wsdl' target="_blank">https://excise.avalara.net/authenticationservice.asmx?wsdl</a>
 - Production Tax Determination: <a href='https://excise.avalara.net/determination/taxdetermination.asmx?wsdl' target="_blank">https://excise.avalara.net/determination/taxdetermination.asmx?wsdl</a>