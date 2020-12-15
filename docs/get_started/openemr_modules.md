# Manual installation

These instructions assume you already have a working [Openemr application installed](https://www.open-emr.org/wiki/index.php/OpenEMR_Installation_Guides).  

## Fhir API modules

### Setup Composer File
Add the following to the openemr/composer.json:  
``` json
"repositories": [
    {
        "type": "vcs",
        "url": "git@github.com:israeli-moh/clinikal-backend.git"
    },
    {
        "type": "vcs",
        "url": "git@github.com:israeli-moh/composer-installers-clinikal-extender.git"
    }
],
"require": {
    "clinikal/clinikal-backend": "dev-master",
    "clinikal/composer-installers-clinikal-extender": "dev-master"
},
"extra": {
    "installer-types": [
        "clinikal-vertical"
    ],
}
```
<br>

### Run Composer
In a terminal, `cd` into the openemr root directory (where the composer.json is), and run:  
```
composer update clinikal
```  
  
This downloads the modules code into the openemr/vendor/clinikal and triggers the composer installer extension in the composer-installers-clinikal-extender repository.  
The extension creates links from the files in vendor/clinikal to there appropriate places in the openemr codebase.  
This enables us to use the vertical's modules, styles, and menus.  
<br>

### Install Modules
In the **Modules** -> **Manage Modules** screen, **Register** then **Install** the following modules (in this order):  
1) GenericTools  
2) FhirAPI  

The [Fhir API](https://clinikal-documentation.readthedocs.io/en/latest/api/fhir/) modules can stand alone for for a variety of uses.

## Clinikal modules - for React client app

### Setup Composer File
Add the following to the openemr/composer.json (In addition to settings from prev section):<br>
**Currently available modules for Emergency center**  
``` json
"repositories": [
    {
        "type": "vcs",
        "url": "git@github.com:israeli-moh/vertical-emergency-medicine-backend.git"
    }
],
"require": {
    "clinikal/vertical-emergency-medicine-backend": "dev-master",
}
```
<br>

### Run Composer
In a terminal, `cd` into the openemr root directory (where the composer.json is), and run:  
```
composer update clinikal
```  
  
This downloads the modules code into the openemr/vendor/clinikal and triggers the composer installer extension in the composer-installers-clinikal-extender repository.  
The extension creates links from the files in vendor/clinikal to there appropriate places in the openemr codebase.  
This enables us to use the vertical's modules, styles, and menus.  
<br>

### Install Modules
In the **Modules** -> **Manage Modules** screen, **Register** then **Install** the following modules (in this order):  
1) ClinikalApi  
2) EmergencyMedicine  
3) ImportData  
4) ReportTool

## Install React app

1. clone repository from Github - `https://github.com/israeli-moh/clinikal-react`
2. Run `npm install`
3. Creat new .env.local in the project root and add single parameter named `REACT_APP_API_BASE_URL=<OPENEMR_DOMAIN>` into file.  
4. Run `npm start` for development mode OR `npm run build` for production.
