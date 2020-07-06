# FHIR API

<https://www.hl7.org/fhir/http.html>

<br><br><br>

##[Patient](https://www.hl7.org/fhir/patient.html)

### Supported Requests
- [x] read
- [x] search
- [x] create
- [x] update
- [ ] delete
- [x] patch (only replace)

<br>

### Supported Resource Properties
```
  {
   "id":1,
   "resourceType":"Patient",
    "identifier": [
        {
            "type": {
                "coding": [
                    {
                        "code": "idtype_3"
                    }
                ],
                "text": "idtype_3"
            },
            "value": "43534535345"
        }
    ],
   "name":[
      {
         "family":"ראשון",
         "given":[
            "בדיקה"
         ]
      }
   ],
   "telecom":[
      {
         "system":"email",
         "value":"amiel@gmail.com"
      },
      {
         "system":"phone",
         "value":"064525252",
         "use":"home"
      },
      {
         "system":"phone",
         "value":"0525112396",
         "use":"mobile"
      }
   ],
   "gender":"male",
   "birthDate":"2015-05-04",
   "deceasedBoolean":false,
   "address":[
      {
         "type":"both",
         "line":[
            "3",
            "34"
         ],
         "city":"city_3000",
         "postalCode":"4517200",
         "country":"country_254"
      }
   ],
   "managingOrganization":{
      "reference":"Organization/6"
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
identifier||exact, contains,of-type| "system\|code\|identifier" *
mobile||exact, contains|
organization|||
name||exact, contains|

<br>
* example :identifier:of-type=|idtype_3|1111111
---

<br><br>

## [Appointment](https://www.hl7.org/fhir/appointment.html)

### Supported Requests
- [x] read  
- [x] search  
- [x] create  
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
- [x] delete
- [x] patch
<br>

### Supported Resource Properties
````
{
    "id": "7",
    "resourceType": "Encounter",
    "extension": [
        {
            "valueString": "Life is peaceful there",
            "url": "http://clinikal/extensions/encounter/reasonCodesDetail"
        },
        {
            "valueString": "Go West ",
            "url": "http://clinikal/extensions/encounter/arrivalWay"
        },
        {
            "valueString": "waiting_for_nurse",
            "url": "http://clinikal/extensions/encounter/secondaryStatus"
        },
        {
            "valueDateTime": "2019-06-21T13:15:20.000Z",
            "url": "http://clinikal/extensions/encounter/statusUpdateDate"
        }
    ],
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
arrival_way|||*1
reason_codes_details|||*1
all-statuses|||*2

<br>

*1 search is by part of string (does not support exact)
*2 search in :
        Encounter.status 
        OR 
        Encounter.extension.valueString (WHERE url "http://clinikal/extensions/encounter/secondaryStatus")

### Examples

Search request:  
`GET /apis/fhir/v4/Encounter/1`  
`GET /apis/fhir/v4/Encounter (all)`  
`GET /apis/fhir/v4/Encounter?_id=8`  
`GET /apis/fhir/v4/Encounter?_id=8&status=planned&status=in progress (or operator)`  
`GET /apis/fhir/v4/HealthcareService?appointment=5&patient=78`  
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
given|||
family|||

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
`GET /apis/fhir/v4/Organization (all)`  
`GET /apis/fhir/v4/Organization?_id=8`  
`GET /apis/fhir/v4/Organization?_id=8&active=1`  
`GET /apis/fhir/v4/Organization?name=לשכת בריאות חיפה`  
`GET /apis/fhir/v4/Organization?name=חיפה&active=1`  

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
    "name": [
        {
            "text": "idan the man"
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
name|||

*name search by name (full name) is exact search unless a parameter is being used. 
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

## [Questionnaire](https://www.hl7.org/fhir/questionnaire.html)

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
    "id": "38",
    "resourceType": "Questionnaire",
    "name": "commitment_questionnaire",
    "title": "Commitment questionnaire",
    "status": "active",
    "item": [
        {
            "linkId": "1",
            "text": "Commitment number",
            "type": "integer"
        },
        {
            "linkId": "2",
            "text": "Commitment date",
            "type": "date"
        }

    ]
}
````

<br>

### Supported Operators

None


### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
title||exact|
status||exact| active|retired
name||exact|


<br><br> 

<br><br> 
 
---


<br><br>

## [QuestionnaireResponse](https://www.hl7.org/fhir/questionnaireresponse.html)

### Supported Requests
- [x] read  
- [x] search  
- [x] create  
- [x] update  
- [ ] delete

<br>

### Supported Resource Properties
````
{
    "id": "61",
    "resourceType": "QuestionnaireResponse",
    "questionnaire": "Questionnaire/38",
    "status": "in-progress",
    "subject": {
        "reference": "Patient/4"
    },
    "encounter": {
        "reference": "Encounter/1"
    },
    "authored": "2020-03-24T12:21:21.000Z",
    "author": {
        "reference": "Practitioner/1"
    },
    "source": {
        "reference": "Patient/4"
    },
    "item": [
        {
            "linkId": "1",
            "text": "Commitment number",
            "answer": [
                {
                    "valueInteger": "11111111"
                }
            ]
        },
        {
            "linkId": "2",
            "text": "Commitment date",
            "answer": [
                {
                    "valueDate": "03/01/1984"
                }
            ]
        }

    ]
}
````

<br>

### Supported Operators

None


### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id||exact|
status||exact|
encounter||exact|
questionnaire|||
subject||exact|
author||exact|
patient||exact|

<br><br> 
 
---

---


<br><br>

## [condition](https://www.hl7.org/fhir/condition.html)

### Supported Requests
- [x] read  
- [x] search  
- [x] create  
- [x] update  
- [ ] delete

<br>

### Supported Resource Properties
````
{
    "id": "1",
    "resourceType": "Condition",
    "clinicalStatus": {
        "coding": [
            {
                "system": "http://clinikal/valueset/reaction/outcome",
                "code": "0"
            }
        ],
        "text": "Unassigned"
    },
    "category": [
        {
            "coding": [
                {
                    "system": "http://clinikal/condition/category/medical_problem",
                    "code": "asthma"
                }
            ]
        }
    ],
    "code": {
        "coding": [
            {
                "system": "http://clinikal/diagnosis/type/MOH_ICD10",
                "code": "A159"
            }
        ]
    },
    "subject": {
        "reference": "Patient/1"
    },
    "onsetDateTime": "2020-05-01T11:12:15.000Z",
    "abatementDateTime": "2020-05-25T11:12:15.000Z",
    "recordedDate": "2020-05-25T15:35:27.000Z",
    "recorder": {
        "reference": "Practitioner/1"
    },
    "stage": [
        {
            "summary": {
                "text": "bad asthma"
            },
            "type": {
                "coding": [
                    {
                        "system": "http://clinikal/valueset/reaction/occurrence",
                        "code": "2"
                    }
                ],
                "text": "frequency_1"
            }
        }
    ],
    "evidence": [
        {
            "code": [
                {
                    "coding": [
                        {
                            "system": "http://clinikal/valueset/reaction",
                            "code": "shortness_of_breath"
                        }
                    ]
                }
            ]
        }
    ],
    "note": [
        {
            "text": "bla bla"
        }
    ]
}
````

<br>

### Supported Operators

None


### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id||exact|
clinical-status||exact|
code||of-type| "system\|code\|identifier" *
category||| "URL\|code" **
subject||exact|

<br><br> 
 
*example  Condition?code:of-type=|MOH_ICD10|A159
**example  category?category=http://clinikal/condition/category/medical_problem|asthma (code is optional)

 
---


## [MedicationStatement](https://www.hl7.org/fhir/medicationstatement.html)

### Supported Requests
- [x] read  
- [x] search  
- [x] create  
- [x] update  
- [ ] delete

<br>

### Supported Resource Properties
````
{
    "id": "1",
    "resourceType": "MedicationStatement",
    "status": "inactive",
    "category": {
        "coding": [
            {
                "system": "clinikal/medicationStatement/category/medication",
                "code": "Lipitor"
            }
        ],
        "text": "Lipitor title"
    },
    "medicationCodeableConcept": {
        "coding": [
            {
                "system": "http://clinikal/valueset/Daa",
                "code": "A10"
            }
        ]
    },
    "subject": {
        "reference": "Patient/1"
    },
    "effectivePeriod": {
        "start": "2020-06-01",
        "end": "2020-06-07"
    },
    "dateAsserted": "2020-06-07 07:22:53T13:39:46.000Z",
    "informationSource": {
        "reference": "Practitioner/1"
    },
    "note": [
        {
            "text": "tell here more stuff"
        }
    ]
}
````

<br>

### Supported Operators

None


### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id||exact|
status||exact|
code||of-type| "system\|code\|identifier" *
patient||exact|

<br><br> 
 
*example  MedicationStatement?code:of-type=|codetype|codevalue
 
---


---


## [Observation](https://www.hl7.org/fhir/observation.html)

### Supported Requests
- [x] read  
- [x] search  
- [x] create  
- [x] update  
- [x] patch  
- [ ] delete

<br>

### Supported Resource Properties
````
{
    "id": "11",
    "resourceType": "Observation",
    "status": "1",
    "category": [
        {
            "coding": [
                {
                    "system": "http://hl7.org/fhir/ValueSet/observation-category",
                    "code": "vital-signs"
                }
            ],
            "text": "Vital Signs"
        }
    ],
    "subject": {
        "reference": "Patient/2"
    },
    "encounter": {
        "reference": "Encounter/1"
    },
    "issued": "2020-06-22T07:51:00.000Z",
    "performer": [
        {
            "reference": "Practitioner/1"
        }
    ],
    "note": [
        {
            "text": "דיאטה דחוף "
        }
    ],
    "component": [
        {
            "valueQuantity": {
                "value": "120",
                "system": "http://loinc.org",
                "code": "8480-6"
            }
        },
        {
            "valueQuantity": {
                "value": "85",
                "system": "http://loinc.org",
                "code": "8462-4"
            }
        },
        {
            "valueQuantity": {
                "value": "198.42",
                "system": "http://loinc.org",
                "code": "8335-2"
            }
        },
        {
            "valueQuantity": {
                "value": "72.05",
                "system": "http://loinc.org",
                "code": "8308-9"
            }
        },
        {
            "valueQuantity": {
                "value": "97.87",
                "system": "http://loinc.org",
                "code": "8310-5"
            }
        },
        {
            "valueQuantity": {
                "value": "120",
                "system": "http://loinc.org",
                "code": "8480-6"
            },
            "valueCodeableConcept": {
                "coding": [
                    {
                        "system": "http://loinc.org/8327-9",
                        "code": "Rectal"
                    }
                ]
            }
        },
        {
            "valueQuantity": {
                "value": "75.00",
                "system": "http://loinc.org",
                "code": "69000-8"
            }
        },
        {
            "valueQuantity": {
                "value": "60.00",
                "system": "http://loinc.org",
                "code": "9303-9"
            }
        },
        {
            "valueQuantity": {
                "value": "26.9",
                "system": "http://loinc.org",
                "code": "39156-5"
            }
        },
        {
            "valueQuantity": {
                "value": "120",
                "system": "http://loinc.org",
                "code": "8480-6"
            },
            "valueCodeableConcept": {
                "coding": [
                    {
                        "system": "http://loinc.org/59574-4",
                        "code": "Normal BL"
                    }
                ]
            }
        },
        {
            "valueQuantity": {
                "value": "72.00",
                "system": "http://loinc.org",
                "code": "8280-0"
            }
        },
        {
            "valueQuantity": {
                "value": "19.69",
                "system": "http://loinc.org",
                "code": "8287-5"
            }
        },
        {
            "valueQuantity": {
                "value": "30.00",
                "system": "http://loinc.org",
                "code": "20564-1"
            }
        },
        {
            "valueQuantity": {
                "value": "120",
                "system": "http://loinc.org",
                "code": "74774-1"
            }
        },
        {
            "valueQuantity": {
                "value": "8",
                "system": "http://loinc.org",
                "code": "72514-3"
            }
        },
        {
            "valueQuantity": {
                "value": "85",
                "system": "http://loinc.org",
                "code": "8462-4"
            }
        },
        {
            "valueQuantity": {
                "value": "198.42",
                "system": "http://loinc.org",
                "code": "8335-2"
            }
        },
        {
            "valueQuantity": {
                "value": "72.05",
                "system": "http://loinc.org",
                "code": "8308-9"
            }
        },
        {
            "valueQuantity": {
                "value": "97.87",
                "system": "http://loinc.org",
                "code": "8310-5"
            }
        },
        {
            "valueCodeableConcept": {
                "coding": [
                    {
                        "system": "http://loinc.org/8327-9",
                        "code": "Rectal"
                    }
                ]
            }
        },
        {
            "valueQuantity": {
                "value": "75.00",
                "system": "http://loinc.org",
                "code": "69000-8"
            }
        },
        {
            "valueQuantity": {
                "value": "60.00",
                "system": "http://loinc.org",
                "code": "9303-9"
            }
        },
        {
            "valueQuantity": {
                "value": "26.9",
                "system": "http://loinc.org",
                "code": "39156-5"
            }
        },
        {
            "valueCodeableConcept": {
                "coding": [
                    {
                        "system": "http://loinc.org/59574-4",
                        "code": "Normal BL"
                    }
                ]
            }
        },
        {
            "valueQuantity": {
                "value": "72.00",
                "system": "http://loinc.org",
                "code": "8280-0"
            }
        },
        {
            "valueQuantity": {
                "value": "19.69",
                "system": "http://loinc.org",
                "code": "8287-5"
            }
        },
        {
            "valueQuantity": {
                "value": "30.00",
                "system": "http://loinc.org",
                "code": "20564-1"
            }
        },
        {
            "valueQuantity": {
                "value": "120",
                "system": "http://loinc.org",
                "code": "74774-1"
            }
        },
        {
            "valueQuantity": {
                "value": "8",
                "system": "http://loinc.org",
                "code": "72514-3"
            }
        }
    ]
}
````

<br>

### Supported Operators

None


### Supported Resource Search Parameters

Parameter|Prefixes|Modifiers|OR Logic
--|--|--|--
_id||exact|
issued||exact|
patient||exact|
performer||exact|
status||exact|
encounter||exact|
category||exact|


<br><br> 
 
*example  MedicationStatement?code:of-type=|codetype|codevalue
 
---



## API Examples
Read request:  
`GET /apis/fhir/v4/Patient/:pid`

Search requests:  
`GET /apis/fhir/v4/Patient`  
`GET /apis/fhir/v4/Patient?_id=1`  
`GET /apis/fhir/v4/Patient?identifier=308826367`  
`GET /apis/fhir/v4/Patient?name=yosi&name=banana`  

Create request:  
`POST /apis/fhir/v4/Patient`  

Update request:  
`PUT /apis/fhir/v4/Patient/:pid`  

Patch request:  
`PATCH /apis/fhir/v4/Patient/:pid`  
``` json
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


Delete request:  
`DELETE apis/fhir/v4/DocumentReference/22` 

success
 
```
{
    "resourceType": "OperationOutcome",
    "text": {
        "status": "generated"
    },
    "issue": [
        {
            "severity": "information",
            "code": "informational",
            "diagnostics": "Successfully deleted 1 resource(s)"
        }
    ]
}
```

<br><br> 

fail
 
```
{
    "resourceType": "OperationOutcome",
    "text": {
        "status": "generated"
    },
    "issue": [
        {
            "severity": "error",
            "code": "processing",
            "diagnostics": "Unable to delete DocumentReference/22.failed to delete from doc db"
        },
        {
            "severity": "information",
            "code": "information",
            "diagnostics": "HTTP Error with status 400 occoured while requesting"
        }
    ]
}
```

<br><br> 
