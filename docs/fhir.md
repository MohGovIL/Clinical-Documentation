#FHIR API

<https://www.hl7.org/fhir/http.html>


##[Patient](https://www.hl7.org/fhir/patient.html)

- [x] read
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/patient.html#search)
    - [x] [Parameters](https://www.hl7.org/fhir/patient.html#search)_id, identifier,name (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix))
    - [ ] [:contains and :exact](https://www.hl7.org/fhir/search.html#string) for name and id

- [ ] create
- [ ] update
- [ ] delete

####supported parameters
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
    "deceasedBoolean": 0,
    "address": [
      {
        "use": "both",
        "line": [
          "3",
          "34"
        ],
        "city": "city_3000",
        "postalCode": "4517200",
        "country": "country_254"
      }
    ]
  }
```


####Read

**Request:**
> GET /apis/v4/Patient/:pid

####search

**Request:**

> GET /apis/fhir/v4/Patient

> GET /apis/fhir/v4/Patient?_id=1

> GET /apis/fhir/v4/Patient?identifier=308826367

> GET /apis/fhir/v4/Patient?name=yosi&name=banana



##[Appointment](https://www.hl7.org/fhir/appointment.html)

- [x] read
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/appointment.html#search)
    - [X] [Basic](https://www.hl7.org/fhir/search.html#string) (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix))
    - [X] [Range time](https://www.hl7.org/fhir/search.html#date) prefix parameter for range time
    - [X] [include](https://www.hl7.org/fhir/search.html#include) patient
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) HealthcareService
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) Practitioner
- [ ] create
- [x] update
    -[x] update status
- [ ] delete

####supported parameters
````
{
  "id": 8,
  "resourceType": "Appointment",
  "status": "pending",
  "serviceType": [
    {
      "coding": [
        {
          "code": "17"
        }
      ],
      "text": "ביקור שגרתי - רופא"
    }
  ],
  "description": "ביקור שגרתי - רופא",
  "start": "2020-01-15T11:00:00.000Z",
  "end": "2020-01-15T12:00:00.000Z",
  "minutesDuration": "60",
  "comment": "יש לי מה להגיד",
  "participant": [
    {
      "actor": {
        "reference": "Patient/2",
        "display": "Idan Gigi"
      }
    }
  ]
}
````
####Read

**Request:**
> GET /apis/fhir/v4/Appointment/:aid

####Search
**Request:**
> GET /apis/fhir/v4/Appointment?date=ge2019-01-16&date=le2020-01-30&_include=Appointment:patient

####Patch
> PATCH /apis/fhir/v4/Appointment/:aid  

**Request body:** 

Example - change status
```
[
   {
      op:"replace",
      path:"/status",
      value:"noshow"
   }
]
```


##[Encounter](https://www.hl7.org/fhir/encounter.html)

- [ ] read
- [ ] search [Search Parameters](https://www.hl7.org/fhir/encounter.html#search)
    - [ ] [simple string search](https://www.hl7.org/fhir/search.html#string) [_id, date,status,appointment,patient]
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) appointment
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) subject.patient
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) participant.practitioner
- [ ] create
- [ ] update
- [ ] delete

####supported parameters
````
{
    "id": 1,
    "resourceType": "Encounter",
}
````

##[practitioner](https://www.hl7.org/fhir/practitioner.html)

- [ ] read
- [ ] search 
    - [ ] [simple string search](https://www.hl7.org/fhir/search.html#string)
- [ ] create
- [ ] update
- [ ] delete

####supported parameters
````
{
    "id": 1,
    "resourceType": "practitioner",
}
````

##[Organization](https://www.hl7.org/fhir/organization.html) 

- [ ] read
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/organization.html#search)  [active, _id, name]
    - [ ] [Basic](https://www.hl7.org/fhir/search.html#string) (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix)) 
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) Organization (part of)
- [ ] create
- [ ] update
- [ ] delete

####supported parameters
````
{
    "id": 1,
    "resourceType": "Organization",
}
````


##[HealthcareService](https://www.hl7.org/fhir/organization.html)

- [ ] read
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/healthcareservice.html#search) [active, _id, identifier, service-type, organization, name]
    - [ ] [Basic](https://www.hl7.org/fhir/search.html#string) (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix)) 
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) Organization (providedBy)
- [ ] create
- [ ] update
- [ ] delete

####supported parameters
````
{
    "id": 1,
    "resourceType": "HealthcareService",
}
````



