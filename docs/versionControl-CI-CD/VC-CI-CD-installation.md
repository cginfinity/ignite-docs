---
id: VC-CI-CD-installation
title: Installation
sidebar_label: Installation
layout: VC-CI-CD-installation
---

## Setting up the Local Environment and Workspace

This guide explains how to set up your environment for Ignite Project development using the Docker & Postgres. It includes information about prerequisites, creating an initial workspace and starter app, and running that app locally to verify your setup.

### Prerequisite

To use the Ignite Project, you should be familiar with the following:
1.  <a href="https://docs.docker.com/get-started/overview/" style="color:blue" taget="_blank">Docker</a>
2.  <a href="https://www.postgresql.org/docs/13/index.html" style="color:blue" taget="_blank">PostgreSQL</a> 
3.  <a href="https://try.github.io/" style="color:blue" taget="_blank">Git</a>

Knowledge of <a href="https://docs.docker.com/compose/" style="color:blue" taget="_blank">**Docker Compose**</a> is helpful, but not required.
To install Ignite Project on your local system, you need the following:

- **Docker**

    Ignite requires a latest version of Docker Desktop.
For more information on installing Docker Desktop, see <a href="https://www.docker.com/products/" style="color:blue" taget="_blank">docker-desktop</a>. 

    If you are unsure what version of Docker Desktop runs on your system, run docker -v in a terminal window.

- **Postgres**

     Ignite requires Postgres Database to start application development.
You can connect to existing Postgres Database or start a new Postgres instance.
For more information on installing Postgres Database on Docker Desktop, see <a href="https://hub.docker.com/_/postgres" style="color:blue" taget="_blank">here</a>.

### Create a workspace and initial application

You develop apps in the context of an <a href="https://dashboard.cgignite.io/apps" style="color:blue" taget="_blank">Ignite App</a>. 

To create a new, Ignite App: 
1.	Navigate to <a href="https://dashboard.cgignite.io/apps" style="color:blue" taget="_blank">Ignite App</a> and create a new app and provide the name, such as my-app

    ![](../assets/VersionControl-CI-CD/CreateNewApp.png)

2.	The **Create App** action, will navigate to registration page which will provide information to start & register Ignite container.

    ![](../assets/VersionControl-CI-CD/RunTimeRegistration.png)

### Run the application

The Ignite Container includes a server, so that you can build and serve your app locally.

1.	Open Terminal, Create new workspace folder, such as my-app.
2.	Run the following command:
    ```
    cd my-app 
    ```
3.	Create a file **docker-compose.yml**. see, Appendix “Docker Compose” for reference.
**cybergroupignite/runtime:rc-dev-1.0.24-98aff1b** is our latest docker image, 
following environment variable are required to start local development.

    ```
        IGNITE_EDITOR_API_SECRET: “<your editor key>” 
        DATABASE_URL: “<your database url>”
        DB_SSL_OPTION: “true” or "false” based on your Postgres Database installation 
        START_MODE: "PROJECT" required for git based application development
    ```

4.	Run the following command:

    ```
    docker-compose up
    ```

The **docker-compose up** command launches the server, watch the logs, wait for container to start.

When application is ready to accept the request, open **http://localhost:1881/**.

If your installation and setup was successful, you should see a page similar to the following

![](../assets/VersionControl-CI-CD/Ignite-Runtime.png)

### Runtime Registration

To start the application development, register your application on registration page. 

![](../assets/VersionControl-CI-CD/RunTimeRegistration.png)

1.	Select Development & Enter **http://localhost:1881/** on Ignite Runtime URL textbox

![](../assets/VersionControl-CI-CD/SelectRuntimeEnvironment.png)

2.	Click on **Test Connection** button to test and complete the registration process

3.	On Successful connection browser will be redirected to editor.

If your environment variable is correct, you should see a page similar to the following,

![](../assets/VersionControl-CI-CD/CreateProjectPage.png)

### Creating your first project

When you open the **Editor**, you’ll be greeted by a welcome screen that invites you to create your first project using your existing flow files.

It will take you through the following steps:

1.	Setup your version control client

    Ignite uses the open source tool Git for version control. It tracks changes to your project files and lets you push them to remote repositories.

    When you commit a set of changes, Git records who made the changes with a username and email address. The Username can be anything you want - it does not need to be your real name.

    You can change these settings at any time via the main **settings** dialog.

2.	Create your project

    The next step lets you name your project and given it a description.

3.	Create your project files

    Ignite will automatically migrate your existing flow files into your project. You can choose to rename them here if you want.

4.	Setup encryption of your credentials file

    As you may choose to share your project on public sites such as GitHub, it is strongly recommended that you encrypt your credentials file.
To encrypt it, you need to choose a key that will be used to secure the file. This key is not stored within the project. If someone else clones your project, you will need to provide them the key to decrypt the credentials file. Otherwise they will need to edit the flow to provide their own credentials.

### Working with projects

Once you have created your project, you can continue to use the editor just as you always have. There are some new parts of the editor that have been added to work with your project.

#### Accessing Project Settings

