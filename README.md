 #File Storage:

* An extra volume added to store resource files.
* Create a soft link of proper partition(for ex: /mnt/volume-1/resource_s1) into project/public
* Create a directory "account" inside resource and grant proper permission.


#Server Setting

*Need to remove rewrite rule from virtualhost setup file (/etc/apache2/sites-enabled/...) and put it in .htaccess file with proper entries.
*Note that .htaccess is already added in the server.
