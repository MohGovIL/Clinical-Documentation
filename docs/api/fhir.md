# FHIR API

<https://www.hl7.org/fhir/http.html>

<br><br><br>

##[Patient](https://www.hl7.org/fhir/patient.html)

### Supported Requests
- [x] read
- [ ] search
- [x] create
- [x] update
- [ ] delete
- [x] patch (only replace)

<br>

### Supported Resource Properties
```

  {
    "id": 1,
    "resourceType": "Patient",
    "identifier": [
      {
        "value": "3432432"
      }
    ],
    "name": [
      {
        "family": "ראשון",
        "given": [
          "בדיקה"
        ]
      }
    ],
    "telecom": [
      {
        "system": "email",
        "value": "amiel@gmail.com"
      },
      {
        "system": "phone",
        "value": "064525252",
        "use": "home"
      },
      {
        "system": "phone",
        "value": "0525112396",
        "use": "mobile"
      }
    ],
    "gender": "male",
    "birthDate": "2015-05-04",
    "deceasedBoolean": false,
    "address": [
      {
        "type": "both",
        "line": [
          "3",
          "34"
        ],
        "city": "city_3000",
        "postalCode": "4517200",
        "country": "country_254"
      }
    ],
    "managingOrganization": {
        "reference": "Organization/6"
    }
  }
```
<br>

### Supported Operators

None

<br>

### Supported General Search Parameters

Parameter|Valid Values
--|--

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id||exact, contains|
identifier||exact, contains|
mobile||exact, contains|
organization|||
name||exact, contains|

<br>

### Examples
Read request:  
`GET /apis/v4/Patient/:pid`

Search requests:  
`GET /apis/fhir/v4/Patient`  
`GET /apis/fhir/v4/Patient?_id=1`  
`GET /apis/fhir/v4/Patient?identifier=308826367`  
`GET /apis/fhir/v4/Patient?name=yosi&name=banana`  

Create request:  
`POST /apis/v4/Patient`  

Update request:  
`PUT /apis/v4/Patient/:pid`  

Patch request:  
`PATCH /apis/fhir/v4/Patient/:pid`  
```
[
    {op:"replace", path:"/id", value:"1"},
    {op:"replace", path:"/identifier/0/value", value:"3432432"},
    {op:"replace", path:"/name/0/family", value:"family"},
    {op:"replace", path:"/name/0/given", value:["lname","mname"]},
    {op:"replace", path:"/telecom/0", value:{system: "phone",value: "064525252",use: "home" } } ,
    {op:"replace", path:"/telecom/1", value:{system: "email",value: "amiel@gmail.com" } } ,
    {op:"replace", path:"/telecom/2", value:{system: "phone",value: "0525112396",use: "mobile" } } ,
    {op:"replace", path:"/gender", value:"male"},
    {op:"replace", path:"/birthDate", value:"1993-05-04" },
    {op:"replace", path:"/deceasedBoolean", value:"true" },
    {op:"replace", path:"/deceasedDateTime", value: "2020-01-04" },
    {op:"replace", path:"/address/0", value:{type:"both",city:"city_3000",postalCode:"4517200",country:"country_254"} },
    {op:"replace", path:"/address/0/line", value:["street_200","3","34"] }
]
```

<br><br> 

---

<br><br>

## [Appointment](https://www.hl7.org/fhir/appointment.html)

### Supported Requests
- [x] read  
- [ ] search  
- [ ] create  
- [x] update  
- [ ] delete

<br>

### Supported Resource Properties
````
{
  "id": 4,
  "resourceType": "Appointment",
  "status": "noshow",
  "serviceType": [
    {
      "coding": [
        {
          "code": "3"
        }
      ],
      "text": "X-ray"
    }
  ],
  "reasonCode": [
    {
      "coding": [
        {
          "code": "1"
        }
      ],
      "text": "shoulder"
    },
    {
      "coding": [
        {
          "code": "2"
        }
      ],
      "text": "ankle"
    }
  ],
  "priority": "1",
  "description": "זה תיאור מגניב",
  "start": "2020-01-28T09:15:00.000Z",
  "end": "2020-01-28T09:30:00.000Z",
  "minutesDuration": "15",
  "comment": "66666666666",
  "participant": [
    {
      "actor": {
        "reference": "Patient/1"
      }
    },
    {
      "actor": {
        "reference": "HealthcareService/2"
      }
    }
  ]
}
````

<br>

### Supported Operators

None

<br>
### Supported General Search Parameters

Parameter|Valid Values
--|--
_include|Appointment:patient
_sort|date, priority, service-type **
_summary|count

** Can be used separately or combined together using commas

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id||||
date|eq, ge, le||
status||not|
actor:HealthcareService.organization|||
service-type|||

<br>

### Examples
Search request:  
`GET /apis/fhir/v4/Appointment?date=ge2019-01-16&date=le2020-01-30&_include=Appointment:patient`


