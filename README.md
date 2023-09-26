## Requirements
- Docker Compose

## Deployment

- add submodule of your app
`git submodule add url-to-git-repository name-of-app`
- initialize and update submodules
`git submodule init`
`git submodule update`
- add your app as service to the docker compose file
- run docker compose `docker-compose up --build`

