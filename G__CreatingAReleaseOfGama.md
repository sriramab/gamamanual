# Product a release of GAMA
## Configure your IDE in order to allow multi-platform builds
This is works not only with the Mars release, but also previous releases, as well.
* Open Window/Preferences.
* Find PDE/Target Platform
* Select your (active) target platform
* Click Edit
* Click Add
* Select "Software Site"
* Click Next
* In "Work With" type: http://download.eclipse.org/eclipse/updates/4.5 (replace 4.3 with your current version)
* Check "Eclipse RCP Target Components"
* Check "Equinox Target Components"
* Uncheck "Include required software"
* Check "Include all environments"
* Press Finish
* Press Finish
* Press OK

Open your product file and select the "Export" option. You will see that the "Export for multiple platforms" checkbox is available.



Ce qui n'est pas nécessaire

Pas besoin Installation de EMF.Validation

Installation de  Equinox Target Components	3.11.1.v20150831-1342	org.eclipse.equinox.sdk.feature.group	Eclipse  
pasEquinox Project
Suppression des dépendance cassé vers windows et linux
