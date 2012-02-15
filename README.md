Consent to Research Website
===========================

http://weconsent.us/

This is the respository for the Consent to Research Alpha Testing Website. You can read more about the alpha testing process here: http://weconsent.us/post/12496478564/alpha-testing-launched

Requirements
------------

The Consent to Research website (hereafter CtR) runs on Aiki Framework. You can learn more about Aiki Framewok here: http://aikiframework.org/

See: http://www.aikiframework.org/wiki/Aiki_Requisites

CtR is run on Aiki Framework 0.8.18.843.

Installation
------------

For background see: http://www.aikiframework.org/wiki/Installing_Aiki

In this example we will install our website at /srv/www/weconsent.us/public/

    cd /srv/www/weconsent.us/public/
    git clone git://github.com/weconsent/Consent-to-Research-Website.git .
    git submodule init
    git submodule update
 
Next, define your Virtual Host in Apache:

    <VirtualHost *:8080>
        ServerAdmin info@weconsent.us
        ServerName weconsent.us
        ServerAlias www.weconsent.us
        DocumentRoot /srv/www/weconsent.us/public/aikiframework-www
        
        <Directory /srv/www/weconsent.us/public/aikiframework-www>
            AllowOverride All
            RedirectMatch 403 /\.(svn|git|bzr|am|in?).*$
        </Directory>
        ErrorLog /srv/www/weconsent.us/logs/error.log
        CustomLog /srv/www/weconsent.us/logs/access.log combined
    </VirtualHost>
    
Restart Apache.

Create a database for CtR: http://www.aikiframework.org/wiki/Create_SQL_User

Visit the Aiki Installer in your web browser: http://weconsent.us

Enter the Database Settings from the database you created.

If successful, you can log in to your default Aiki installation. Be sure to keep a record of your admin login credentials.

Finally, load the custom CtR tables into your database, based on the database you created for aiki:

    cd /srv/www/weconsent.us/public/aikiframework-www/assets/extensions/ctr
    mysql -u USERNAME -p DATABASE_NAME < CreateTables-sites_CtR.sql
    mysql -u USERNAME -p DATABASE_NAME < InsertVariable-sites_CtR.sql
    mysql --execute="delete from aiki_widgets where app_id = '0'" -u USERNAME -p DATABASE_NAME
    mysql -u USERNAME -p DATABASE_NAME < InsertWidgets-sites_CtR.sql
    mysql -u USERNAME -p DATABASE_NAME < InsertForms-sites_CtR.sql
    
Your copy of CtR is now installed at http://weconsent.us

Instructions
------------

To make any functional changes to the site, sign in using your admin login credentials at: http://weconsent.us/login. This will present you with the Aiki Framework Admin panel where you can develop the website.

To create and assign alpha codes, or edit the consent form, sign in using your admin login credentials at: http://weconsent.us/sage. This will present you with a dashboard with two options: Check and assign alpha codes, and Edit the Consent Form.

### Check and Assign Alpha codes

Sign in using your admin credentials, visit the main page of the site, and click on "Check and assign alpha codes."

Under Tools, click "Create an Alpha Code". This will create a new table of Alpha Codes listing the User ID, the Alpha Code with link, and the Last Login. Each time you click the button, a single alpha code will be generated.

To assign an Alpha code, copy the link in the Alpha Code column, and send that link to your alpha tester. Once the alpha tester has started the testing procedure, his or her last visit to the site will be recorded in the Last Login column.

Once an alpha tester has sucessfully completed the testing process, his or her alpha code will disappear from the list of Alpha Codes. You will see an Alpha Testers column appear on this page, recording the User ID, Name and Email address of the successful alpha tester.
