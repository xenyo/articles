# How to Set Up a Git Repository for a Drupal Project

In this guide, you will learn how to set up a Git repository for a new Drupal project and push the project code to GitHub.

## Before You Begin

Set up a new Drupal project by following [this guide](set_up_new_drupal_project.md).

## Setting Up the Git Repository

In the examples below, replace **PROJECT_NAME** with your chosen project name.

### 1. Create a `.gitignore` file

Certain folders should be excluded from being checked in to the git repository. This will make the repository a lot smaller and prevent git commands from running slowly.

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
.idea/
.vscode/
*.sql
*.sql.gz
```

### 2. Initialize the repository

`cd` to the root of the project:

```
cd /var/www/PROJECT_NAME
```

Initialize a new Git repository:

```
git init
```

Stage and commit the project files:

```
git add .
```

```
git commit -m 'Initial commit'
```

### 3. Push the repository to GitHub

Go to https://github.com/new and create a new repository.

Add the remote repository URL and push the default branch:

```
git remote add origin git@github.com:xenyo/PROJECT_NAME.git
```

```
git push -u origin main
```
