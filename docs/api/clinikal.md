# Clinikal - REST API


##Fhir authorization 
Get Bearer token

**Request:**
> POST /apis/fhir/auth

**Body params:**
```
{
    "grant_type":"password",
    "username": "<USER_NAME>",
    "password": "<PASSWORD>",
    "scope":"default"
}
```

**Response (example):**
```
{
"token_type":"Bearer",
"access_token":"d2870cb522230dbb8946b2f47d2c7e6664656661756c74",
"expires_in":"3600"
}
```