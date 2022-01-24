docker build -t myjenkins-blueocean:1. -f Dockerfile.jenkins .
docker stack deploy -c docker-compose-jenkins.yml jenkins