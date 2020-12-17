# Documents storage

Clinikal supports 2 options to store documents, using [AWS S3](https://aws.amazon.com/s3/) or CouchDB (supported also by OpenEMR).
In the storage are saved all the discharge letters and the uploaded files.

## AWS S3 settings
In the **Administration** -> **Globals** -> **Clinikal Storage**

| **Settings**                           | **Description**                                                                                                                                                                                             |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Clinikal storage method                | select S3
| S3 API version                         | leave it as '2006-03-01'
| S3 bucket region                       | Your [AWS region](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-available-regions)
| S3 bucket name                         | The bucket name in the S3
| S3 files path                          | Path to selected folder in S3
The url to file will be built from those parameters (e.g s3://bucket_name/path/to/1607034941_summary_letter_patient_1_2020-12-04 00:35:41.pdf)

 
## CouchDB settings
In the **Administration** -> **Globals** 

In the **Clinikal Storage** 

| **Settings**                           | **Description**                                                                                                                                                                                             |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Clinikal storage method                | select CouchDB

In the **Documents**

| **Settings**                           | **Description**                                                                                                                                                                                             |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Document Storage Method               | select CouchDB
| CouchDB HostName                      | CouchDB host
| CouchDB UserName                       | User name 
| CouchDB Password                     | Password (saved encrypt in the database)
| CouchDB Port                          | Port 
| CouchDB Database                   | Database name
