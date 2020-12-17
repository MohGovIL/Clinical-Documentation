
# Internationalization

This project sponsored by Israeli Ministry Of Health to promote EMR products in Israel and designed first for Israeli developers community.

Therefore the initial status after installation compatible with Israeli clinics by default.

Most of Israeli behavior enable to change by settings manager and part waiting to development in the future. 

**Languages**  
The default language of the system when you setup Emergency medicine clinic is Hebrew.  
To change language go to Globals setting in the Openemr project, **Administration** -> **Globals** -> **Locale** -> **Default Language**.  
Currently the language of client application is based on Openemr languages system, the application support Hebrew and English and can be extend using [Openemr tools](https://www.open-emr.org/wiki/index.php/OpenEMR_Internationalization_Translator_Guide).

Future language features-
* client-side translation based on i18n files.
   

**Format date**  
The default format date is `'DD/MM/YYYY'`.  
Can be changed in **Administration** -> **Globals** -> **Locale** 

**Identifier types**  
The system is initialed with list of identifier types that in used in Israel.  
The list can be changed in **Administration** -> **Forms** -> **Lists** -> **User Defined List 3** 

**HMOs**
Every patient must be a member of the HMO.   
 
  
