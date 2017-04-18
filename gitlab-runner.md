Run gitlab-runner in a container

Docker image installation and configuration

Install Docker first:

curl -sSL https://get.docker.com/ | sh
We need to mount a config volume into our gitlab-runner container to be used for configs and other resources:

docker run -d --name gitlab-runner --restart always \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  gitlab/gitlab-runner:latest
OR you can use a config container to mount your custom data volume:

docker run -d --name gitlab-runner-config \
    -v /etc/gitlab-runner \
    busybox:latest \
    /bin/true

docker run -d --name gitlab-runner --restart always \
    --volumes-from gitlab-runner-config \
    gitlab/gitlab-runner:latest
If you plan on using Docker as the method of spawning runners, you will need to mount your docker socket like this:

docker run -d --name gitlab-runner --restart always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  gitlab/gitlab-runner:latest
Register the runner:

docker exec -it gitlab-runner gitlab-runner register

Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com )
https://gitlab.com
Please enter the gitlab-ci token for this runner
xxx
Please enter the gitlab-ci description for this runner
my-runner
INFO[0034] fcf5c619 Registering runner... succeeded
Please enter the executor: shell, docker, docker-ssh, ssh?
docker
Please enter the Docker image (eg. ruby:2.1):
ruby:2.1
INFO[0037] Runner registered successfully. Feel free to start it, but if it's
running already the config should be automatically reloaded!
The runner should is started already and you are ready to build your projects!

Make sure that you read the FAQ section which describes some of the most common problems with GitLab Runner.

Update

Pull the latest version:

docker pull gitlab/gitlab-runner:latest
Stop and remove the existing container:

docker stop gitlab-runner && docker rm gitlab-runner
Start the container as you did originally:

docker run -d --name gitlab-runner --restart always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  gitlab/gitlab-runner:latest
Note: you need to use the same method for mounting you data volume as you did originally (-v /srv/gitlab-runner/config:/etc/gitlab-runner or --volumes-from gitlab-runner)
