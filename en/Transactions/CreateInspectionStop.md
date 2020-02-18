# Create Stop (Inspection Request)

Creates a New Inspection Stop.

**URL** : `/api/InboundStop/Create`

**Method** : `POST`

**Auth **Required\*\*\*\* : YES

**Headers**

| Key           | Value                                                           |
| ------------- | --------------------------------------------------------------- |
| Content-Type  | application/json                                                |
| Accept        | application/json                                                |
| Authorization | Bearer + AccessToken received from Authenticate Response Result |

_(Example: “Bearer yJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi...”)_

### Stop Data Model

**Data constraints**

| Type         | Params                  | Values              | Validation                 |
| ------------ | ----------------------- | ------------------- | -------------------------- |
| BasicStopDto | StopType                | Enum (0)            | **Required**               |
| BasicStopDto | InspectionTypes         | array []            | **Required**               |
| BasicStopDto | FileRefNo               | string [150]        | Optional                   |
| BasicStopDto | CaseNumber              | string [150]        | Optional                   |
| BasicStopDto | MasterAirWaybillNo      | string [150]        | Optional                   |
| BasicStopDto | HouseAirWaybillNo       | string [150]        | Optional                   |
| BasicStopDto | FlightDateTime          | DateTime            | Optional                   |
| BasicStopDto | Consignee               | string [150]        | Optional                   |
| BasicStopDto | Warehouse               | string [150]        | Optional                   |
| BasicStopDto | FlightNumber            | string [150]        | Optional                   |
| BasicStopDto | ReferenceNo             | string [150]        | Optional                   |
| BasicStopDto | Depot                   | string [150]        | Optional                   |
| BasicStopDto | MovementReferenceNumber | string [18]         | \*Conditional **Required** |
| BasicStopDto | BillOfEntryNo           | string [150]        | \*Conditional **Required** |
| BasicStopDto | BillOfEntryDate         | DateTime            | Optional                   |
| BasicStopDto | PortHealthRefNo         | string [150]        | Optional                   |
| BasicStopDto | ContainerNo             | string [11]         | Optional                   |
| BasicStopDto | FCLGRP                  | string [150]        | Optional                   |
| BasicStopDto | PCKT                    | string [150]        | Optional                   |
| BasicStopDto | Weight                  | number (double)     | Optional                   |
| BasicStopDto | BranchCode              | string [150]        | **Required**               |
| BasicStopDto | AgentCode               | string [150]        | **Required**               |
| BasicStopDto | StopFiles               | array [StopFileDto] | Optional                   |

_MovementReferenceNumber -> Conditional **Required** (When MovementReferenceNumber is NULL or Empty then BillOfEntryNo Becomes Required.) The MRN number is made up of Customs office code eg. JSA Customs Bill of Entry date and Assessment date eg 20190828 Lastly the bill of entry no eg 5075236 Full MRN number would be JSA201908285075236_

_BillOfEntryNo -> Conditional **Required** When BillOfEntryNo is NULL or Empty then MovementReferenceNumber Becomes Required._

_InspectionType -> **Required** InspectionType defines the type of inspection required for the agent eg. Port Health(Detain), State Vet(Detain). This will be match on the Name or Code or AltCode fields of the Inspection Types Lookup up table_

### Stop File Data model

| Type        | Params                  | Values       | Validation                 |
| ----------- | ----------------------- | ------------ | -------------------------- |
| StopFileDto | FileAsBase64String      | string [max] | **Required**               |
| StopFileDto | MimeType                | string [150] | **Required**               |
| StopFileDto | FileName                | string [150] | **Required**               |
| StopFileDto | MovementReferenceNumber | string [18]  | \*Conditional **Required** |
| StopFileDto | TransactionRefId        | number       | \*Conditional **Required** |

_MovementReferenceNumber -> Conditional **Required** (When MovementReferenceNumber is NULL or Empty then TransactionRefId Becomes Required.)_
_TransactionRefId -> Conditional **Required** When TransactionRefId is NULL or Empty then MovementReferenceNumber Becomes Required._

### InspectionTypes Data model

| Type            | Params  | Values       | Validation   |
| --------------- | ------- | ------------ | ------------ |
| InspectionTypes | Name    | string [150] | **Required** |
| InspectionTypes | AltCode | string [150] | **Required** |

_InspectionTypes -> **Required** (Stop (Booking) will be created for each Inspection Type Provided,If only one Inspection Type listed then only one Stop wil be created.)_

**Body Raw (application/json)**

**Content Example InspectionTypes Enum**

