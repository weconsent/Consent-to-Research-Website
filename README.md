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

If successful, you can log in to your default Aiki installation.

Finally, load the custom CtR tables into your database, based on the database you created for aiki:

    cd /srv/www/weconsent.us/public/aikiframework-www/assets/extensions/ctr
    mysql -u USERNAME -p DATABASE_NAME < CreateTables-sites_CtR.sql
    mysql -u USERNAME -p DATABASE_NAME < InsertVariable-sites_CtR.sql
    mysql -u USERNAME -p DATABASE_NAME < InsertWidgets-sites_CtR.sql
    
Your copy of CtR is now installed at http://weconsent.us
    
