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
        --env GITLAB_OMNIBUS_CONFIG="external_url 'https://localhost:80';" \
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
        --env GITLAB_OMNIBUS_CONFIG="external_url 'https://localhost:80';" \
        -v /srv/gitlab/config:/etc/gitlab ^
        -v /srv/gitlab/logs:/var/log/gitlab ^
        -v /srv/gitlab/data:/var/opt/gitlab ^
        gitlab/gitlab-ce:12.10.3-ce.0
        ```

2. 配置external_url

    ```shell
    docker exec -it gitlab vim /etc/gitlab/gitlab.rb

    external_url 'https://gitlab.example.com'
    ```

3. 配置邮箱 (可选)

    ```shell
    docker exec -it gitlab vim /etc/gitlab/gitlab.rb

    gitlab_rails['smtp_enable'] = true
    gitlab_rails['smtp_address'] = "smtp.163.com"
    gitlab_rails['smtp_port'] = 25
    gitlab_rails['smtp_user_name'] = "xxxx@163.com"
    gitlab_rails['smtp_password'] = "xxxxpassword"
    gitlab_rails['smtp_domain'] = "163.com"
    gitlab_rails['smtp_authentication'] = "login"
    gitlab_rails['smtp_enable_starttls_auto'] = false
    gitlab_rails['smtp_openssl_verify_mode'] = "peer"

    gitlab_rails['gitlab_email_from'] = "xxxx@163.com"
    user["git_user_email"] = "xxxx@163.com"
    ```
