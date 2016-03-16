=============================
Developer Environment Setup:
=============================

##Project SetUP:
* Please check the software versions from (General-Information.txt) to check the softwares required for the application.
* Code can be pulled from [GIT](https://bitbucket.org/rapidfunnel/web-application)
* Application needs to be set up using the virtual host.
* In virtual host setting the server needs to point to the index file under the "public" directory
* Following code needs to be in the virtual setting:
	1. For allowing few files access directly
	2. Set the environment(Development | Testing | Production)
	3. Need to put the Zend library inside the include path or you can add a new include path as shown below

		php_value upload_max_filesize 100M
		php_value post_max_size 100M
	
		RewriteEngine on
		RewriteCond %{REQUEST_FILENAME} !-f
		RewriteCond %{REQUEST_FILENAME} !-d
		RewriteRule !\.(js|ico|gif|jpg|jpeg|png|css|woff|eot|svg|ttf)$ /index.php
		ErrorDocument 404 /system/resource/error

    SetEnv ENVIRONMENT [Environment]
    php_value include_path ".;C:/xampp/php/zendframework/1.12.0;C:/xampp/php/PEAR"


##Database SetUP:
* Please get the DB files from the location <ProjectDirectoryName>/sql/ and create DB


##Config Modification:
* Modify data in the config files under <ProjectDirectoryName>/lib/RapidFunnel/Config/ based on your environment.
* Also check the commonCofig.ini for common config settings under above mentioned location.


##External Libraries:
* Need few external libraries, as mentioned below with their version
* Then libraries of specific version can be downloaded using composer in <ProjectDirectoryName>/lib/composer.json
* Following libraries have been used
	1. "mailgun/mailgun-php": **~1.7.1**,
	2. "ext-curl": *,
	3. "authorizenet/authorizenet": **1.8.0**


##phpUnit For Testing:
* Needs to install phpUnit / there also exists the phpunit.php file under <ProjectDirectoryName>/tests/
* Few constants for phpUnit testing needs to be modified in <ProjectDirectoryName>/tests/app/bootstrap.php
* Xdebug needs to be installed for Unix systems or Xdebug module can be enabled in windows systems to make unit testing functional.
