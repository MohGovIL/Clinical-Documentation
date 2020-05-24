# Setup Composer File
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

# Run Composer
In a terminal, `cd` into the openemr root directory (where the composer.json is), and run:  
```
composer update clinikal
```  
  
This downloads the modules code into the openemr/vendor/clinikal and triggers the composer installer extension in the composer-installers-clinikal-extender repository.  
The extension creates links from the files in vendor/clinikal to there appropriate places in the openemr codebase.  
This enables us to use the vertical's modules, styles, and menus.  
<br>

# Install Modules
In the **Modules** -> **Manage Modules** screen, **Register** then **Install** the following modules (in this order):
1) GenericTools
2) FhirAPI