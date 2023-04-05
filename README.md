

# FMS REST API Integration Documentation 

This documentation outlines the Freight Management System (FMS) Integration API, which allows you to manage the creation of consignments for shipments and track the status of your deliveries.

Note that this API does not include managing client data for shipments' destination. Customers must be onboarded into our system to have access to this client data and have the billing customer configured with their required routes. Once these steps have been completed, or already exist, the API can be provided as part of this process with the required access keys.


 The FMS Integration API uses JSON for data exchange and is accessible via the FMS API. All requests to the FMS Integration API must include the following headers:

Authorization: Your API `ClientId`  and `ClientSecret`.

Content-Type: application/json.

## License

The code is licensed to [Namlog](http://www.namlog.co.za/).


## Authentication

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

Before using the Integration API, you must obtain an API `ClientId` and `ClientSecret` from Namlog, which will be used to authenticate your requests, as part of the headers.

## API Endpoints

The following endpoints are available in the Integration API:

**GET ROUTES ENDPOINT**

To get the routes for a consignment, use the following API call:

**URL** : `/api/v{version}/Integrations/client/{integrationclientId}/routes`


**Method** : `GET`

**Auth required** : YES

**Permissions required** : YES

**Data constraints**
* Include the Client Secret and the Client Id in the Headers




The `integrationclientId` is provided as part of the API Key configuration.

`integrationclientId` : *integer*



Here's an example from a test integration client to get the routes for a consignment customer:

**Example** : `/api/v1/Integrations/client/1/routes`



## Success Response

```json
{
    "succeeded": true,
    "data": [
        {
            "billCustomerId": 28624,
            "billCustomer": "Alex (Test2)101",
            "routeId": 4907,
            "activeFlag": true,
            "fromTown": "*Johannesburg",
            "fromPCode": "2001 ",
            "toTown": "*Springbok",
            "toPCode": "8240 ",
            "courierId": "NLG       ",
            "cService": "SDS       "
        }, 
         {
            "billCustomerId": 28624,
            "billCustomer": "Alex (Test2)101",
            "routeId": 8323,
            "activeFlag": true,
            "fromTown": "*Johannesburg",
            "fromPCode": "2001 ",
            "toTown": "Vereeniging",
            "toPCode": "1930 ",
            "courierId": "NLG       ",
            "cService": "SDS       "
        },
        {
            "billCustomerId": 28624,
            "billCustomer": "Alex (Test2)101",
            "routeId": 54284,
            "activeFlag": true,
            "fromTown": "*Johannesburg",
            "fromPCode": "2001 ",
            "toTown": "East London",
            "toPCode": "5205 ",
            "courierId": "NLG       ",
            "cService": "ECO       "
        },
      
        {
            "billCustomerId": 28624,
            "billCustomer": "Alex (Test2)101",
            "routeId": 54285,
            "activeFlag": true,
            "fromTown": "*Johannesburg",
            "fromPCode": "2001 ",
            "toTown": "*Springbok",
            "toPCode": "8240 ",
            "courierId": "NLG       ",
            "cService": "ECO       "
        }
    ]
}
  ```

## Error Response

```json
{
    "succeeded": false,
    "message": "You are not Authorized",
    "data": false
}
  ```



**CREATE WAYBILL ENDPOINT**

The successfull response from the *Get Routes* api call has values needed to create a new waybill.

To create a waybill for a consignment, use the following API call:

**URL** : `/api/v{version}/Integrations/waybill`


**Method** : `POST`

**Auth required** : YES

**Permissions required** : YES

**Data constraints**
* Include the `ClientSecret` and the `ClientId` in the Headers
* The following fields with the data types are required for this request payload object

       
        wayBillNo: string. The New Waybill Number that needs to be created
        cService: string. From the Routes call
        courierId: string. From the Routes call
        depotId: int. Depot is default 1
        billCustomerId: int. From the routes 
        pickupCustomerId: int. This will be provided separately for now during onboarding
        routeId: int. The chosen route Id from the Routes call
        town: string.  toTown From the chosen Route
        postalCode: string. toPCode From the chosen Route        
        sendingCustomer : string.  The Billing Customer Name
        receivingCustomer : string. The Pickup  Customer Name
        billCust: int. billCustomerId from the routes 
        noOfParcels: int. Number of parcels to create
        barcode: string. Provide your Barcode
  


## Request 




The `integrationclientId` is provided as part of the API Key configuration process.





```json
{
    "integrationModel": {
      "cService":"SDS", 
      "courierId": "NLG", 
      "depotId": 1, 
      "billCustomerId": 28624, 
      "pickupCustomerId": 68633,
      "integrationClientId": 12, 
      "customers": [
        {
          "customerName": "Customer B",  
          "custRef": "", 
          "newCustReference": "", 
          "routeId": 8323,  
          "billCustomerId": 28624,
          "address": {
            "address1": "string",  
            "streetAddress": "string",  
            "town": "Vereeniging", 
            "postalCode": "1930" 
          },
          "contact": {
            "email": ""  
          },
          "waybills": [
            {
              "wayBillNo": "TEST_API_Integration", 
              "sendingCustomer": "Alex (Test2)101",  
              "receivingCustomer": "Customer B",  
              "routeId": 8323,  
              "country": "South Africa",
              "billCust":  28624, 
              "cService":"SDS", 
              "courierId": "NLG", 
              "depotId":  1, 
              "billCustomerId":  28624, 
              "pickupCustomerId": 68633, 
              "noOfParcels": 1, 
              "parcels": [
                {
                  "parcelTypeId": 0, 
                  "parcelType": "PARCEL", 
                  "dimms": 0,
                  "barcode": "string", 
                  "orderId": "string", 
                  "weight": 5, 
                  "pl": 0,
                  "ph": 0,
                  "pw": 0,
                  "verificationTypeId": 0 
                }
              ],
              "orders": [
                {
                  "waybillNo": "TEST_API_Integration",
                  "orderNo": "string",
                  "invoiceNo": "string"
                }
              ]
            }
          ]
        }
      ],
      "branch": 0  
    }
  }
```

## Success Response


```json
{
    "message": "Waybills created successfully.",
    "succeeded": true
}

  ```







The following request parameters are available for use in the FMS Integration API:

`CService`: The service type for the shipment.

`CourierId`: The ID of the courier for the shipment.

`DepotId`: The ID of the depot for the shipment.

`BillCustomerId`: The ID of the customer who will be billed for the shipment.

`PickupCustomerId`: The ID of the customer who will be picking up the shipment.

`IntegrationClientId`: The ID of the integration client.

Customers: An array of objects containing customer details, such as 
CustomerName, CustRef, RouteId, Address, Contact, Waybills, etc.
`branch`: An optional parameter that specifies the branch location for the shipment.

## Response Format ##

The FMS Integration API returns responses in JSON format. The response body contains a status code and a message describing the result of the request. If the request was successful, the response body may also include additional data, such as a list of customers or waybills.


## Error Responses

If an error occurs during the processing of a request, the FMS Integration API will return an error response with an appropriate HTTP status code and an error message describing the problem. Error responses will also include an error code to help you identify the specific issue.
The following error responses may be returned by the FMS Integration API:

**Condition** : If Account does not exist with `id` of provided `pk` parameter.

**Code** : `404 NOT FOUND`

**Content** : `{}`

### Or

**Condition** : If Account exists but Authorized User does not have required
permissions.

**Code** : `403 FORBIDDEN`

**Content** :

```json
{"detail": "You do not have permission to perform this action."}
```


### Or

**Condition** : If Account exists but Authorized User does not have required
permissions.

**Code** : `400 Bad Request`

**Content** :

```json
{
  "message": "The request could not be understood or was missing required parameters",
  "succeeded": false,
  "data": null
}
```