The Info sidebar now shows what project you are working on at the top. Next to the project name is a button that opens up the Project Settings dialog.

![](../assets/VersionControl-CI-CD/ProjectSettingDialogue.png)

You can also access this from the Projects -> Project Settings option in the main menu.

The dialog has three tabs:

**Project** lets you edit the project’s README.md file.

**Dependencies** - manage the list of node modules your project depends on

**Settings** - manage the project settings, including the git remotes

**Project Dependencies**

Each project has its own package.json file that includes a list of node modules the project depends on. The editor tracks what nodes you are using in a flow and helps you to keep that list of dependencies up to date.

![](../assets/VersionControl-CI-CD/ProjectInformation.png)

In the screenshot above, the current project has three modules listed in its package.json file, each in a different state:

-	**node-red-node-mysql** is not currently installed
-	**node-red-node-random** is used by the current flow
-	**node-red-node-rbe** is listed, but is unused by the current flow
 
Finally, **node-red-node-smooth** provides a node that is used by the current flow, but that module is not listed as a dependency.

Keeping the dependency list up to date is important if you want to share the project with others - as it will help users to install the necessary modules.

**Project Settings**

The project settings tab lets you manage your flow files, the encryption configuration of your credentials and configure your local git branches and remote repositories.

**Version Control**

A new history tab has been added to the sidebar. This is where you manage the version control of your project. The tab has two sections:

- **Local Changes** - shows project files that have changed, allowing you to stage and commit them.

- **Commit History** - a list of all commits in the repository, with tools to push commits to remote repositories.

##### Local Changes

Whenever you change a project file, such as by deploying a new flow configuration, it will be listed in the ‘Local files’ section. You can click on the file name to see a diff of what has changed. When you hover over the file, you’ll see a + button - clicking that will stage the file - moving it down to the ‘Changes to commit’ list.

When you have staged the files you want to commit, click the commit button, enter a message and confirm.
    
![](../assets/VersionControl-CI-CD/LocalChanges.png)

##### Commit History

The Commit History section lists all of the commits in the current branch of the repository. When you create a project, Editor automatically commits the initial set of default files for the project.

At the top of the list is the ‘Branch’ button. That allows you to checkout/create branches within the repository.

If your repository has a remote repository configured, there is also a button that shows how many commits ahead and/or behind your local repository is compared with the remote. It allows you to pick the remote/branch to track, and push/pull your changes to the remote.

![](../assets/VersionControl-CI-CD/CommitHistory.png)

This is one area that the editor tries to simplify the user experience, and doesn’t expose all of the various options git provides. This is an area we welcome feedback on. For example, it does not provide options to rebase your local commits, or force push your changes to the remote. You can still do those things by falling back to the command line.

##### Creating new projects

After you have created your first project by migrating your existing flow files you can create additional projects.

Selecting Projects -> New from the menu opens the Projects dialog.

This provides three options:

-   open an existing project
-   create a new project
-   clone a project repository

**Open an existing project**

Runtime only runs one project at any time. By opening another project you change what flows are running. 

The ‘open project’ view also allows you to delete projects by hovering over them in the list and clicking the delete button. You cannot delete the active project.

**Create a new project**

This lets you create a new project. It provides the same options as the ‘create your first project’ set of screens, but collapsed into one. 

**Clone a project repository**

This lets you clone an existing remote repository. You can use either an http(s) or git/ssh url for the repository. If the repository requires authentication you must provide it here.

Note: for http urls, do not include your username and/or password in the url itself. You can should provide those separately when prompted.

## Build

The Ignite Application runs on docker container, you can build image from project repository.

1.  Open Terminal

2.  Clone your git repository

3.  Create a Docker file. See, Appendix "Build” for reference or https://github.com/Cybergroup-Research/example-project/blob/main/Dockerfile

4.  Run the following command:

    ```
    docker build . -t your-image-name
    ```

Docker image can be pushed to public/private repository like https://hub.docker.com/ 

## Deployment

To start application, follow following command.

1.  Open Terminal

2.  Run the following command:

    ```
    docker run [OPTIONS] IMAGE [COMMAND] [ARG..]
    ```

Environment variable required to start the application are:

```
IGNITE_EDITOR_API_SECRET: "<Your Ignite Secret key>"

DATABASE_URL: "<Database URL>"

START_MODE: "BUILD"
```

## Appendix

### Example

Checkout example repository to build image using git action & deploy on Heroku, see https://github.com/Cybergroup-Research/example-project

#### Docker Compose

##### Application Development

```
version: "3.9"
```

```
  services:

    web:

      image: cybergroupignite/runtime:rc-dev-1.0.24-98aff1b

      ports:

        - "1881:1881"

      volumes: 

        - ./data:/root/.node-red

      environment:

        IGNITE_EDITOR_API_SECRET: "<Your Ignite Secret key>"

        DATABASE_URL: "<Database URL>"

        START_MODE: "PROJECT"
```

#### Docker Compose

##### Application Development

```
FROM cybergroupignite/runtime:rc-dev-1.0.24-fdcaeba
```

```
  WORKDIR /usr/src/nodered

  COPY . ./build

  RUN npm run compile
```