Simple-Wordpress-Multisite
==========================

Run multiple Wordpress sites on separate databases using 1 Wordpress installation without the plugins or htaccess configurations.

The Benefits
------------

 - separate databases for each site mean better performance
 - 
 - single updating on 1 core installation of Wordpress + Wordpress Plugins
 - no htaccess hassle

Why Not Wordpress Multi Site?
-----------------------------
Multi site is great and offers many features allowing you to control user access.
 - domain mapping is not needed
 - each domain will have its on uploads directory for images
 - again, the dbs are completely separate

Installation Instructions
=====================

1.Create define your private string
----------
> - an example string would be xciU23Xpo  ( any randomly generated string can be used here )
> - this string will be prepended to your db name ( xciU23XpoMYSITENAME )
> - since your dbname and passwords are usually different. Your private string should also be set as your password for all sites
> **NOTE: Wordpress Multi-site normally uses the same method. One db username with one db password **

2.Setup Databases and Define Domains
---------
remember the database name should be your domain name and prepend the    private string you made.

    example: private string + MYSITENAME = gh8YG5O1PpMYSITENAME


In your hosting panel, point all Wordpress domains you have to the single Wordpress directory on your server.


    example:foo.com -points to-> /path/to/wordpress
            foo2.com -points to-> /path/to/wordpress
            foo3.com -points to-> /path/to/wordpress
    
    

 Copy the wp-config.php file in this repo into a text editor and change the privateString and DB_USER into your own.

    $privateString = 'gh8YG5O1PpD07C8B7UT1qKiR6p2K1P97';
    define('DB_USER', 'universal_dbuser_for_all_sites');
    


3. Begin Wordpress Setup
---------

> - Go to your first domain and initalize wordpress installer.


4. COMPLETED!!
---------
>- if you encounter any errors like db connection error, check to make sure your private password matches the one used during the database creation.
>- you can now log into each domain using a single Wordpress Installation

Caveates
--------
***Specify upload path per site using this code in your themes function.php***
***This will keep the upload path for every site nice and organized***

    add_filter( 'pre_option_upload_path', 'upload_path_files' );
        function upload_path_files(){
         return 'sites/'.array_shift(explode(".",$_SERVER['HTTP_HOST'])).'/uploads';  
        }
        
Also, pertaining to the db naming sequence. You can use what ever sequence you choose.
As long as the sequence matches the one created in the database name.


The Gotchas
--------------

 1. Plugins and Themes are visible across all sites
 2. No Network admin panel for disabling user access to plugins and themes
 3. sitemaps will overwrite each other

The Solutions
-------------

 1. set users role as editor
 2. using site theme to disconnect access to admin functions
 3. sitemaps will need a prefix of domain-name_sitemap.xml to avoid overwrites.
