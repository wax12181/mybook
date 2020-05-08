# Jenkins

## 环境搭建

1. Docker运行Jenkins

    - 在 macOS 和 Linux 系统上

        ```shell
        docker run \
        --rm \
        -u root \
        -p 8080:8080 \
        -v jenkins-data:/var/jenkins_home \
        -v /var/run/docker.sock:/var/run/docker.sock \
        -v "$HOME":/home \
        jenkinsci/blueocean
        ```

    - 在Windows系统上

        ```shell
        docker run ^
        --rm ^
        -u root ^
        -p 8080:8080 ^
        -v jenkins-data:/var/jenkins_home ^
        -v /var/run/docker.sock:/var/run/docker.sock ^
        -v "%HOMEPATH%":/home ^
        jenkinsci/blueocean
        ```
