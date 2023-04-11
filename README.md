

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
            "routeId": 7941,
            "activeFlag": true,
            "fromTown": "*Johannesburg",
            "fromPCode": "2001 ",
            "toTown": "UPINGTON",
            "toPCode": "8801 ",
            "courierId": "NLG       ",
            "cService": "ONX       "
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




**GET NON-BILLING CUSTOMERS ENDPOINT**

To choose the correct delivery customer, the route must be chosen first. 
This call will provide a list of customers linked to the billing customer. From this list, the delivery customer should exist that meets the following criteria:
  The selected delivery customer bcentreId and toPCode from the chosen route must match

o get the routes for a consignment, use the following API call:

**URL** : `/api/v{version}//api/v{version}/Integrations/{id}/nonbillcustomers`


**Method** : `GET`

**Auth required** : YES

**Permissions required** : YES

**Data constraints**
* Include the Client Secret and the Client Id in the Headers


The `id` is the billingCustomerId from the chosen route in the *Get Routes* api call response.

`id` : *integer*



Here's an example from a test integration client to get the non-billing customers:

**Example** : `/api/v1/Integrations/28624/nonbillcustomers`

## Success Response

```json
{
    "succeeded": true,
    "data": [
        {
            "customerId": 69709,
            "name": "UPINTONITE",
            "custMainId": 28624,
            "vatno": "",
            "importVatno": "",
            "exportCode": "",
            "updCust": true,
            "codflag": false,
            "lastModified": "2020-07-11T14:46:20.12",
            "bcentreId": "8801 ",
            "isBillCustomer": false,
            "sendingBranch": false,
            "customerStatusId": 4,
            "bcentre": "UPINGTON",
            "displayText": "UPINTONITE - UPINGTON",
            "customerAddressId": 0,
            "suburbId": 0,
            "townId": 0,
            "provinceId": 0,
            "countryId": 0,
            "customerAddressTypeId": 0,
            "custProvinceID": 0,
            "customerAddress": {
                "customerAddressId": 342564,
                "lat": -33.7392000000,
                "long": 25.4224000000,
                "suburbId": 1,
                "townId": 731,
                "provinceId": 5,
                "countryId": 0,
                "customerId": 69709,
                "customerAddressTypeId": 1,
                "address1": "10 Upington St",
                "address2": "Uitenhage Upper Central ,South Africa",
                "address3": "",
                "custMainId": 28624
            }
        },
        {
            "customerId": 156054,
            "name": "Test Customer",
            "custMainId": 28624,
            "createDate": "2020-12-01T00:00:00",
            "lastModified": "2022-11-25T10:23:05.96",
            "bcentreId": "2001 ",
            "isBillCustomer": false,
            "customerStatusId": 4,
            "bcentre": "*Johannesburg",
            "displayText": "Test Customer - *Johannesburg",
            "customerAddressId": 0,
            "suburbId": 0,
            "townId": 0,
            "provinceId": 0,
            "countryId": 0,
            "customerAddressTypeId": 0,
            "custProvinceID": 0,
            "customerAddress": {
                "customerAddressId": 410419,
                "lat": -26.1548390000,
                "long": 28.1695910000,
                "suburbId": 10400,
                "townId": 452,
                "provinceId": 1,
                "countryId": 1,
                "postalCode": "1614",
                "customerId": 156054,
                "customerAddressTypeId": 1,
                "verified": true,
                "address1": "Address1",
                "address2": "Corobrik Street",
                "address3": "",
                "address4": "Meadowdale",
                "custMainId": 28624
            }
        },
        {
            "customerId": 45065,
            "name": "Capie",
            "custMainId": 28624,
            "vatno": "",
            "importVatno": "",
            "exportCode": "",
            "updCust": true,
            "codflag": false,
            "lastModified": "2020-07-11T14:46:22.913",
            "bcentreId": "8000 ",
            "isBillCustomer": false,
            "sendingBranch": false,
            "customerStatusId": 4,
            "bcentre": "*Cape Town",
            "displayText": "Capie - *Cape Town",
            "customerAddressId": 0,
            "suburbId": 0,
            "townId": 0,
            "provinceId": 0,
            "countryId": 0,
            "customerAddressTypeId": 0,
            "custProvinceID": 0,
            "customerAddress": {
                "customerAddressId": 364302,
                "lat": -33.9251000000,
                "long": 18.4240000000,
                "suburbId": 1,
                "townId": 57,
                "provinceId": 3,
                "countryId": 0,
                "customerId": 45065,
                "customerAddressTypeId": 1,
                "address1": "17 Darling St",
                "address2": "Foreshore ,South Africa",
                "address3": "8000",
                "custMainId": 28624
            }
        },
        {
            "customerId": 150205,
            "name": "Clifford Customer ",
            "custMainId": 28624,
            "pcentreId": 0,
            "vatno": "------------------",
            "importVatno": "",
            "exportCode": "",
            "glaccNo": "",
            "updCust": true,
            "codflag": false,
            "createDate": "2020-07-14T00:00:00",
            "lastModified": "2020-08-21T13:01:17.467",
            "bcentreId": "8240 ",
            "isBillCustomer": false,
            "customerStatusId": 4,
            "bcentre": "*Springbok",
            "displayText": "Clifford Customer  - *Springbok",
            "customerAddressId": 0,
            "suburbId": 0,
            "townId": 0,
            "provinceId": 0,
            "countryId": 0,
            "customerAddressTypeId": 0,
            "custProvinceID": 0,
            "customerAddress": {
                "customerAddressId": 404610,
                "lat": -26.1548390000,
                "long": 28.1695910000,
                "suburbId": 10400,
                "townId": 390,
                "provinceId": 1,
                "countryId": 2,
                "postalCode": "1614",
                "customerId": 150205,
                "customerAddressTypeId": 1,
                "verified": true,
                "address1": "1 Corobrik Street",
                "address2": "Namlog",
                "address3": "Namlog",
                "address4": "Meadowdale",
                "custMainId": 28624
            }
        },
        {
            "customerId": 196383,
            "name": "ProdCust",
            "custMainId": 28624,
            "createDate": "2023-03-07T15:14:44.953",
            "createUser": 3335,
            "lastModified": "2023-03-07T15:14:44.953",
            "lastModifiedUserId": 3335,
            "bcentreId": "2001 ",
            "isBillCustomer": false,
            "customerStatusId": 4,
            "bcentre": "*Johannesburg",
            "displayText": "ProdCust - *Johannesburg",
            "customerAddressId": 0,
            "suburbId": 0,
            "townId": 0,
            "provinceId": 0,
            "countryId": 0,
            "customerAddressTypeId": 0,
            "custProvinceID": 0,
            "customerAddress": {
                "customerAddressId": 450157,
                "suburbId": 4747,
                "townId": 931,
                "provinceId": 1,
                "countryId": 1,
                "postalCode": "",
                "customerId": 196383,
                "customerAddressTypeId": 1,
                "address1": "AddressTest",
                "activeFlag": true,
                "custMainId": 28624
            }
        },        
        {
            "customerId": 66078,
            "name": "Windhoek Distributors",
            "custMainId": 28624,
            "vatno": "",
            "importVatno": "",
            "exportCode": "",
            "updCust": true,
            "codflag": false,
            "lastModified": "2020-07-11T14:46:20.6",
            "bcentreId": "n015 ",
            "isBillCustomer": false,
            "sendingBranch": false,
            "customerStatusId": 4,
            "bcentre": "*Windhoek",
            "displayText": "Windhoek Distributors - *Windhoek",
            "customerAddressId": 0,
            "suburbId": 0,
            "townId": 0,
            "provinceId": 0,
            "countryId": 0,
            "customerAddressTypeId": 0,
            "custProvinceID": 0,
            "customerAddress": {
                "customerAddressId": 346108,
                "lat": 0.0000000000,
                "long": 0.0000000000,
                "suburbId": 1,
                "townId": 1,
                "provinceId": 10,
                "countryId": 0,
                "customerId": 66078,
                "customerAddressTypeId": 1,
                "address1": "",
                "address2": "",
                "custMainId": 28624
            }
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
* The following fields with the data types are required for this request payload object, using the example chosen route:

       
        wayBillNo: string. The New Waybill Number that needs to be created
        cService: string. From the Routes call
        courierId: string. From the Routes call
        depotId: int. Depot is default 1
        billCustomerId: int. From the chosen routes 
        pickupCustomerId: int. This will be in the GET NON-BILLING CUSTOMERS response. 
        The customerId will be from a matching customer using "fromTown" and "fromPCode" of the chosen route. 
        e.g. customerId 196383 has a "bcentreId": "2001" from the chosen routeId: 7941
        routeId: int. The chosen route Id from the Get Routes call
        town: string.  toTown From the chosen Route
        postalCode: string. toPCode From the chosen Route. This must match the delivery customer "bcentreId", in this example. 8801, for customerId 69709.         
        sendingCustomer : string.  The Billing Customer Name
        receivingCustomer : string. The delivery Customer Name
        billCust: int. billCustomerId from the routes 
        noOfParcels: int. Number of parcels to create
        barcode: string. Provide your Barcode
  




    ```json
      {         //Chosen  Route
                "billCustomerId": 28624,
                "billCustomer": "Alex (Test2)101",
                "routeId": 7941,
                "activeFlag": true,
                "fromTown": "*Johannesburg",
                "fromPCode": "2001 ",
                "toTown": "UPINGTON",
                "toPCode": "8801 ",
                "courierId": "NLG       ",
                "cService": "ONX       "
            }

    ```

## Request 




The `integrationclientId` is provided as part of the API Key configuration process.





```json
{
    "integrationModel": {
      "cService":"ONX", 
      "courierId": "NLG", 
      "depotId": 1, 
      "billCustomerId": 28624, 
      "pickupCustomerId": 196383, 
      "integrationClientId": 1, 
      "customers": [
        {
          "customerName": "UPINTONITE",  
          "custRef": "", 
          "newCustReference": "", 
          "routeId": 7941,  
          "billCustomerId": 28624,
          "address": {
            "address1": "10 Upington St",  
            "streetAddress": "Uitenhage Upper Central ,South Africa",  
            "town": "UPINGTON", 
            "postalCode": "8801" 
          },
          "contact": {
            "email": ""  
          },
          "waybills": [
            {
              "wayBillNo": "TEST_API_Integration_3", 
              "sendingCustomer": "Alex (Test2)101",  
              "receivingCustomer": "UPINTONITE",  
              "routeId": 7941,  
              "country": "South Africa",
              "billCust":  28624, 
              "cService":"ONX", 
              "courierId": "NLG", 
              "depotId":  1, 
              "billCustomerId":  28624, 
              "pickupCustomerId": 196383, 
              "noOfParcels": 1, 
              "parcels": [
                {
                  "parcelTypeId": 0, 
                  "parcelType": "PARCEL", 
                  "dimms": 0,
                  "barcode": "TestAlexAPI", 
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
                  "waybillNo": "TEST_API_Integration_3",
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
