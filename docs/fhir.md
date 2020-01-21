#FHIR API

<https://www.hl7.org/fhir/http.html>


##[Patient](https://www.hl7.org/fhir/patient.html)

- [x] read
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/patient.html#search)
    - [ ] [Basic](https://www.hl7.org/fhir/search.html#string) (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix))
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


##[Appointment](https://www.hl7.org/fhir/appointment.html)

- [x] read
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/appointment.html#search)
    - [ ] [Basic](https://www.hl7.org/fhir/search.html#string) (without [modifiers](https://www.hl7.org/fhir/search.html#modifiers) and [prefix](https://www.hl7.org/fhir/search.html#prefix))
    - [ ] [Range time](https://www.hl7.org/fhir/search.html#date) prefix parameter for range time
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) patient
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) HealthcareService
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) Practitioner
- [ ] create
- [ ] update
- [ ] delete

####supported parameters
````
{
    "id": 1,
    "resourceType": "Appointment",
}
````
####Read

**Request:**
> GET /apis/v4/Appointment/:aid



##[Encounter](https://www.hl7.org/fhir/encounter.html)

- [ ] read
- [ ] search 
    - [ ] [simple string search](https://www.hl7.org/fhir/search.html#string)
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
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/organization.html#search)
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
- [ ] search - [Search Parameters](https://www.hl7.org/fhir/healthcareservice.html#search)
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

