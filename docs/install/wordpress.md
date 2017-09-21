# WordPress Installation Guide for CiviCRM

!!! note "Install process for CiviCRM 4.5 on WordPress"

    **IMPORTANT: CiviCRM 4.7 requires WordPress 3.4.x or higher. It is recommended to use a current version of WordPress. The current release (at 19 February 2017) is WP 4.7.2**
     This page provides instructions for installing CiviCRM as a plugin for WordPress. This is the recommended installation method.

    **If you are upgrading from CiviCRM v4.2, v4.3, 4.5, 4.6 or a prior version of v4.7 - [use these instructions](https://wiki.civicrm.org/confluence/display/CRMDOC/Upgrade+WordPress+Sites+to+4.7)**

    **Before beginning the install process, please verify that your server meets all the requirements for CiviCRM 4.5.**

    * **WordPress 3.4.x or newer** : CiviCRM 4.5 is built to run under WordPress 3.4.x or higher and **is not compatible with earlier WordPress versions**.
    * **PHP 5.3.3+** (more info...).
    * **MySQL 5.1.x or higher with INNODB support** : CiviCRM is compatible with the current [generally available MySQL release](http://dev.mysql.com/downloads/mysql). Trigger permission is required. SUPER privileges are required in MySQL 5.1 if binary logging is enabled. See the [CiviCRM MySQL Permission Requirements](https://wiki.civicrm.org/confluence/display/CRMDOC/CiviCRM+MySQL+Permission+Requirements) page.
    * **PCRE with Unicode properties support** ([more info](http://forum.civicrm.org/index.php/topic,9316.0.html "CentOS, CiviCRM and PCRE Unicode Properties")).
    * MAMP XCache in-compatibility* - Several people have reported "white screen of death" trying to run CiviCRM 4 with MAMP's XCache enabled (check MAMP > Preferences > PHP > Cache).
    * eAccelerator - Several people have reported problems with this performance optimiser ([http://eaccelerator.net](http://eAccelerator)) - "white screen of death" and "snippet type is unrecognised".

## Server Requirements

### Plugin Issues

Because of the huge number and ever-changing nature of community contributed Wordpress plugins, CiviCRM cannot guarantee compatibility with contributed plugins. A list of know incompatibilities can be found at [WordPress plugins and themes incompatible with CiviCRM](https://wiki.civicrm.org/confluence/display/CRMDOC/WordPress+plugins+and+themes+incompatible+with+CiviCRM).

## WordPress Installed

Before installing CiviCRM you need to have a working site with WordPress 3.4.x. If you do not have the required version of WordPress installed, refer to:

* [WordPress Installation Guide](http://codex.wordpress.org/Installing_WordPress)

!!! note "Path for WordPress"
     The rest of these instructions assume that you have WordPress installed in _/var/www/wordpress_. Adjust paths as needed. |

    ## 3. Download and Un-zip CiviCRM Code

    All CiviCRM code and packages used by CiviCRM (such as PEAR libraries) are included in the compressed CiviCRM distribution files ('tarballs'). Follow these steps to download and install the codebase:

    * Download the appropriate tarball file from [here](https://civicrm.org/download) with your browser. Tarball file-names include the CiviCRM version. For example, **civicrm-4.7.x-wordpress.zip.**

    * Copy or ftp the tarball file to your WordPress installation's _/wp-content/plugins_ directory. You may have to change the "File Permissions" setting of _/wp-content/plugins/civicrm_ directory to allow for "Write" Access. Just remember to change it back to default when done.
    * You can upload the zip file that was downloaded via your WordPress admin panel at
    ```
    wp-admin/plugin-install.php
    ```

    * **Create the <wordpress path>/wp-content/plugins/files/ directory and ensure it is writable.** CiviCRM for versions 4.6 and prioruses this directory for temporary and uploaded files.

    !!! information "Downloading Directly to Your Server with wget"

    If you have command-line access, you may prefer to download the tarball file directly to your server using wget:

    ```
    // Move into WordPress's plugin directory
    cd /var/www/wordpress/wp-content/plugins

    // wget the file (modify this line to use the current tarball file name for the version you want)
    wget https://download.civicrm.org/civicrm-4.7.xx-wordpress.zip
    ```


* Extract (aka: unzip, unpack) the codebase into the wordpress/wp-content/plugins directory.

```
// Move to the wordpress/wp-content/plugins directory (if not already there)
cd /var/www/wordpress/wp-content/plugins

// Un-zip the file (modify this line with the actual downloaded filename)
unzip civicrm_download_file.zip
```

* You should now have a /var/www/wordpress/wp-content/plugins/civicrm directory containing civicrm.php, README.txt and another civicrm directory (which in turn contains bin, CRM, sql, templates, etc.).

## If Using Localization, Download and Un-tar the Localization Files

Follow these steps to download and install the files that contain strings for languages other than American English:

* Download the appropriate tarball file from [here](http://sourceforge.net/projects/civicrm/files/civicrm-stable/4.4.5/) with your browser. Tarball file-names include the CiviCRM version, and l10n (that's lower case ell-ten-en). For example, **civicrm-4.5.x-l10n.tar.gz.**.

* Copy or ftp the tarball file to your WordPress installation's _/wp-content/plugins_ directory. You may have to change the "File Permissions" setting of _/wp-content/plugins_ directory to allow for "Write" Access. Just remember to change it back to default when done.

!!! note "Downloading Directly to Your Server with wget"

    If you have command-line access, you may prefer to download the tarball file directly to your server using wget:

    ```
    // Move into WordPress's modules directory and then into the civicrm subdirectory
    cd /var/www/wordpress/wp-content/plugins/civicrm

    // wget the file (modify this line to use the current tarball file name for the version you want)
    wget http://sourceforge.net/projects/civicrm/files/civicrm-latest/4.5.x/civicrm-4.5.x-l10n.tar.gz
    ```


* Un-tar (unpack) the language files into the wordpress/wp-content/plugins directory.

```
// Move to the wordpress/wp-content/plugins/civicrm directory (if not already there)
cd /var/www/wordpress/wp-content/plugins/civicrm

// Un-tar the file (modify this line with the actual downloaded filename)
tar -zxvf civicrm_download_file.tgz
```

* You should now have a wordpress/wp-content/plugins/civicrm/civicrm/l10n directory with a number of directories below it (including bin, CRM, sql and templates).

## Enable CiviCRM plugin and run installer

The installer will verify that you've downloaded the correct version of CiviCRM, and will check your server environment to make sure it meets CiviCRM requirements. It will then create and populate a database for CiviCRM as well as create your CiviCRM settings file (civicrm.settings.php).

* Login to your WordPress site with Administrator level permissions.
* Go to plugins page: http://<your_wordpress_home>/wp-admin/plugins.php.
* Click the 'Activate' link to activate the CiviCRM plugin.
* Then go to Settings > CiviCRM Installer: http://<your_wordpress_home>/wp-admin/options-general.php?page=civicrm-install
    * In version 4.7 you will see a link on the wp-admin page to the Installer screen

* You should see the **CiviCRM Installer** screen.

    * Initially, you will see a red bar with the message "These database details don't appear to be correct." This is expected as you haven't entered your database settings yet.
    * If you see other errors, check the **Requirements** details at the bottom of the page for more information. You will need to correct any issues before continuing.
* Fill in the CiviCRM Database Settings.

!!! tip "Where Should I Store CiviCRM Data?"
 CiviCRM may be configured to use your existing WordPress database, or a separate (new) database. Using a separate database is generally preferred - as it makes backups and upgrades easier. The installer will create a new database for CiviCRM automatically if you enter a database name that doesn't already exist on your database server AND the database user you enter has permission to create databases. In case the installer does not automatically create a new database, simply create a new one following the same process as creating a new database for WordPress. |

* Fill in the WordPress Database Settings for your existing WordPress database (as noted in step 2 above). In version 4.7.x CiviCRM will fill in the WP database settings, you can change these if you want to use a separate database.

!!! tip "Loading Sample Data"
 The Installer includes an option to load a set of sample contact, group, and relationship data by default. Sample data can provide a useful head-start in learning to use CiviCRM. However, if you do NOT want the sample data to be loaded, just uncheck **Load sample data** under **Other Settings**. |

* Select the appropriate language for the base installation. You will be able to add other languages after the installation for multi-lingual sites.
* Click the **Check Requirements and Install CiviCRM** button.

    * The installer will configure your databases, create the settings file and will redirect to success message.
    * If you still see a red bar with the message "These database details don't appear to be correct." - check the Database Details section below your settings for specific errors and problems. Once you correct these problems, click "Recheck requirements" to verify your settings before continuing.
    * If you are on a Windows machine and get the message "The user account used by your web-server needs to be granted write access to the following directory in order to configure the CiviCRM settings file:
 C:<wordpress path>/wp-content/plugins/civicrm/" even after changing directory permission in Explorer, see [http://forum.civicrm.org/index.php/topic,5056.msg23720.html#msg23720](http://forum.civicrm.org/index.php/topic,5056.msg23720.html#msg23720) for instructions how to change the permissions using CMD.
    * Once you see the green "You're ready to install!" message - you can click **Check Requirements and Install CiviCRM**

## Locate and Backup the CiviCRM settings file

After installation, a configuration file will have been created by CiviCRM at: <wordpress>/wp-content/uploads/civicrm/civicrm.settings.php

It is critical you make a copy of this file and save as a backup in a safe location. This file contains passwords and other critical information, take precautions to secure the copy from prying eyes.

Should an upgrade fail, you will need this backup copy to restore your site.

## Create CiviCRM Contacts for Existing WordPress Users

Once installed, CiviCRM keeps your WordPress Users synchronized with corresponding CiviCRM contact records. The 'rule' is that there will be a matched contact record for each WordPress user record. Conversely, only contacts who are authenticated users of your site will have corresponding WordPress user records.

When CiviCRM is installed on top of an existing WordPress site, a special CiviCRM Administrative feature allows you to automatically create CiviCRM contacts for all existing WordPress users:

* Login to your WordPress site with an administrator-level login
* Click the **CiviCRM** link in the main navigation block
* (If your WordPress site makes use of the db_prefix setting (in settings.php - cf. Step 2, above), in de top bar click **Administer » System Settings » CMS Database Integration** , and update the box for the WordPress Users Table Name so that it includes the prefix.)
* Click **Administer** in the menu bar
* Click **Users and Permissions** from the drop-down menu, then select **Synchronize Users to Contacts**

## Review the Configuration Checklist

The **Configuration Checklist** provides a convenient way to work through the settings that need to be reviewed and configured for a new site. You can link to this checklist from the installation success page AND you can visit it at any time from **Administer** » **Administration Console** » **Configuration Checklist**.

## Test-drive CiviCRM

There should now be a **CiviCRM** link in your WordPress menu. Click that link and the CiviCRM Menu, Shortcuts, Search and New Individual Blocks should appear.

You can now explore CiviCRM end-user features and begin configuring CiviCRM for your site/organization needs. Refer to the [Administrator Guide](https://wiki.civicrm.org/confluence/display/CRMDOC/User+guide+supplement) for information on configuration tasks and options. Tips for creating CiviCRM Profiles (forms), custom data fields and programming custom data manipulation are included in the [**Drupal installation and configuration example**](https://wiki.civicrm.org/confluence/display/CRMDOC/Drupal+installation+and+configuration+example) document.

## Upgrade CiviCRM

When a new, stable version of CiviCRM is released it is recommended you upgrade if the release contains security patches, bug fixes or new features you desire.

1. Backup your existing <wordpress>/wp-content/plugins/civicrm directory by creating an archive or FTPing it to your local computer
  1. Backup your existing database through Control Panel or PHPMyAdmin
  1. Download the latest CiviCRM .zip package from the download link at CiviCRM.org
  1. Upload the .zip file to: <wordpress>/wp-content/plugins
  1. Use your Control Panel to "extract" or "unzip" the file careful to:
 a. make sure you have a backup of your civicrm.settings.php file (see above at heading #6)
 b. you overwrite existing civicrm directory during the extraction/unzip
 c. do NOT create an additional subdirectory for the extraction
  1. Delete all files in <wordpress>/wp-content/plugins/files/civicrm/templates_c/ and clear browser cache
  1. Run the Upgrade script at:[http://www.YOURSITE.org/wp-admin/admin.php?page=CiviCRM&q=civicrm/upgrade&reset=1](http://www.YOURSITE.org/wp-admin/admin.php?page=CiviCRM&q=civicrm/upgrade&reset=1)

## Trouble-shooting Resources

Review the **[Installation and Configuration Troubleshooting](https://wiki.civicrm.org/confluence/display/CRMDOC/Installation+and+Configuration+Troubleshooting)** section of our wiki for help with problems you may encounter during the installation.

You can often find solutions to your issue by searching the **[installation support section of the community forum](http://forum.civicrm.org/index.php/board,64.0.html)** and you can check out the **Installation section of our FAQs**.

If you don't find an answer to your problem in those places, the next step is to **[post a support request on the forum](http://forum.civicrm.org/index.php/board,64.0.html)**.