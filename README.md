## Get Users
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

## Get Leaderboards
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
## Get Single User
Request Uri: <code>/api/user/</code>

Request Type: POST

Description: This will fetch data regarding any one user in question via their username [ blockchain address ].

Auth Token Required: True

Request Parameters:
```json
{ 
   "block": "0xBe540603F70191e3c984e88A7a8562A3084B1167"
}
```
Response:
```json
{
    "id": "45051ee8-0403-479f-8cb7-50ac18c79565",
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "total_credits": 75,
    "ref_by": "1A113F"
}
```

## Increment Score
Request: <code>/api/users/score/</code>

Request Type: POST

Description: This will decode the blockchain address from the given signature, and if the user exists on the server increment the score as given in the score parameter.

Auth Token Required: True

Request Parameters:
```json
{
    "signature": "0x31f8b104895822caf944627aa4b42771c9cc438f3752d246d6f984071292d7ff0d1fbee722ab3012d0750fe178aa02301d5b770665c971d873c95a5632d6b3f21c",
    "message": "1234567890",
    "score": 25
}
```
Response:
```json
{
    "Status": "Score Updated!",
    "score": 100
}
```
## User Registration
Request Uri: <code>/api/auth/register/</code>

Request Type: POST

Description: Registration part, user will need a blockchain address, and a total credits amount will be given dynamically as of now, later it will be hard coded in backend for registration of users. There are two cases where users can either give a referral code provided to them via pre-existing users or can register without using any ref codes as well.

Auth Token Required: True

Request Parameters:

If user don't have a ref code:
```json
{
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "total_credits": 50
}
```
Response:
```json
{
    "id": "45051ee8-0403-479f-8cb7-50ac18c79565",
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "total_credits": 50,
    "ref_by": ""
}
```

If user had a ref code while registration:
```json
{
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "ref_by": "1A113F",
    "total_credits": 50
}
```
Response:
```json
{
    "id": "45051ee8-0403-479f-8cb7-50ac18c79565",
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "total_credits": 50,
    "ref_by": "1A113F"
}
```
