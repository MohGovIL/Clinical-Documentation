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


##load forms

**Request:**
> GET  /apis/api/load-forms?service_type=3&reason_code=7

**querystring parametrs **

    service-type : integer / null 
    
    reason-code  : integer / null

**Response (example):**
```
[
{component: <REACT_COMPONENT_NAME>, //directory column in registry table.
 form_name:<NAME>, // name column
 order: <ORDER_NUMBER> // priority column
 },
{component: <REACT_COMPONENT_NAME>, //directory column in registry table.
 form_name:<NAME>, // name column
 order: <ORDER_NUMBER> // priority column
 }
]
```



##Templates for the forms

**Request:**
> GET  api/templates/search?service-type=5&reason-code=2&form=7&form-field=recomended_medicine

**querystring parametrs **

    service-type : integer not null - the type of the service needed
    reason-code  : integer not null - the reason code
    form-field : string not null - the field of the form like recomended_medicine
    form : string not null - the id of the form

**Response (example):**
```
[
'template  1',
'template 2',
'this is template 3'
]
```
