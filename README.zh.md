# 自动配置ssl的nginx反代docker-compose模板

## 新建一个docker网络

1. 使用以下命令:

    ```docker network create nginx-ssl-proxy```

## 启动该服务

1. 使用以下命令开启服务:

    ```docker-compose up -d```

## 启动你的应用

1. 通过 docker-compose.yml 文件启动你的应用, 例如:

    ```yml
    version: '3'

    services:
    example-app:
        image: nginx:alpine
        expose:
        - 80
        environment:
        VIRTUAL_HOST: example.com
        VIRTUAL_PORT: 80
        LETSENCRYPT_HOST: example.com
        LETSENCRYPT_EMAIL: foo@example.com

    networks:
        default:
            external:
                name: nginx-ssl-proxy

    ```

2. 访问 example.com, 等待若干秒后, 查看 example.com 是否启用了`https`

## 参阅

- [https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion)
- [https://github.com/jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy)
