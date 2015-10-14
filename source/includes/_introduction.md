# Introduction

> As you scroll down in this document, you'll see code samples in this column. You can select the language for the code samples with the tabs at the top of the column.

The <a href="#avatax-rest-api" target="_self">**Avalara AvaTax**</a> APIs allow you to connect your web cart or accounting software to realtime tax calculation and address validation services. You can just retrieve tax amounts, but your transactions can also be recorded for reporting and tax filing. We have a <a href="#avatax-rest-api">RESTful API</a>, a <a href="#avatax-soap-api">SOAP API</a>, and <a href="http://developer.avalara.com/api-docs/api-sample-code" target="_parent">class wrappers (adapters)</a> for a variety of languages to assist in calling the web service. Sign up for a <a href='http://developer.avalara.com/getting-started'>free trial account</a> to get started.

The <a href="#taxrates-api">**Avalara TaxRates**</a> REST API provides an easy way for developers to use sales tax rates in their project. Our API is powered by our tax rule content, and rates are updated as tax rules change to stay current. You can use this API to get the sales tax rate for a five digit zip code in the United State or get the sales tax rate for a specific street address in the United States. <a href="http://taxratesapi.avalara.com/" target="_parent">Register</a> for an API Key to get started.

The <a href="#excise-api">**Avalara AvaTax Excise**</a> API is a SOAP web service that is the external programmatic interface into the Avalara AvaTax Excise application.   It provides for a platform independent mechanism to obtain tax calculation information.  This document defines the object structure, and an introduction on how to consume the web service.

**Please Note:** Future updates to our API may introduce new fields. We *highly* recommend building any validation of returned data with tolerance for unexpected fields, such as logging a warning instead of returning an error.
