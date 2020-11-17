# Simple Payment Card Generator API
A payment card generator over rest/api for the purpose of automated testing when building ecommerce platforms, 
payment gateways, or simply any apps requiring a valid Luhn algorithm payment card number

## Introduction
The API repository currently only holds 20 BIN/IIS, but the program is able can generate 200 million
unique valid card number permutation.


##How TO
### Creating test payment card number
* Request new card number, with a POST request to https://szc14cspaa.execute-api.eu-west-1.amazonaws.com/Prod/api2/{your-account}/payment-card?id={unque-id} where {your-account} is your given account and passing a unique reference id
Example using a GUID as reference;
```bash
$ curl -X POST 'https://szc14cspaa.execute-api.eu-west-1.amazonaws.com/Prod/api2/my-tests/payment-card?id=0e9998d3-51aa-4ddc-8ab6-621aff5cd7b0' -i
```

The API will response with an HTTP 200
```
HTTP/2 200
date: Tue, 17 Nov 2020 14:37:13 GMT
content-type: application/json
content-length: 154
...
```

* On a successful request, the new card number can be retrieved with a GET request using the same unique id.
```bash
$ curl -X POST 'https://szc14cspaa.execute-api.eu-west-1.amazonaws.com/Prod/api2/my-tests/payment-card?id=0e9998d3-51aa-4ddc-8ab6-621aff5cd7b0' -i
```

Example response below;
```
HTTP/2 200
date: Tue, 17 Nov 2020 14:51:57 GMT
content-type: application/json
content-length: 176

{"number":"6304 9062 4709 6405","brand":"Mastercard","type":"Debit","issuer":"Bank Of Ireland","country":"Ireland","attributes":{"uuid":"0e9998d3-51aa-4ddc-8ab6-621aff5cd7b0"}}
```


### Adding custom meta data
* It is often desirable to store metadata associated with the card number, the payment card attributes payload can be amended with a PUT request. Below a PUT example to associate a name with the payment card.
```bash$
$ curl -X PUT 'https://szc14cspaa.execute-api.eu-west-1.amazonaws.com/Prod/api2/my-tests/payment-card?id=0e9998d3-51aa-4ddc-8ab6-621aff5cd7b0' -H 'Content-Type: application/json' -d '{"Name":"John Smith"}' -i

$ curl -X GET 'https://szc14cspaa.execute-api.eu-west-1.amazonaws.com/Prod/api2/my-tests/payment-card?id=0e9998d3-51aa-4ddc-8ab6-621aff5cd7b0'
```
Updated response
```
{"number":"6304 9062 4709 6405","brand":"Mastercard","type":"Debit","issuer":"Bank Of Ireland","country":"Ireland","attributes":{"uuid":"0e9998d3-51aa-4ddc-8ab6-621aff5cd7b0","Name":"John Smith"}}%
```
