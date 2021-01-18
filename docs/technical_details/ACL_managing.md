Clinikal comes with extensive Access Control System that based on [OpenEMR ACL](https://www.open-emr.org/wiki/index.php/Access_Controls_Listing).  
In our modules we create new Access roles, sections and objects according to the clinic type (e.g. the imaging clinic needed X-ray technician what that not needed in the other clinics).  
The settings of the ACL are written in every module in the `acl` folder in the `acl_setup.php` and `acl_upgrade.php` and use functions from class `OpenEMR\Common\Acl\AclExtended` for the configurations.

**Example of useful ACL functions**  
Add new role (nurse for emergency center with view permission):  
```injectablephp
$emergency_nurse_view =AclExtended::addNewACL('Emergency nurse', 'emergency_nurse', 'view', 'Things that emergency nurse can read but not modify');
```
new ACL object for Encounter report:  
```injectablephp
AclExtended::addObjectAcl('client_app', 'Client Application', 'EncountersReport','Encounters Report');
```

Allow nurse to show Encounter report:  
```injectablephp
AclExtended::updateAcl($emergency_nurse_view, 'Emergency nurse', 'client_app', 'Client Application', 'EncountersReport','Encounters Report', 'view');
```

The ACL setting can be modified in the administration interface of OpenEMR - _Administration -> ACL_
![Screenshot](acl_screen.png)