<br><br> 

---

<br><br>  

## [Encounter](https://www.hl7.org/fhir/encounter.html)

### Supported Requests
- [x] read
- [x] search
- [x] create
- [x] update
- [ ] delete
- [x] patch
<br>

### Supported Resource Properties
````
{
    "id": "7",
    "resourceType": "Encounter",
    "status": "planned",
    "serviceType": {
        "coding": [
            {
                "code": "1"
            }
        ],
        "text": "Ultrasound"
    },
    "priority": {
        "coding": [
            {
                "code": "0"
            }
        ]
    },
    "subject": {
        "reference": "Patient/1"
    },
    "participant": [
        {
            "individual": {
                "reference": "Practitioner/1"
            }
        },
        {
            "individual": {
                "reference": "RelatedPerson/4"
            }
        }
    ],
    "appointment": [
        {
            "reference": "Appointment/1"
        }
    ],
    "period": {
        "start": "2020-03-08T00:00:00.000Z"
    },
    "reasonCode": [
        {
            "coding": [
                {
                    "code": "5"
                }
            ],
            "text": "Upper Abdomen"
        }
    ],
    "serviceProvider": {
        "reference": "Organization/2"
    }
}
````

<br>

### Supported Operators

None

<br>

### Supported General Search Parameters

Parameter|Valid Values
--|--
_include|Encounter:patient
_sort|date, priority, service-type **
_summary|count

** Can be used separately or combined together using commas

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id||||
date|eq, ge, le||
status|||V
appointment|||
patient|||
service-provider|||
service-type|||
<br>

### Examples

Search request:  
`GET /apis/v4/Encounter/1`  
`GET /apis/v4/Encounter (all)`  
`GET /apis/v4/Encounter?_id=8`  
`GET /apis/v4/Encounter?_id=8&status=planned&status=in progress (or operator)`  
`GET /apis/v4/HealthcareService?appointment=5&patient=78`  
`GET /apis/fhir/v4/Encounter?date=gt2020-02-09`  

<br><br>  

---

<br><br>  

## [Practitioner](https://www.hl7.org/fhir/practitioner.html)

### Supported Requests

- [x] read
- [x] search
- [ ] create
- [ ] update
- [ ] delete

<br>

### Supported Resource Properties
````
{
   "id":4,
   "resourceType":"Practitioner",
   "identifier":[ 
      { 
         "value":"039664776"
      }
   ],
   "active":1,
   "name":[ 
      { 
         "family":"yosi",
         "given":[ 
            "cohen",
            "motek"
         ]
      }
   ]
}
````

<br>

### Supported Operators

None

<br>

### Supported General Search Parameters

Parameter|Valid Values
--|--

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id|||
name**|||
active|||

** Value comes from "family" or "given"

<br>

### Examples
Read request:  
`GET /apis/fhir/v4/Practitioner/:id`  

Search requests:  
`GET /apis/fhir/v4/Practitioner?name=yosi&active=1`  

<br><br> 

---

<br><br>  

## [Organization](https://www.hl7.org/fhir/organization.html) 

### Supported Requests
- [X] read
- [X] search
- [ ] create
- [ ] update
- [ ] delete

<br>

### Supported Resource Properties
````
{
   "resourceType":"Organization",
   "id":4,
   "name":"מחוז אשקלון",
   "alias":[
      null
   ],
   "telecom":[
      {
         "system":"fax",
         "value":"+972-546-837-767"
      },
      {
         "system":"phone",
         "value":"+972-546-837-766",
         "use":"work"
      }
   ],
   "address":[
      {
         "line":[
            "שד הפלי\"ם 15א"
         ],
         "city":"חיפה",
         "state":"32"
      }
   ]
}
````

<br>

### Supported Operators

None

<br>

### Supported General Search Parameters

Parameter|Valid Values
--|--

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id|||
name|||
active|||

<br>

### Examples
Read request:  
`GET /apis/fhir/v4/Organization/:id`  

Search requests:  
`GET /apis/v4/Organization (all)`  
`GET /apis/v4/Organization?_id=8`  
`GET /apis/v4/Organization?_id=8&active=1`  
`GET /apis/v4/Organization?name=לשכת בריאות חיפה`  
`GET /apis/v4/Organization?name=חיפה&active=1`  

<br><br> 

---

<br><br> 

## [HealthcareService](https://www.hl7.org/fhir/healthcareservice.html)

### Supported Requests
- [x] read
- [x] search
- [ ] create
- [ ] update
- [ ] delete

<br>

### Supported Resource Properties:

