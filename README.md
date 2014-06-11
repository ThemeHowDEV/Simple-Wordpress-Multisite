Simple-Wordpress-Multisite
==========================

Run multiple Wordpress sites on separate databases using 1 Wordpress installation

Installation Instructions
=====================


----------


1.Create Databases for all domains
---------

> **NOTE:**
> 
> - remember the database name, user and password. These will be needed later.

2. Begin Wordpress Setup
---------
>- Log into your Hosting panel and point your domains to the wordpress folder installed on your server.

3. Begin Wordpress Setup
---------

> - Go to your first domain and initalize wordpress installer. This will allow Wordpress to generate the needed wp-config file for next step.
- after successfully installing your first domain.
- Access your wp-config file using ftp.
- Paste the code contained in the below snippet into your 'wp-config.php' file.


4. COMPLETED!!
---------
>- update the neccessary fields for each domain.
>- you can now log into each domain using a single Wordpress Installation

Caveates
--------
***Specify upload path per site using this code in your theme function.php***

    add_filter( 'pre_option_upload_url_path', 'subdomain_upload_url' );
    function subdomain_upload_url()
    {
     return 'http://cloud.'.str_replace('http://','',get_bloginfo('url'));
    }
