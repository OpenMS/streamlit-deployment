# OpenMS streamlit app deployment

Multiple streamlit apps based on the [OpenMS streamlit template](https://github.com/OpenMS/streamlit-template/) can be deployed together using docker compose.

## Features

- deploy all OpenMS apps at once
- user data (in workspaces) is stored in persistent docker volumes for each app

## Requirements
- Docker Compose

## Deployment (e.g., needed after one app changed)

**1. Make sure submodules are up-to-data.**

`git submodule init`

`git submodule update`

**2. Specify GitHub token (to download Windows executables).**

> This is **important**! Omitting this step while result in all apps not having the option to download executables any more.

Create a temporary `.env` file with your Github token. It should contain only one line:

`GITHUB_TOKEN=<your-github-token>`

**3. Run docker-compose.**

`docker compose build`

> Make sure to remove the `.env` file with your Github token after successfull build
> Optionally use the `--no-cache` flag to prevent caching

> Optionally use the `--no-cache` flag to prevent caching

## Add new app

This will add your app as a submodule to the streamlit deployment repository. 

**1. Fork and clone the [OpenMS streamlit deployment](https://github.com/OpenMS/streamlit-deployment) repository locally.**

**2. Add your app as submodule. Make sure the app name is not used already.**

`git submodule add <url-to-git-repository> <name-of-app>`

**3. Initialize and update submodules.**

`git submodule init`

`git submodule update`

**4. Add your app to `docker-compose.yml` file as a new service.**

Copy the last service as a template.

Check and update the following entries:

- name of the service 
    - the name of the submodule
- build context
    - the relative path to the submodule
- build dockerfile
    - the correct Dockerfile
- image
    - name of the docker image (typically the service name with underscores)
- ports
    - chose an incremental host port number from the last service pointing to the streamlit port in docker container (8501)
- volumes
    - update the names of the workspace directories, user data is stored outside of the docker container in a docker volume 
- command
    - update command with your main streamlit file

**6. Test everything works locally.**

Run docker-compose to launch all services.

` docker compose up -d`

- there should be no errors building all services
- make sure all apps are accessible via their port from localhost
- test functionality of your app

**7. Make a pull request with your changes to OpenMS/streamlit-deployment main branch.**
