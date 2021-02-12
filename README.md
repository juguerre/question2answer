# question2answer PaaS

Project enabling question2answer OSS producto to run on Paas framework

## Defining variables with getenv

See: [PHP](https://confluence.cloud.lacaixa.es/confluence/display/grupoPlataformaArquitecturaCloud/PHP)

File: [qa-config.php](public/qa-config.php)

```php
define('QA_MYSQL_USERNAME', getenv("Q2ACOM_Q2ACOM_MYSQL_USER_NAME"));
define('QA_MYSQL_PASSWORD', getenv("Q2ACOM_Q2ACOM_MYSQL_USER_PASSWORD"));
$mysqlURL= getenv('Q2ACOM_Q2ACOM_MYSQL_CONNECTION_STRING');
# Prepare hostname, port and database variables from connection string
$hostname = strtok($mysqlURL, ":");
$port_db = strtok(":");
$port = strtok($port_db,"/");
$database = strtok("/");

define('QA_MYSQL_HOSTNAME', $hostname);
define('QA_MYSQL_PORT', $port);
define('QA_MYSQL_DATABASE', $database);
```

## Dependences

PaaS PHP provider seems to have all dependences. 
> See pdf sample of standar extensions installed: [pdf](https://confluence.cloud.lacaixa.es/confluence/download/attachments/53971372/phpinfo56.pdf?version=1&modificationDate=1603895044000&api=v2)

```shell
docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
docker-php-ext-install ldap && \
docker-php-ext-install mysqli mbstring && \
docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ &&\
docker-php-ext-install gd calendar
```

## Product standard install

The instructions below are for installing Question2Answer where it manages user accounts and logins for you. If you would like Question2Answer to integrate with your existing user database and account system, see the instructions for single sign-on installation. From version 1.4, Question2Answer also offers easy integration with a WordPress 3.x site and user database.

1. Download the latest version of Question2Answer to your computer or web server (also available on GitHub).
2. Unzip the download using a tool such as WinZip (or unzip in the Unix shell). Relase Zip has the same structure that git repository.
3. If you want to run a non-English site, check if the appropriate language file is available. If so, download and install it in the qa-lang folder. If not, it’s simple to translate Question2Answer for yourself.
4. Create a MySQL database, and a MySQL user with full permissions for that database. If you’re interested, the privileges actually needed are: CREATE, ALTER, DELETE, INSERT, SELECT, UPDATE, LOCK TABLES
5. Note down the MySQL details: username, password, database name and server host name. If MySQL is running on the same server as your website, the server host name is likely to be 127.0.0.1 or localhost.
6. Find qa-config-example.php and .htaccess-example in the unzipped question2answer folder, and rename them to qa-config.php and .htaccess, respectively.
7. Open qa-config.php in your text editor, insert the MySQL details at the top, and save the file. Do not use a word processor such as Microsoft Word for this, but rather Notepad or another appropriate text editing program.
8. Place all the Question2Answer files in the appropriate location on your web server:
To serve Question2Answer at the root of a domain (e.g. http://www.mysite.com/), move or upload all the contents of the unzipped question2answer folder into the root directory for that domain on your web server.
To serve Question2Answer in a subdirectory of a site (e.g. http://www.mysite.com/qa/), create the subdirectory inside the root directory for the site, then move or upload all the contents of the unzipped question2answer folder into this subdirectory.
9. Open the appropriate web page for Question2Answer in your web browser, for example:
   - If you installed Question2Answer at the root of a domain, http://www.mysite.com/
   - If you installed Question2Answer in a subdirectory, http://www.mysite.com/qa/
10. Follow the on-screen instructions to set up your database and administrator account. That’s it!

see: <https://docs.question2answer.org/install/>