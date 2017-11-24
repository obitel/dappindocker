# Dapp in Docker

----
Контейнер для сборки контейнера с помощью dapp от компании flant
https://github.com/flant/dapp
----
## Настройка GitLab Runner
Особенность - это докер сокет для управления докером хоста, и /tmp - для корректной работы кэша Dapp
```
[[runners]]
  name = "gitlab-runner-01"
  url = "https://git.local"
  token = "a5534fd58346ac5fc37ba2b71c79a"
  executor = "docker"
  [runners.docker]
    tls_verify = false
    image = "yourregistry.local/dapp_in_docker"
    privileged = false
    pull_policy = "if-not-present"
    disable_cache = false
    volumes = ["/cache", "/var/run/docker.sock:/var/run/docker.sock", "/tmp:/tmp"]
    shm_size = 0
  [runners.cache]
```

### Расширение сборочного контейнра требуемыми утилитами
```
before_setup do
   run 'curl -sL https://deb.nodesource.com/setup_8.x | bash -',
   'apt-get install -y nodejs'
end
```