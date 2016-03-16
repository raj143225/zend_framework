# Server Setup Architecture:

* Please check the software versions to check the softwares required for the application.
* Application needs to be set up using the virtual host.
* In virtual host setting the server needs to point to the index file under the "public" directory
* Following code needs to be in the virtual setting,
	1. For allowing few files access directly
	2. Set the environment(Development | Testing | Production)
	3. Need to put the Zend library inside the include path or you can add a new include path as shown below

	    RewriteEngine on  
	    RewriteCond %{REQUEST_FILENAME} !-f  
	    RewriteCond %{REQUEST_FILENAME} !-d  
	    RewriteRule !\.(js|ico|gif|jpg|png|css|woff|eot|svg|ttf)$ /index.php  

    SetEnv ENVIRONMENT [Environment]  
    **php_value include_path** ".;C:/xampp/php/zendframework/1.12.0;C:/xampp/php/PEAR"

 
 ##Software Versions:
* PHP 5.4
* Mysql 5.6
* Zend Framework 1.12

 
 ##PM System Used:
* [JIRA] (https://rapidfunnel.atlassian.net)
* [GIT] (https://bitbucket.org/rapidfunnel/web-application)
