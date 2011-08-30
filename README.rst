=====================================
Facebook Ignited v1.0.6 Documentation
=====================================
Both of the projects merged into this project are open source projects.
I make no claim to their origin just the work put into expanding on them 
and making their functionality more accessable.

You can view CodeIgniter at http://codeigniter.com and Facebook PHP SDK at 
https://github.com/facebook/php-sdk/ if you have any bugs regarding them please 
check their coresponding sites. 

As of this this version I am using CI v2.0.3 & FB SDK v3.1.1.

Thanks! And I hope you enjoy this preconfigured version of Facebook Ignited!

-deth4uall aka Rev. Alfonso E Martinez, III


Instructions for Installation
=============================

You will need a few things for this to work correctly: 
	
1) This code 
2) Hosting with PHP support
3) A facebook application

You can register your app at http://www.facebook.com/developers

Once you have all those steps done, and you have set up your hosting and added that to your
app in the developers panel of facebook. You will need to edit a few files in this code.

The following page you will need to change the variables to that found in your Dev Panel.
	
	``application/config/fb_ignited.php``
	
One of the configurations you will need to pay close attention  to: ``$config['fb_apptype']`` If you set it to 
iframe only use the info you put in the dev panel of your app. Eg. ``facebook-ignited`` in ``http://apps.facebook.com/facebook-ignited/`` 
otherwise put the whole domain name excluding the ``http://`` or ``https://``.

After that you can load the example page and start to learn from there!

Once you have the system loaded for first time, please go and read: 

https://bitbucket.org/deth4uall/facebook-ignited/wiki/Home 
and 
https://bitbucket.org/deth4uall/facebook-ignited/wiki/API

It will explain what the features do. Please note that I will only provide limited support to 
people who have editted their 'application/libraries/Fb_ignited.php' file. As stated at the top 
of the file it can cause disruption of app stability, please wait for me to either reply with a fix 
or upload a new version. I am quick to respond and will make every effort to find a solution.

Instructions for Using Facebook Ignited
=======================================

In order for you to get the system started on other files you will need to call:

	``$this->fb_me = $this->fb_ignited->fb_get_me();``

This will allow you to check if they are logged in, and if they are authenticated, if either one is not 
true it will redirect them to the correct page so that they may do so. It also allows you to view all of the 
information from ->api('/me').

Any and all facebook functions can be called via the ``$this->fb_ignited->api()`` format. If it is not within 
Facebook Ignited class it will call it from the facebook class which is called via the fb_ignited system, acting 
as a shell for Facebook SDK. 

As a added bonus the system now supports facebook credits, if you want use the system as it is create a database and 
use this database query::

	CREATE TABLE `fb_item_store` (
	`item_id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY ,
	`title` VARCHAR( 50 ) NOT NULL ,
	`price` INT NOT NULL ,
	`description` VARCHAR( 100 ) NOT NULL ,
	`image_url` VARCHAR( 100 ) NOT NULL ,
	`product_url` VARCHAR( 100 ) NOT NULL
	) ENGINE = MYISAM CHARACTER SET utf8 COLLATE utf8_general_ci;
	CREATE TABLE `fb_item_cache` (
	`userid` BIGINT NOT NULL ,
	`item_id` INT NOT NULL ,
	`order_id` BIGINT NOT NULL ,
	`finalized` INT NOT NULL,
	`time` BIGINT NOT NULL,
	KEY `userid` ( `userid` )
	) ENGINE = MYISAM CHARACTER SET utf8 COLLATE utf8_general_ci;

Also ensure that you have the database info for that database added into the ``/config/database.php`` file and that 
you auto-load the database class. This will allow the facebook processing function to automatically add the items to 
the fb_item_cache table so that users can grab them. You will need to make sure that you remove them from the 
fb_item_cache table so that they do not get duplicates.
