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
> /apis/v4/Patient/:id

