
# Get Status Events

Retrieves a list of status events for a stop inspection request. 


**URL** : `/api/OutboundStop/GetStatusUpdates`

**Method** : `POST`

**Auth **Required**** : YES

**Headers**

| Key | Value |
|--------------|--------------|
| Content-Type | application/json  |
| Accept | application/json |
| Authorization | Bearer + AccessToken received from Authenticate Response Result |

*(Example: “Bearer yJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJodHRwOi...”)*


### Status Event Filter Parameters Body Data model \*(array)
| Type| Params| Values| Validation |
|--------------|---------- |-------------- |------------ |
|StatusEventFilterDto|TransactionRefId|number|**Required**|
|StatusEventFilterDto|LastKnowStatusId|number(nullable)| \* **Optional**|

_When LastKnowStatusId property is left null/empty you will get the full list of status events for the given inspection stop request transaction reference Id provided._


**Available Status Events**

| Order Of Events | Status Id | Status Display Name |Description|
|--------------|--------------|--------------|--------------|
| 1 | 0 | Inspection Open |Inspection Stop Request was received and booked in the application manually or via API call.|
| 2 | 3 | Inspection Pending Confirmation |Booked Inspection Stop Request needs approval before the inspection can take place. |
| 3 | 6 | Inspection Allocated | Booked Inspection Stop Request as been allocated an Inspecting officer & inspection date-time has been assigned. |
| 4 | 1 | Inspection In Progress | Physical Inspection has started and is currently being officiated by a Global DFS inspector. |
| 5 | 5 | Inspection Paused | Booked Inspection Stop Request has been paused due to external factors and can not continue at this time. |
| 6 | 4 | Inspection Complete | Physical inspection has been completed by official Global DFS inspector and preliminary results have been uploaded & updated. |
| 7 | 2 | Inspection Finalized | Booked Inspection Stop Request has been Finalized and survey report is available. |
| 8 | 7 | Inspection Cancelled | Booked Inspection Stop Request has been Cancelled internally or by the requested party. |


**Body Raw (application/json)**

**Content Example**

```json
[
	{
		"TransactionRefId":3002,
		"LastKnowStatusId":1
	},
	{
		"TransactionRefId":3000
	},
]
```

## Response *Success* 
**Success** : `true`

**Content Example**

```json
{
    "result": [
        {
            "movementReferenceNumber": null,
            "transactionRefId": 3000,
            "inspectionOfficer": null,
            "inspectionDateTime": null,	    
            "statusEvents": [
                {
                    "statusId": 0,
                    "statusDisplayName": "Inspection Open",
                    "transactionRefId": "3000",
                    "creationTime": "2019-05-02T15:15:12.0522219+02:00"		
                },
                {
                    "statusId": 4,
                    "statusDisplayName": "Inspection Complete",
                    "transactionRefId": "3000",
                    "creationTime": "2019-05-03T09:12:32.3792393+02:00"
                },
                {
                    "statusId": 2,
                    "statusDisplayName": "Inspection Finalized",
                    "transactionRefId": "3000",
                    "creationTime": "2019-05-03T09:12:41.3148374+02:00"		
                }
            ]
        },
        {
            "movementReferenceNumber": null,
            "transactionRefId": 3002,
            "inspectionOfficer": "Lufuno Randela",
            "inspectionDateTime": "2019-05-03T09:00:00+02:00",
            "statusEvents": [
                {
                    "statusId": 4,
                    "statusDisplayName": "Inspection Complete",
                    "transactionRefId": "3002",
                    "creationTime": "2019-05-03T11:10:34.4741131+02:00"	
                },
                {
                    "statusId": 2,
                    "statusDisplayName": "Inspection Finalized",
                    "transactionRefId": "3002",
                    "creationTime": "2019-05-03T11:25:28.6966016+02:00"	
                }
            ]
        }
    ],
    "targetUrl": null,
    "success": true,
    "error": null,
    "unAuthorizedRequest": false,
    "__abp": true
}

```


## Response *Failed*
**Result** : `false`

**Content Example**

```json
{
    "result": null,
    "targetUrl": null,
    "success": false,
    "error": {
        "code": 422,
        "message": "Unprocessable Entity",
        "details": "",
        "validationErrors": [
            {
                "message": "Input parameters is invalid!,Atleast one TransactionRefId is required.",
                "members": null
            }
        ]
    },
    "unAuthorizedRequest": false,
    "__abp": true
}
```