````
{
  "id": 2,
  "resourceType": "HealthcareService",
  "active": 1,
  "providedBy": {
    "reference": "Organization/3",
    "display": "Your Clinic Name Here"
  },
  "category": [
    {
      "coding": [
        {
          "code": "30"
        }
      ],
      "text": "Specialist Radiology/Imaging"
    }
  ],
  "type": [
    {
      "coding": [
        {
          "code": "1"
        }
      ],
      "text": "Ultrasound"
    }
  ],
  "name": "The Ultrasounders Inc.",
  "comment": "only ultrasounds",
  "extraDetails": "this can be in markdown",
  "availableTime": [
    {
      "daysOfWeek": [
        "mon",
        "tue"
      ],
      "allDay": 1
    },
    {
      "daysOfWeek": [
        "thu",
        "fri"
      ],
      "availableStartTime": "08:30:00",
      "availableEndTime": "05:30:00"
    }
  ],
  "notAvailable": [
    {
      "during": {
        "start": "2015-12-25T12:03:31.000Z",
        "end": "2015-12-26T12:03:31.000Z"
      }
    },
    {
      "during": {
        "start": "2016-01-01T12:03:31.000Z",
        "end": "2016-01-01T12:03:31.000Z"
      }
    }
  ],
  "availabilityExceptions": "Reduced capacity is available during the Christmas period"
}
````

<br>

### Supported Operators

None

<br>

### Supported General Search Parameters

Parameter|Valid Values
--|--

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id|||
active|||
name|||
organization|||
service-type|||

<br>

### Examples
Read request:  
`GET /apis/fhir/v4/HealthcareService/:id`

<br><br> 

---

<br><br> 

## [ValueSet](https://www.hl7.org/fhir/valueset.html)

### Supported Requests
- [x] read
- [ ] search

<br>

### Supported Resource Properties:

````
{
  "id": "reason_codes_5",
  "resourceType": "ValueSet",
  "title": "MRI Reason Codes",
  "status": "active",
  "expansion": {
      "timestamp": "2020-02-19 06:07:24T18:07:24.000Z",
      "contains": [
          {
              "system": "clinikal_reason_codes",
              "code": "18",
              "display": "Backbone"
          },
          {
              "system": "clinikal_reason_codes",
              "code": "19",
              "display": "Brain"
          }
      ]
  }
}
````

<br>

### Supported Operators

* $expand

<br>

### Supported General Search Parameters

Parameter|Valid Values
--|--

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--

<br>

### Examples
Read request:  
`GET /apis/fhir/v4/ValueSet/:id/$expand`  

<br><br>






## [RelatedPerson](https://www.hl7.org/fhir/relatedperson.html)

### Supported Requests
- [x] read
- [x] search
- [x] create
- [x] update
- [ ] delete
- [x] patch

<br>

### Supported Resource Properties:

````
{
    "id": "1",
    "resourceType": "RelatedPerson",
    "identifier": [
        {
            "type": {
                "coding": [
                    {
                        "code": "bobo"
                    }
                ]
            },
            "value": "1235698"
        }
    ],
    "active": true,
    "patient": {
        "reference": "Patient/1"
    },
    "relationship": [
        {
            "coding": [
                {
                    "code": "OCVJO"
                }
            ]
        }
    ],
    "telecom": [
        {
            "system": "phone",
            "value": "036495774",
            "use": "home"
        },
        {
            "system": "email",
            "value": "bobo@gmail.com"
        },
        {
            "system": "phone",
            "value": "054480880",
            "use": "mobile"
        }
    ],
    "gender": "male"
}
````

<br>

### Supported Operators

None

<br>

### Supported General Search Parameters

Parameter|Valid Values
--|--

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id|||
identifier|||
active|||
patient|||
relationship|||
gender|||
email|||
<br>

### Examples
Read request:  
`GET /apis/fhir/v4/RelatedPerson/:id`

<br><br> 

---

<br><br> 



## [DocumentReference](https://www.hl7.org/fhir/DocumentReference.html)

### Supported Requests
- [x] read
- [x] search
- [x] create
- [ ] update
- [ ] delete
- [ ] patch

<br>

### Supported Resource Properties:

````
{
    "id": "5",
    "resourceType": "DocumentReference",
    "category": [
        {
            "coding": [
                {
                    "code": "2",
                    "display": "EMedical Record"
                }
            ]
        }
    ],
    "author": [
        {
            "reference": "Practitioner/1"
        }
    ],
    "content": [
        {
            "attachment": {
                "contentType": "application/pdf",
                "data": "fgsdFGSDER4543524ASDFSADFSDFSDAFSDF$@#FV$%TtvserTDFZSD", **
                "url": "name_bla_bla"
            }
        }
    ],
    "context": {
        "encounter": [
            {
                "reference": "Encounter/1"
            }
        ],
        "sourcePatientInfo": {
            "reference": "Patient/1"
        }
    }
}
````
** In base64 format

<br>

### Supported Operators

None

<br>

### Supported General Search Parameters

Parameter|Valid Values
--|--
_summary|true

<br>

### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id|||
encounter|||
patient|||

<br>

### Examples
Read request:  
`GET /apis/fhir/v4/DocumentReference/:id`

<br><br> 

---

<br><br> 
