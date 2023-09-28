## Requirements
- Docker Compose

## Start / update containers
- to include Windows executables, create a `.env` file and write a variable with valid Github token such as `GITHUB_TOKEN=yourgithubtoken
- run docker compose `docker-compose up --build -d`

### Initial deployment
- initialize and update submodules

`git submodule init`

`git submodule update`

- start containers

### Add new App
- add submodule of your app

`git submodule add url-to-git-repository name-of-app`

- uüdate containers

### Update your App

- update submodules

`cd your-app-submodule-directory`

`git pull origin main`

`cd ..`

`git status`

`git add .`

`git commit -m "updated submodule"`

`git push origin main`

- update containers