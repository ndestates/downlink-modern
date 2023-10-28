# Downlink

This project runs Craft CMS 3 (latest version of as 1/17/22) and the following plugins:
- Feed Me
- Redactor
- Servd Asset & Helpers

## Local Development

The simplest way to do local development on this project is using DDEV, a Docker-based local development environment. A DDEV config directory is already included in the project but you need to have DDEV (and DOcker Desktop) already running on your machine. Here's how to do that.

### Installing the DDEV & Dependencies

1. Install [Docker Desktop](https://www.docker.com/products/docker-desktop)
2. Install DDEV using Homebrew [per these instructions](https://ddev.readthedocs.io/en/stable/#homebrew-macoslinux) _Don't have Homebrew installed? [Learn more here](https://brew.sh/)_.

### Cloning the Project Repository

_Make sure your SSH keys are added to your Github account._

1. In your preferred location (I use '~/projects`), clone the project repository.
```bash
cd ~/projects
git clone git@github.com:XXXXXXX.git
```
This will clone the project code into `~/projects/downlink-modern`. Once it successfully completes, move on to the next step.
2. Copy the `.env.example` file to a new file called `.env`. In the project root (`downlink-modern`):

```bash
cp .env-example .env
```

### Starting Up DDEV

There is already a DDEV configuration directory in the project, so you should be able to get started fairly quickly.

On the command line, navigate to the project directory, if you're not already there, and start DDEV.

```bash
cd ~/projects/downlink-modern
ddev start
```
### Composer Install

Craft uses Composer to fetch software dependencies. Every time we set up a new environment, we need to run `composer install`. Since we're using DDEV for localhosting, we'll run it right on the container using the `ddev exec` subcommand.

```bash
ddev exec composer install
```
_If you're prompted to trust `yiisoft/yii2-composer` or `craftcms/plugin-installer` answer yes to both._

Wait for this complete. When it's done, you should have a `vendor` directory in the root of the project.

### Pulling Down a Database

You need to get a copy of the database imported locally, so you can fully run the site.

In the project, there's a zip file in `db/`. Unzip that file using your computer's zip utility. You should now have a file called `starter-db.sql`

On the command line, run the following, which will import the starter database and  into your local environment:

```bash
ddev exec php craft db/restore db-seed/starter-db.sql 
```

Wait for this to complete before moving on to the next step.

### Accessing the Site in the Browser

DDEV is already setup to host the sites at the following local domain:

- https://downlink-modern.ddev.site

## Development Workflow

- Make your changes in a feature branch, using the naming pattern `feature/name-of-feature`.
- Commit all changes into that branch. 
- When complete, merge the feature branch into the `develop` branch
  ```bash
  git checkout develop
  git merge feature/name-of-feature
  ``` 
- Push `develop` to origin
    ```bash
    git push develop
    ```
  
The `develop` branch will automatically build and deploy to the staging server.