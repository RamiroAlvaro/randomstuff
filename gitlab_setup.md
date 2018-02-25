/home/ubuntu/dkgitlab.sh

```
sudo docker run --detach \
    --hostname gitlab.example.com \
    --publish 8443:443 --publish 8080:80 --publish 2222:22 \
    --name gitlab \
    --restart always \
    --volume /home/ubuntu/dkdata/gitlab/config:/etc/gitlab \
    --volume /home/ubuntu/dkdata/gitlab/logs:/var/log/gitlab \
    --volume /home/ubuntu/dkdata/gitlab/data:/var/opt/gitlab \
    gitlab/gitlab-ce:latest
```

/etc/nginx/sites-enabled/gitlab.conf

```
server {
   server_name gitlab.memoreba.com.br;
   listen 80

   location / {
        proxy_pass http://localhost:8080;
        include proxy_params;
   }
}
```

/home/ubuntu/dkdata/gitlab/config/gitlab.rb

```
...
gitlab_rails['gitlab_shell_ssh_port'] = 2222
```
