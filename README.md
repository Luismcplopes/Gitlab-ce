# Gitlab-ce
The latest docker guide can be found here: GitLab Docker images.
https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/docker/README.md
https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/docker/README.md#install-gitlab-using-docker-compose

https://github.com/gitlabhq/gitlabhq


sudo docker container run --detach  --publish 8929:80 --publish 2289:22 --name gitlab --restart always --volume /srv/gitlab/config:/etc/gitlab --volume /srv/gitlab/logs:/var/log/gitlab --volume /srv/gitlab/data:/var/opt/gitlab gitlab/gitlab-ce:latest
root qwertyuui 



sudo docker run --detach \
    --hostname gitlab.example.com \
    --publish 8929:80 --publish 2289:22 \
    --name gitlab \
    --restart always \
    --volume /srv/gitlab/config:/etc/gitlab \
    --volume /srv/gitlab/logs:/var/log/gitlab \
    --volume /srv/gitlab/data:/var/opt/gitlab \
    gitlab/gitlab-ce:latest
