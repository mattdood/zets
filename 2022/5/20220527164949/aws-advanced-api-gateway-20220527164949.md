---
path: '/2022/5/aws-advanced-api-gateway-20220527164949'
title: 'aws advanced api gateway'
date: '20220527164949'
category: 'aws'
tags: ['developer associate', 'certification', 'api gateway']
---

# aws advanced api gateway
API Gateway has many advanced usage patterns.

## Importing APIs into API Gateway
* Importing API Definition Files
    * You can use the API Gateway Import API feature to import an API using
    a definition file
* Supported protocols
    * OpenAPI (Swagger) is supported
* Create new and update existing APIs
    * You can use an OpenAPI definition file to create a new API or update an existing
    API endpoint

## Legacy protocols
API Gateway supports legacy API protocols like SOAP (Simple Object Access Protocol)
that returns in XML format rather than JSON.

* API Gateway can be configured as a SOAP web service passthrough that will pass
the XML responses through the gateway
* You can also use API Gateway to transform the XML response into JSON

## Exam tips
* You can import APIs using external definition files, ex: OpenAPI (Swagger)
* When using legacy applications you can configure API Gateway to handle XML
from SOAP responses either as passthrough or transforming to JSON

