## Get Users
Request Uri: `/api/users/`

Request Type: GET

Paginated Response: True

Description: This will fetch all the users on the server with their total credits.

Auth Token Required: True

There are two ways to handle pagination:
  1. provide the results size in url: `/api/users/?results=1`
     
Response:
   ```json
   {
       "count": 2,
       "next": "http://127.0.0.1:8000/api/users/?page=2&results=1",
       "previous": null,
       "results": [
           {
               "id": "c2686f63-c83b-4e7a-83cf-1c9723f2575c",
               "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
               "total_credits": 50
           }
       ]
   }
   ```
   2. or by not providing the results parameter | by giving anything other then results: `/api/users/`

Response:
```json
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": "c2686f63-c83b-4e7a-83cf-1c9723f2575c",
            "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
            "total_credits": 50
        },
        {
            "id": "143776d9-7fde-4b91-acb1-bef3f054a590",
            "username": "unravler",
            "total_credits": 0
        }
    ]
}
```

## Get Leaderboards
Request Uri: <code>/api/ranking/</code>

Request Type: GET

Paginated Response: True

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
## Delete User
Request Uri: <code>/api/user/delete/</code>

Request Type: DELETE

Description: Just to delete a user from the platform.

Auth token Required: True

Request Parameters:
```json
{
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167"
}
```
Response:
```json
{
    "Status": "Deleted user!"
}
```
## User Auth Tokens Get
Request Uri: <code>/api/auth/token/</code>

Request Type: POST

Description: To get the access tokens, u need to supply a Signature and a message and if both matched and if the decoded blockchain address is in the database, we give out tokens for that specific user.

Auth Token Required: False

Request Parameters:
```json
{
    "signature": "0x31f8b104895822caf944627aa4b42771c9cc438f3752d246d6f984071292d7ff0d1fbee722ab3012d0750fe178aa02301d5b770665c971d873c95a5632d6b3f21c",
    "message": "1234567890"
}
```
Response:
```json
{
    "message": "Success",
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjk3MTY1MTQ2LCJpYXQiOjE2OTY1NjAzNDYsImp0aSI6IjVmYTI2Y2IwYWU0ODRmNTFiZTc3ZjU1YzhhMzkwZDg0IiwidXNlcl9pZCI6IjQ1MDUxZWU4LTA0MDMtNDc5Zi04Y2I3LTUwYWMxOGM3OTU2NSJ9.9tKjxKm-M5sj8ZNgMIaIDlaeF3CgwfENKXEhEfmEXiI",
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY5ODk3OTU0NiwiaWF0IjoxNjk2NTYwMzQ2LCJqdGkiOiIyZDcyYWI5MjIxYTA0NWQ0YWI3ZjA2MmYwOGNlNjE3MiIsInVzZXJfaWQiOiI0NTA1MWVlOC0wNDAzLTQ3OWYtOGNiNy01MGFjMThjNzk1NjUifQ.PYi3O4yUjXn0XHVNPqSwiXIB1a3-vvHlKtgFqqxP_XU"
}
```
## Refresh Auth Tokens
Request Uri: <code>/api/auth/token/refresh/</code>

Request Type: POST

Description: To Refresh an access token after it has expired.

Auth Token Required: False

Request Parameters:
```json
{
    "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY5ODYyNDg3MSwiaWF0IjoxNjk2MjA1NjcxLCJqdGkiOiI1ZGMyOWEzZTE3ZjU0YmU2YjhiZDFlNmE2M2MxMzRiNCIsInVzZXJfaWQiOiI4NWQ2OWViZS00NzkyLTRjZDktYmY3OC01YmU5YWMwMWM5YjIifQ.3bxqm1LzNAgeQnvUxzQah0wCtkS-VpeJbl5T-kJLIhQ"
}
```
Response:
```json
{
    "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjk2ODEwNjU1LCJpYXQiOjE2OTYyMDU2NzEsImp0aSI6IjYwYWUxMDdjODgyZjQwYTE5NTUxZDNhMzQ2OGRmM2E4IiwidXNlcl9pZCI6Ijg1ZDY5ZWJlLTQ3OTItNGNkOS1iZjc4LTViZTlhYzAxYzliMiJ9.qUMXvqWrRq--com8jJ07y1GuneXprB3Z1O6t2jS1hzA"
}
```
