# Clinikal - REST API

For non-medical calls (like settings, forms structures etc.) that the application needs we have developed different API modules.  

##Authorization 
We are using the [OpenEMR Authorization interface](https://github.com/openemr/openemr/blob/master/API_README.md#authorization)



##load forms

The encounter sheets can shows a various of forms (from `Components/forms` in the react repository).  
The setting what form will shown for every service type or reason code is fetched from the API.  
**Request:**
> GET  /apis/api/load-forms?service_type=3&reason_code=7

**Querystring parameters**

| **parameter**      | **type**      |
| -------------------------- | -------------- |
|  service-type                       |   integer / null              |                                                                                       
| reason-code          | integer / null           |

    
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



##Templates for the form fields
The templates API provides common sentences for fast form filling.  

**Request:**
> GET  api/templates/search?service-type=5&reason-code=2&form=7&form-field=recomended_medicine

**Querystring parameters**

| **parameter**      | **description**      |
| -------------------------- | -------------- |
|  service-type                       |   integer not null - the type of the service needed             |                                                                                       
| reason-code          | integer not null - the reason code           |
| form-field          | string not null - the field of the form like recomended_medicine           |
| form          | string not null - the id of the form           |

**Response (example):**
```
[
'template  1',
'template 2',
'this is template 3'
]
```


##Letters

###List of all the available letters

**Request:**
> GET  api/letters/list

The response contains all the parameters are required for the letter.

**Response (example):**
```
{
    "xray": {
        "letter_post_json": {
            "facility": "required",
            "encounter": "required",
            "owner": "optional",
            "patient": "optional"
        }
    }
}
```


###Create letter

**Request:**
> POST  api/letters/<letter_name>


**Body params: (according the requirement)**
example - 
```
{
        "facility": "13",
        "encounter": "1",
 }
```

**Response (example):**
```
{
    "id": 1,
    "base64_data": "JVBERi0xLjQKJ....................VBERi0"
}
```