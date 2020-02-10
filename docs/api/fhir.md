# FHIR API

<https://www.hl7.org/fhir/http.html>


##[Patient](https://www.hl7.org/fhir/patient.html)

- [x] read
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/patient.html#search)
    - [x] [Parameters](https://www.hl7.org/fhir/patient.html#search)_id, identifier,name (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix))
    - [ ] [:contains and :exact](https://www.hl7.org/fhir/search.html#string) for name and id

- [x] create
- [X] update
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



####Create

**Request:**
> POST /apis/v4/Patient

**body:** fhirPatient

####Update

**Request:**
> PUT /apis/v4/Patient/:pid

**body:** fhirPatient
**note:** can not update pid
<br><br> 

---

<br><br>  

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

<br><br> 

---

<br><br>  

##[Encounter](https://www.hl7.org/fhir/encounter.html)

- [x] read
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
  "resourceType": "Encounter",
  "meta": {
    "versionId": 1,
    "lastUpdated": "",
    "source": ""
  },
  "status": "",
  "serviceType": {
    "coding": [
      {
        "code": "5"
      }
    ]
  },
  "participant": [
    {
      "individual": {
        "reference": "/Practitioner/1"
      }
    }
  ],
  "appointment": [
    {
      "reference": "/Appointment/11"
    }
  ],
  "period": {
    "start": "2020-01-27 00:00:00"
  },
  "serviceProvider": {
    "reference": "/Organization/3"
  }
}
````

<br><br> 

---

<br><br>  

##[Practitioner](https://www.hl7.org/fhir/practitioner.html)

- [x] read
- [x] search 
    - [x] [simple string search](https://www.hl7.org/fhir/search.html#string)
- [ ] create
- [ ] update
- [ ] delete

####supported parameters
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

####Read

**Request:**
> GET /apis/fhir/v4/Practitioner/:id


####search

**Request:**
> GET /apis/fhir/v4/Practitioner?name=yosi&active=1

<br><br> 

---

<br><br>  

##[Organization](https://www.hl7.org/fhir/organization.html) 

- [X] read
- [X] search - [Search Parameters](https://www.hl7.org/fhir/organization.html#search)  [active, _id, name]
    - [X] [Basic](https://www.hl7.org/fhir/search.html#string) (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix)) 
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) Organization (part of)
- [ ] create
- [ ] update
- [ ] delete

####supported parameters
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

<br><br> 

####Read

**Request:**

> GET /apis/fhir/v4/Organization/:id


####search

**Request:**

Basic search

only parameters - active, _id, name from -https://www.hl7.org/fhir/organization.html#search 

Some examples

In this task we implement only AND operator (Each parameter can only be added once)

GET /apis/v4/Organization (all)

GET /apis/v4/Organization?_id=8

GET /apis/v4/Organization?_id=8&active=1

GET /apis/v4/Organization?name=לשכת בריאות חיפה

GET /apis/v4/Organization?name=חיפה&active=1

<br><br> 

---

<br><br> 

## [HealthcareService](https://www.hl7.org/fhir/organization.html)

- [x] read
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/healthcareservice.html#search) [active, _id, identifier, service-type, organization, name]
    - [ ] [Basic](https://www.hl7.org/fhir/search.html#string) (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix)) 
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) Organization (providedBy)
- [ ] create
- [ ] update
- [ ] delete

<br>

### Supported Parameters:

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

### Read

```
GET /apis/fhir/v4/HealthcareService/:id
```
