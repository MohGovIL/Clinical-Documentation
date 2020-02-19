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
- [X] patch only replace

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

####Patch
> PATCH /apis/fhir/v4/Appointment/:aid  

**Request body:** 

Example - change status
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
####Read

**Request:**
> GET /apis/fhir/v4/Appointment/:aid

####Search
**Request:**
> GET /apis/fhir/v4/Appointment?date=ge2019-01-16&date=le2020-01-30&_include=Appointment:patient

**params examples**

*date=2020-01-28*

*date=ge2020-01-28*

*date=le2020-01-28*

*status:not=arrived*

*actor:HealthcareService.organization=3*

*service-type=5*

*_include=Appointment:patient*

*_sort=date,-priority,service-type*

*_sort=date*

*_id=5*

*_summary=count*

```
{
  "resourceType": "Bundle",
  "type": "searchset",
  "timestamp": "2020-02-19T15:54:27.000Z",
  "total": 9,
  "entry": [
    {
      "response": {
        "status": "200",
        "outcome": {
          "resourceType": "OperationOutcome"
        }
      }
    }
  ]
}
```

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
- [x] search [Search Parameters](https://www.hl7.org/fhir/encounter.html#search)
    - [x] [simple string search](https://www.hl7.org/fhir/search.html#string) [_id, date,status,appointment,patient]
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) appointment
    - [x] [include](https://www.hl7.org/fhir/search.html#include) subject.patient
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) participant.practitioner
- [ ] create
- [ ] update
- [ ] delete

GET /apis/v4/Encounter/1 

GET /apis/v4/Encounter (all)

GET /apis/v4/Encounter?_id=8

GET /apis/v4/Encounter?_id=8&status=planned&status=in progress  (or operator)

GET /apis/v4/HealthcareService?appointment=5&patient=78

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
```
/apis/fhir/v4/Encounter

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?_id=8&status=planned&status=in_progress

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":0,"resourceType":"Encounter","status":null,"priority":{"coding":[[]]},"period":[]},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?appointment=2&patient=3

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":0,"resourceType":"Encounter","status":null,"priority":{"coding":[[]]},"period":[]},"search":{"mode":"match"}}]}/apis/fhir/v4/Encounter/1{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}}

 

/apis/fhir/v4/Encounter?date=gt2020-02-09

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?_id=1

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?date=eq2020-02-09

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?appointment=1&patient=2

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":0,"resourceType":"Encounter","status":null,"priority":{"coding":[[]]},"period":[]},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?date=eq2020-02-09

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?_include=Encounter:patient

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}},{"resource":{"id":1,"resourceType":"Patient","identifier":[{"value":"45640"}],"name":[{"family":"דג","given":["דגי"]}],"gender":"male","birthDate":"2020-01-01","deceasedBoolean":false},"search":{"mode":""}}]}

 

/apis/fhir/v4/Encounter?_sort=-date,patient

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?_sort=date

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:52.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

/apis/fhir/v4/Encounter?_sort=date,-priority,service-type

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:53.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Encounter?_sort=-date

 

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:53.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":1,"resourceType":"Encounter","status":"planned","priority":{"coding":[{"code":"2"}]},"subject":{"reference":"Patient/1"},"participant":[{"individual":{"reference":"Practitioner/1"}}],"period":{"start":"2020-02-09 00:00:00"},"serviceProvider":{"reference":"Organization/4"}},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Organization?_id=3&active=1

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:53.000Z","total":1,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":3,"resourceType":"Organization","name":"Your Clinic Name Here","telecom":[{"system":"phone","value":"035519966","use":"work"}]},"search":{"mode":"match"}}]}

 

/apis/fhir/v4/Organization

{"resourceType":"Bundle","type":"searchset","timestamp":"2020-02-18T10:20:53.000Z","total":2,"entry":[{"response":{"status":"200","outcome":{"resourceType":"OperationOutcome"}}},{"resource":{"id":3,"resourceType":"Organization","name":"Your Clinic Name Here","telecom":[{"system":"phone","value":"035519966","use":"work"}]},"search":{"mode":"match"}},{"resource":{"id":4,"resourceType":"Organization","name":"מחוז אשקלון","telecom":[{"system":"fax","value":"+972-546-837-767"},{"system":"phone","value":"+972-546-837-766","use":"work"}],"address":[{"line":["שד הפלי\"ם 15א"],"city":"חיפה","state":"32"}]},"search":{"mode":"match"}}]}



```
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
- [x] search - [Search Parameters](https://www.hl7.org/fhir/healthcareservice.html#search) [active, _id, service-type, organization, name]
    - [x] [Basic](https://www.hl7.org/fhir/search.html#string) (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix)) 
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

> GET /apis/fhir/v4/HealthcareService/:id

<br>
<br>

### Search

Example showing how to use parameters:  

> GET /apis/fhir/v4/HealthcareService?_id=3&name=ClintonServices


Parameter|Database Table|Database Column\s|Note
--|--|--|--
_id|fhir_healthcare_services|id|
active|fhir_healthcare_services|active|
name|fhir_healthcare_services|name|
organization|fhir_healthcare_services|providedBy|
service-type|fhir_healthcare_services|type|