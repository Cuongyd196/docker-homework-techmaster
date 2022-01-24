- Build image:
```sh
docker build -t myjenkins-blueocean:1. -f Dockerfile.jenkins .
```
- Docker stack deploy
```sh
docker stack deploy -c docker-compose-jenkins.yml jenkins
```