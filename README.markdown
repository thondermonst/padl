# PHP Aplication Distribution Licensing

## What is PADL?

A class to generate and validate licenses for a domain, restricting
an expire date.

## Demo

See the [PADL Site](http://padl.rgou.net).

## History

PADL is a originaly written in 2005 by Oliver Lillie under older PHP4, 
parked on PHPCLASSES site. You can find the original code as part as 
this distribution or directelly in 
http://www.phpclasses.org/package/2298-PHP-Generate-PHP-application-license-keys.html .

It was updated to PHP 5.2,5.3 by Raphael Goulart (https://github.com/rafaelgou/padl)

And later modified to use composer by me

You can find more about the original author in:

* [PHP CLASSES: Classes of Oliver Lillie](http://www.phpclasses.org/browse/author/122732.html)
* [PHP CLASSES: Professional profile of Oliver Lillie](http://www.phpclasses.org/professionals/profile/9072/)
* Otherwise a lot of modifications has been made, all core methods and examples 
  are or just a copy or strongly based on the original project.

### Generate:

    /*
    Instance of License
    parameters:
    - useMcrypt
    - useTime
    - useServer
    - allowLocal
    */
    $padl = new Padl\License(true, true, true, true);

    //For better security injecting a copy of $_SERVER global var
    $server_array = $_SERVER;
    $padl->setServerVars($server_array);

    $date_expire = '12/31/2011';
    list($month, $day, $year) = explode($date_expire);
    // Calculating the time offset (expire_in)
    $now       = mktime(date('H'), date('i'), date('s'), date('m'), date('d') , date('Y'));
    $dateLimit = mktime(23, 59, 59, $month, $day, $year);
    $expireIn  = $dateLimit - $now;

    // Generating a key with your server details
    $license = $padl->generate('localhost', 0, $expire_in);

    // Save the license anywhere, database, filesystem, even remotely

###  Validate

    /*
    Instance of License
    parameters used in this sample:
    - useMcrypt  = false 
    - useTime    = true
    - useServer  = false
    - allowLocal = true
    */
    $padl = new PadlLicense(true, true, true, true);

    // For better security injecting a copy of $_SERVER global var
    $server_array = $_SERVER;
    $padl->setServerVars($server_array);

    // get the license from a form, or load from database, filesystem
    $license = (... load the license ...);

    // the set key is the key validated
    $results = $padl->validate($license);
