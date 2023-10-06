# dot-docs
Request Uri: <code>/api/users/</code>

Request Type: GET

Description: This will fetch all the users on the server with their total credits.

Auth Token Required: True

Response:
```json
[    
   {
        "id": "64a5219b-a208-471f-b989-2d4a1f0f4ba4",
        "username": "0xHe540603F70191e3c984e88A7a8562A3084B1167",
        "total_credits": 50
    },
    {
        "id": "835ae960-5fec-40a7-b39d-6abe3c592128",
        "username": "0xKe540603F70191e3c984e88A7a8562A3084B1167",
        "total_credits": 50
    },
    {
        "id": "74f7819f-ecb0-4e03-9dd0-5df3606b6bfe",
        "username": "0xMe540603F70191e3c984e88A7a8562A3084B1167",
        "total_credits": 50
    },
    {
        "id": "5a1182f1-8277-4a1a-97f6-df5d954ecaa4",
        "username": "0xAe540603F70191e3c984e88A7a8562A3084B1167",
        "total_credits": 50
    },
    {
        "id": "45051ee8-0403-479f-8cb7-50ac18c79565",
        "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
        "total_credits": 75
    }
]

```

Request Uri: <code>/api/ranking/</code>

Request Type: GET

Description: This will return a list of users [ Query Limited to 10 Users ] based on their referral count.

Auth Token Required: False

Response:
```json 
[
    {
        "username": "0xMe540603F70191e3c984e88A7a8562A3084B1167",
        "referrers_count": 3
    },
    {
        "username": "0xHe540603F70191e3c984e88A7a8562A3084B1167",
        "referrers_count": 0
    },
    {
        "username": "0xAe540603F70191e3c984e88A7a8562A3084B1167",
        "referrers_count": 0
    },
    {
        "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
        "referrers_count": 0
    },
    {
        "username": "0xKe540603F70191e3c984e88A7a8562A3084B1167",
        "referrers_count": 0
    }
]
```
