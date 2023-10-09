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

****

## Get Leaderboards
Request Uri: `/api/ranking/`

Request Type: GET

Paginated Response: True

Description: This will return a list of users [ Query Limited to 10 Users by default ] based on their referral count.

Auth Token Required: False

Response:
```json 
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
            "referrers_count": 1
        },
        {
            "username": "unravler",
            "referrers_count": 0
        }
    ]
}
```

provide the results size in url: `/api/ranking/?results=1`

Response:
```json
{
    "count": 2,
    "next": "http://127.0.0.1:8000/api/ranking/?page=2&results=1",
    "previous": null,
    "results": [
        {
            "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
            "referrers_count": 1
        }
    ]
}
```

****

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
    "ref_by": "1A113F",
    "code": "ZPE3BO"
}
```

****

## Increment Score
Request: <code>/api/users/score/</code>

Request Type: POST

Description: This will decode the blockchain address from the given signature, and if the user exists on the server increment the score as given in the score parameter.

Auth Token Required: True

Request Parameters:
```json
{
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "total_credits": 50,
    "discord_id": "unravler",
    "twitter_id": "unravler",
    "is_following_twitter": true,
    "has_broadcasted_twitter": true,
    "mapped_ip": "192.168.1.18",
    "score": 25,
    "signature": "0x8b43f5839effc245a041714b1af649a3908b572918e3b53e091365770c3c5b1c452e65437abd1c401b24b51a95067c01b30852093a91fb2f4c29193d1bd89d251c"
}
```

`Explaination:` I created the signature using above fields so I gave the data and signature in that format. You can pass your parameters with whom you created this signature from. the signature will be taken out from the request JSON and all the other parameteres will be used to process and decode the signature.

If the decoded username matches then we update the score.

Response:
```json
{
    "Status": "Score Updated!",
    "score": 75
}
```

****

## User Registration
Request Uri: <code>/api/auth/register/</code>

Request Type: POST

Description: Registration part, user will need a blockchain address, and a total credits amount will be given dynamically as of now, later it will be hard coded in backend for registration of users. There are two cases where users can either give a referral code provided to them via pre-existing users or can register without using any ref codes as well.

Auth Token Required: False

Request Parameters:

If user don't have a ref code:

```json
{
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "total_credits": 50,
    "discord_id": "unravler",
    "twitter_id": "unravler",
    "is_following_twitter": true,
    "has_broadcasted_twitter": true,
    "mapped_ip": "192.168.1.18",
    "signature": "0x902d68a8cdfd574e1f4bbe8cd5b0d00cee6389ef3dd4ce4f6d97065b43db095e27501f4c1cdcb5208537192c1e9561292e72b1f20c860bee9e30c99e4339a46b1c"
}
```

Response:

```json
{
    "success": {
        "id": "63f918a4-256b-46e9-9539-16e88dea0836",
        "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
        "total_credits": 50,
        "referred_by": "",
        "registered_at": "2023-10-09"
    },
    "status": 200
}
```

If user had a ref code while registration:

```json
{
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "total_credits": 50,
    "discord_id": "unravler",
    "twitter_id": "unravler",
    "is_following_twitter": true,
    "has_broadcasted_twitter": true,
    "mapped_ip": "192.168.1.18",
    "ref_by": "1A113F",
    "signature": "0x902d68a8cdfd574e1f4bbe8cd5b0d00cee6389ef3dd4ce4f6d97065b43db095e27501f4c1cdcb5208537192c1e9561292e72b1f20c860bee9e30c99e4339a46b1c"
}
```

Response:

```json
{
    "success": {
        "id": "63f918a4-256b-46e9-9539-16e88dea0836",
        "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
        "total_credits": 50,
        "referred_by": "1A113F",
        "registered_at": "2023-10-09"
    },
    "status": 200
}
```

****

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

****

## User Auth Tokens Get
Request Uri: <code>/api/auth/token/</code>

Request Type: POST

Description: To get the access tokens, u need to supply a Signature and a message and if both matched and if the decoded blockchain address is in the database, we give out tokens for that specific user.

Auth Token Required: False

Request Parameters:
```json
{
    "username": "0xBe540603F70191e3c984e88A7a8562A3084B1167",
    "total_credits": 50,
    "discord_id": "unravler",
    "twitter_id": "unravler",
    "is_following_twitter": true,
    "has_broadcasted_twitter": true,
    "mapped_ip": "192.168.1.18",
    "signature": "0x902d68a8cdfd574e1f4bbe8cd5b0d00cee6389ef3dd4ce4f6d97065b43db095e27501f4c1cdcb5208537192c1e9561292e72b1f20c860bee9e30c99e4339a46b1c"
}
```

`Note`: Am just using these parameters for the sake of signature verification because i initially used these parameters to encode and create a signature. You can any data and any signature and if the data matches you will be given access tokens.

Response:
```json
{
    "message": "Success",
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjk3MTY1MTQ2LCJpYXQiOjE2OTY1NjAzNDYsImp0aSI6IjVmYTI2Y2IwYWU0ODRmNTFiZTc3ZjU1YzhhMzkwZDg0IiwidXNlcl9pZCI6IjQ1MDUxZWU4LTA0MDMtNDc5Zi04Y2I3LTUwYWMxOGM3OTU2NSJ9.9tKjxKm-M5sj8ZNgMIaIDlaeF3CgwfENKXEhEfmEXiI",
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY5ODk3OTU0NiwiaWF0IjoxNjk2NTYwMzQ2LCJqdGkiOiIyZDcyYWI5MjIxYTA0NWQ0YWI3ZjA2MmYwOGNlNjE3MiIsInVzZXJfaWQiOiI0NTA1MWVlOC0wNDAzLTQ3OWYtOGNiNy01MGFjMThjNzk1NjUifQ.PYi3O4yUjXn0XHVNPqSwiXIB1a3-vvHlKtgFqqxP_XU"
}
```

****

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
