---
layout: page
title: Developer Guide
---

# Developer Guide

## Installation for Developer

* optional: fork the repository
* clone the repository into your web folder (e.g. `/var/www/ontowiki`)
* enable Apaches rewrite  module (e.g. `a2enmod rewrite`)
* run `make install` to download Zend, init git submodules as well as to create log and cache dir
* copy `config.ini-dist` to `config.ini` and modify it according to your store
* open your browser, go to your ontowiki URL, login as `Admin` without pass and change the password
* make sure you create your own feature branch
* maybe turn off the query and object cache in you `config.ini`:
  * `cache.query.enable = false`
  * `cache.enable = false`

## Set a Test Environment

###  Ready ... 

**Do not** use a XAMPP environment for testing. There a few things which makes problems. So use **native** OS packages for Apache2, MySQL, PHP5 etc. Execute the following commands over your terminal. 

For **Ubuntu** 10.04 (Lucid Lynx):

  * **Apache2**
    sudo apt-get install apache2 
  For eLDS we need **mod_rewrite**

    sudo a2enmod rewrite
  Give you full write access to webfolder

    sudo chmod 777 /var/www

  * **MySQL**
  If you would use Virtuoso or whatever ignore this part. 

    sudo apt-get install mysql-server
  for more information how to set up and configure a MySQL server please take a look at [[http://wiki.ubuntuusers.de/MySQL]]

  * **PHPMyAdmin**
  Not neccessary but useful for administrate your MySQL databases. If you would use Virtuoso or whatever ignore this part.

    sudo apt-get install phpmyadmin
  * **PHP5**, **PHPUnit**, PEAR

    sudo apt-get install php5 php5-cli php-pear php5-curl php5-mysql php5-odbc phpunit


###  .. steady, ... 

Now start neccessary services

  * Apache2

    sudo service apache2 start

  * MySQL

   sudo service mysql start

Now put a copy of eLDS into */var/www/myow*! ( [[InstallFromGit]] )

Currently the testability of eLDS is getting refactored so change your current branch 


   cd /var/www/myow && hg update OntoWiki-RefactoringTestability

If you type 


   hg branch

you should be get


   hg branch 
   OntoWiki-RefactoringTestability

Be sure that your **Zend** version is >= **1.9.5**. If you dont know the version execute


    cd /var/www/myow && make zend

###  ... **Go!** 

#####  Tests folder content 

Please use your terminal for navigating and doing things because of PHPUnit has no GUI and is usable only via terminal. Get folder content


    cd /var/www/myow/application/tests && ls

You should get something like:

    controllers  DropErrorMails.php  OntoWiki  Selenium  test_base.php  TestSuite.php

Now take a test

    phpunit TestSuite

You should get something like:

    PHPUnit 3.4.5 by Sebastian Bergmann.
    
    .........
    
    Time: 2 seconds, Memory: 16.25Mb
    OK (9 tests, 27 assertions)
    
Driven eLDS developers write every time tests for their new fancy stuff so this output can be changed in the future! But there should be _no_ errors by PHPUnit.

For an **easier way** to execute PHPUnit go back to OntoWiki root folder

    cd /var/www/myow

and execute 

    make test

It executes _phpunit TestSuite_ too.

###  Curiosities 

#####  Percent symbol 
If phpunit stop testing and breaks with an % like

    PHPUnit 3.4.5 by Sebastian Bergmann.
    ..........%    

in your tested code contains an **exit** call, which is reached (and the % indicates that your terminal complains about a missing newline). Use **return;** instead!