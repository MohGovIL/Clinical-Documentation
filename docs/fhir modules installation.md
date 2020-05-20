# Setup Composer File
1) Go to the `composer.json` file under the openemr root directory.  
2) Add the following json objects to the "repositories" array: 
```
{
    "type": "vcs",
    "url": "https://github.com/israeli-moh/clinikal-backend.git"
},
{
    "type": "vcs",
    "url": "https://github.com/israeli-moh/composer-installers-clinikal-extender.git"
}
```
3) Add the following json object to the root json object:
```
"extra": {
        "installer-types": [
            "clinikal-vertical"
        ]
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
1) Open openemr in the web browser and login  
2) In the top navigation menu, choose **Modules** -> **Manage Modules**  
3) Go to the **Unregistered** tab  
4) Next to the GenericTools module, click on **Register**  
5) Go back to the **Registered** tab  
6) Next to the GenericTools module, click on **Install**  
7) Do the same for the FhirAPI module (steps 3-7) 