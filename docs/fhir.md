#FHIR API

<https://www.hl7.org/fhir/http.html>


##[Patient](https://www.hl7.org/fhir/patient.html)

- [x] read
- [ ] search 
    - [ ] [simple string search](https://www.hl7.org/fhir/search.html#string)
- [ ] create
- [ ] update
- [ ] delete

###supported parameters
| Name     |      Details   | 
| ---------- | --------------|
| id |               | 
| resourceType |               | 
| identifier |               | 
| name.family |               | 
| name.given |               | 
| gender |               | 
| birthDate |               | 
| deceasedBoolean |               | 

###Read

**Request:**
> GET /apis/v4/Patient/:pid


##[Appointment](https://www.hl7.org/fhir/appointment.html)

- [x] read
- [ ] search 
    - [ ] [simple string search](https://www.hl7.org/fhir/search.html#string)
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) patient
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) HealthcareService
    - [ ] [include](https://www.hl7.org/fhir/search.html#include) Practitioner
- [ ] create
- [ ] update
- [ ] delete

###supported parameters
| Name     |      Details   | 
| ---------- | --------------|
| id |               | 
| resourceType |               | 
| identifier |               | 


###Read

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

###supported parameters
| Name     |      Details   | 
| ---------- | --------------|
| id |               | 
| resourceType |               | 
| identifier |               | 


###Read

**Request:**
> GET /apis/v4/Encounter/:eid
