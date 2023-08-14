# How to Create a New Drupal Project

In this guide, you will learn how to set up a new Drupal project, initialize a Git repository and create a virtual host to serve the project locally.

## Before You Begin

Set up a development environment using https://github.com/xenyo/docker-drupal.

If you prefer to use a different environment, make sure it includes Apache, MySQL, PHP, Composer and Git.

## Creating a Drupal Project

Choose an appropriate name for your project. In the code examples below, replace PROJECT_NAME with your chosen project name.

### 1. `cd` to the directory above where you would like to create the project.

```
cd /var/www
```

### 2. Download Drupal using Composer.

To download the latest stable version:

```
composer create-project drupal/recommended-project PROJECT_NAME
```

To download a specific version, for example Drupal 9:

```
composer create-project drupal/recommended-project:^9 PROJECT_NAME
```

After Composer finishes, `cd` into the project directory:

```
cd PROJECT_NAME
```

### 3. Create a new `.gitignore` file.

Create a new file named `.gitignore` in the project root and insert the following text into the file:

```
/vendor/
/web/core/
/web/modules/contrib/
/web/themes/contrib/
/web/profiles/contrib/
/web/libraries/
/web/sites/*/settings.php
/web/sites/*/settings.local.php
/web/sites/*/files/
node_modules/
/.idea/
/.vscode/
*.sql
*.sql.gz
```

### 4. Set up a new Git repository.

Initialize a new Git repository and commit everything:

```
git init
```

```
git add .
```

```
git commit -m 'Initial commit'
```

Then, create a new repository on GitHub and push your code:

```
git remote add origin git@github.com:xenyo/PROJECT_NAME.git
```

```
git push
```

### 5. Create a new virtual host to map a domain name to your project.

Create a new virtual host configuration file:

```
vim /etc/apache2/sites-available/PROJECT_NAME.conf
```

Insert the following text into the file:

```
<VirtualHost *:80>
  ServerName MY_PROJECT
  DocumentRoot /var/www/MY_PROJECT
</VirtualHost>
```

Then, add the following line to your hosts file (`C:\Windows\System32\drivers\etc\hosts` on Windows, `/etc/hosts` on Mac)

```
127.0.0.1 MY_PROJECT
```
