# Gitlab

## 环境搭建

1. Docker运行Gitlab

    - 在 macOS 和 Linux 系统上

        ```shell
        docker run -d --name gitlab -h gitlab.wax.com \
        --rm \
        -p 80:80 \
        -p 443:443 \
        -p 2289:22 \
        --env GITLAB_OMNIBUS_CONFIG="external_url 'http://localhost:80/';" \
        -v /srv/gitlab/config:/etc/gitlab \
        -v /srv/gitlab/logs:/var/log/gitlab \
        -v /srv/gitlab/data:/var/opt/gitlab \
        gitlab/gitlab-ce:12.10.3-ce.0
        ```

    - 在Windows系统上

        ```shell
        docker run -d --name gitlab ^
        --rm \
        -p 80:80 ^
        -p 443:443 ^
        -p 2289:22 ^
        --env GITLAB_OMNIBUS_CONFIG="external_url 'http://localhost:80/';" \
        -v /srv/gitlab/config:/etc/gitlab ^
        -v /srv/gitlab/logs:/var/log/gitlab ^
        -v /srv/gitlab/data:/var/opt/gitlab ^
        gitlab/gitlab-ce:12.10.3-ce.0
        ```

2. 配置external_url (可选)

    ```shell
    docker exec -it gitlab vim /etc/gitlab/gitlab.rb
    external_url 'https://gitlab.example.com'
    ```
