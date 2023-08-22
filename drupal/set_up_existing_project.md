# How to Set Up an Existing Drupal Project

In this guide, you will learn how to set up an existing Drupal project in a local environment.

## Before You Begin

Set up a Drupal development environment using https://github.com/xenyo/docker-drupal.

Make sure you have access to the Git repository for the project as well as a recent database dump.

## Setting Up an Existing Drupal Project

In the examples below, replace **PROJECT_NAME** with your actual project name.

### 1. Clone the project and install dependencies

`cd` to the directory above where you would like to clone the project:

```
cd /var/www
```

Clone the repository:

```
git clone git@github.com:xenyo/PROJECT_NAME.git
```

`cd` into the project directory:

```
cd PROJECT_NAME
```

Install dependencies using Composer:

```
composer i
```

> If you installed Drush 12 or higher, you will need to use direnv to make the `drush` command available in the terminal.
>
> Create a new file named `.envrc` in the project root and insert the following text into the file:
>
> ```
> PATH_add vendor/bin
> ```
>
> Then, run this command in the terminal to allow the `.envrc` file to take effect:
>
> ```
> direnv allow
> ```
>
> See [this issue](https://github.com/drush-ops/drush-launcher/issues/105) for more details.

### 2. Install Drupal to a new database

Create a new database for the project:

```
mysqladmin -hmariadb create PROJECT_NAME
```

Then, run the Drupal installer using Drush:

```
drush si --db-url=mysql://root@mariadb:3306/PROJECT_NAME
```

### 3. Import the database dump

Copy the database dump to the project root and rename it to `database.sql`. You can do this using Docker Desktop or a SFTP client.

First, drop all tables in the database created in the previous step.

```
drush sql:drop
```

Then, run this command to import the database dump:

```
drush sql:cli < database.sql
```

> If `xenyo/dbtools` is installed in your project, you can run this command instead:
>
> ```
> composer exec dbi
> ```

### 4. Set up Apache to serve the project locally

Create `/etc/apache2/sites-available/PROJECT_NAME.conf` and insert the following text into the file:

```
<VirtualHost *:80>
  ServerName MY_PROJECT
  DocumentRoot /var/www/MY_PROJECT/web
</VirtualHost>
```

Then, enable the virtual host and restart Apache:

```
a2ensite PROJECT_NAME.conf
```

```
service apache2 restart
```

Finally, open the hosts file in your host OS (`C:\Windows\System32\drivers\etc\hosts` on Windows, `/etc/hosts` on Mac) and add the following line:

```
127.0.0.1 PROJECT_NAME
```

Now, you should be able to load the site in your browser by going to http://PROJECT_NAME:8081 (adjust port number as necessary).

## Next Steps

- [How to Enable Development Settings on a Drupal Project](enable_development_settings.md)