```json
{
     "inspectionTypes": [
          {
               "name": "Port Health(Detain)",
               "altCode": "Code 4:Port Health"
          },
          {
               "name": "Plant Inspection(Detain)",
               "altCode": "Code 4:Plant Inspection"
          },
          {
               "name": "SAPS",
               "altCode": "Code 4:SAPS"
          }
     ]
}
```

**Content Example StopType Enum**

```json
{"stopType": {
    "type": "number",
    "enum": [{"seaFreight": 0}, {"airFreight": 1}]
}
```

**Content Example Without Files**

```json
{
     "stopType": 1,
     "inspectionTypes": [
          {
               "name": "Port Health(Detain)",
               "altCode": "Code 4:Port Health"
          },
          {
               "name": "Plant Inspection(Detain)",
               "altCode": "Code 4:Plant Inspection"
          }
     ],
     "fileRefNo": "Test",
     "caseNumber": "123456",
     "masterAirWaybillNo": "083-1234567",
     "houseAirWaybillNo": "House1",
     "flightDateTime": "2019-08-26T23:05:09.9159514+02:00",
     "consignee": "",
     "warehouse": "",
     "flightNumber": "FL12345",
     "movementReferenceNumber": "JSA201908285075236",
     "depot": "",
     "referenceNo": "",
     "billOfEntryNo": "",
     "billOfEntryDate": "",
     "portHealthRefNo": "",
     "containerNo": "",
     "fclgrp": "",
     "pckt": "",
     "weight": 25,
     "branchCode": "PTA",
     "agentCode": "DFG00149AS2",
     "stopFiles": []
}
```

## Response _Success_

**Success** : `true`

**Content Example**

```json
{
     "result": [
          {
               "transactionRefId": 4526,
               "transactionNo": "SDFR19054526"
          },
          {
               "transactionRefId": 4527,
               "transactionNo": "SDFR19054526"
          }
     ],
     "targetUrl": null,
     "success": true,
     "error": null,
     "unAuthorizedRequest": false,
     "__abp": true
}
```

## Response _Failed_

**Result** : `false`

**Content Example**

```json
{
     "result": null,
     "targetUrl": null,
     "success": false,
     "error": {
          "code": 422,
          "message": "Your request is not valid!",
          "details": "The following errors were detected during validation. - The field Code must be a string with a maximum length of 50.",
          "validationErrors": [
               {
                    "message": "The field Code must be a string with a maximum length of 50.",
                    "members": ["code"]
               }
          ]
     }
}
```

**Content Example With Files**

```json
{
     "stopType": 1,
     "inspectionTypes": [
          {
               "name": "Port Health(Detain)",
               "altCode": "Code 4:Port Health"
          }
     ],
     "fileRefNo": "Test",
     "caseNumber": "123456",
     "masterAirWaybillNo": "083-1234567",
     "houseAirWaybillNo": "House1",
     "flightDateTime": "2019-08-26T23:05:09.9159514+02:00",
     "consignee": "",
     "warehouse": "",
     "flightNumber": "FL12345",
     "movementReferenceNumber": "JSA201908285075236",
     "depot": "",
     "referenceNo": "",
     "billOfEntryNo": "",
     "billOfEntryDate": "",
     "portHealthRefNo": "",
     "containerNo": "",
     "fclgrp": "",
     "pckt": "",
     "weight": 25,
     "branchCode": "PTA",
     "agentCode": "DFG00149AS2",
     "stopFiles": [
          {
               "fileAsBase64String": "JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdGFsb2cvUGL1ZpZXdlclByZW=...",
               "mimeType": "application/pdf",
               "fileName": "TT01.pdf",
               "movementReferenceNumber": "JSA201908285075236",
               "transactionRefId": ""
          },
          {
               "fileAsBase64String": "JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdGFsb2cvUGFnZXMgMiAwIFIvT=...",
               "mimeType": "application/pdf",
               "fileName": "TT02.pdf",
               "movementReferenceNumber": "",
               "transactionRefId": "4526"
          }
     ]
}
```

## Response _Success_

**Success** : `true`

**Content Example**

```json
{
     "result": [
          {
               "transactionRefId": 4526,
               "transactionNo": "SDFR19054526"
          }
     ],
     "targetUrl": null,
     "success": true,
     "error": null,
     "unAuthorizedRequest": false,
     "__abp": true
}
```

## Response _Failed_

**Result** : `false`

**Content Example**

```json
{
     "result": null,
     "targetUrl": null,
     "success": false,
     "error": {
          "code": 422,
          "message": "Your request is not valid!",
          "details": "The following errors were detected during validation. - The field Code must be a string with a maximum length of 50.",
          "validationErrors": [
               {
                    "message": "The field Code must be a string with a maximum length of 50.",
                    "members": ["code"]
               }
          ]
     }
}
```
