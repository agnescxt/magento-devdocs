---
group: get-started
subgroup: 20_REST
title: 响应和状态码
menu_title: 响应和状态码
menu_order: 3

version: 2.0
github_link: get-started/gs-web-api-response.md
redirect_from: /guides/v1.0/get-started/gs-web-api-response.html
---

## REST responses {#rest-responses}

Each web {% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %} call returns a HTTP status code and a response payload. When an error occcurs, the response body also returns an error message.

### HTTP status codes {#http-status-codes}

Each {% glossarytooltip 377dc0a3-b8a7-4dfa-808e-2de37e4c0029 %}web API{% endglossarytooltip %} call returns an HTTP status code that reflects the result of a request:

HTTP code | Meaning | Description
--- | --- | ---
200 | Success | The framework returns HTTP 200 to the caller upon success.
400 | Bad Request | If service implementation throws either `Magento_Service_Exception` or its derivative, the framework returns a HTTP 400 with a error response including the service-specific error code and message. This error code could indicate a problem such as a missing required parameter or the supplied data didn't pass validation.
401 | Unauthorized | The caller was not authorized to perform the request. 例如， the request included an invalid token or a user with customer permissions attempted to access an object that requires administrator permissions.
403 | Forbidden | Access is not allowed for reasons that are not covered by error code 401.
404 | 否t found | The specified REST endpoint does not exist. The caller can try again.
405 | 否t allowed | A request was made of a resource using a method that is not supported by that resource. 例如， using GET on a form which requires data to be presented via POST, or using PUT on a read-only resource.
406 | 否t acceptable | The requested resource is only capable of generating content that is not acceptable according to the Accept headers sent in the request.
500 | System Errors | If service implementation throws any other {% glossarytooltip 53da11f1-d0b8-4a7e-b078-1e099462b409 %}exception{% endglossarytooltip %} like network errors, database communication, framework returns HTTP 500.


### Response payload {#response-payload}

POST, PUT, and GET web API calls return a response payload. This payload is a JSON- or XML-formatted response body. The `Accept: application/<FORMAT>` header in the request determines the format of the response body, where `FORMAT` is either `json`或`xml`.

A successful DELETE call returns `true`. An unsuccessful DELETE call returns a payload similar to the other calls.

The response payload depends on the call.
例如， a `GET /V1/customers/:customerId` call returns the following payload:

{% highlight json %}
{
    "customers": {
        "customer": {
            "email": "user@example.com",
            "firstname": "John",
            "lastname": "Doe"
        },
        "addresses": [
            {
                "defaultShipping": true,
                "defaultBilling": true,
                "firstname": "John",
                "lastname": "Doe",
                "region": {
                    "regionCode": "CA",
                    "region": "California",
                    "regionId": 12
                },
                "postcode": "90001",
                "street": ["Zoe Ave"],
                "city": "Los Angeles",
                "telephone": "555-000-00-00",
                "countryId": "US"
            }
        ]
    }
}
{% endhighlight %}

This JSON-formatted response body includes a `customer` object with the customer email, first name, and last name, and customer address information. The information in this response body shows account information for the specified customer.

### Error format {#error-format}
When an error occurs, the response body contains an error code, error message, and optional parameters.

Part | Description
--- | --- | ---
`code` | The status code representing the error.
`message` | The message explaining the error.
`parameters` | 可选. An array of attributes used to generate a different and/or localized error message for the client.

As an example, Magento returns a `code` of `400` and the following `message` when an invalid `sku` value is specified in the call `PUT V1/products/:sku`.

{% highlight json %}
{
  "message": "Invalid product data: %1",
  "parameters": [
    "Invalid attribute set entity type"
  ]
}
{% endhighlight %}
