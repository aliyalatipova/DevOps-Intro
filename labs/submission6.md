```
docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

```
docker pull ubuntu:latest
docker images ubuntu
latest: Pulling from library/ubuntu
01d7766a2e4a: Pull complete
fd8cda969ed2: Download complete                                                                                                              
Digest: sha256:d1e2e92c075e5ca139d51a140fff46f84315c0fdce203eab2807c7e495eff4f9
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
                                                                                                                         i Info →   U  In Use
IMAGE           ID             DISK USAGE   CONTENT SIZE   EXTRA
ubuntu:latest   d1e2e92c075e        119MB         31.7MB
```

```
 docker run -it --name ubuntu_container ubuntu:latest
root@b48f92221f01:/# 
```

```
# cat /etc/os-release
PRETTY_NAME="Ubuntu 24.04.4 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.4 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
root@b48f92221f01:/#
```
```
ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   4588  3888 pts/0    Ss   07:51   0:00 /bin/bash
root          10  0.0  0.0   7888  3888 pts/0    R+   07:52   0:00 ps aux
root@b48f92221f01:/#
```

```
 docker save -o ubuntu_image.tar ubuntu:latest
ls -lh ubuntu_image.tar
-rwxrwxrwx 1 aliya aliya 31M Mar 12 10:53 ubuntu_image.tar
```

```Attempt Image Removal:
 docker rmi ubuntu:latest
Error response from daemon: conflict: unable to delete ubuntu:latest (must be forced) - container b48f92221f01 is using its referenced image d1e2e92c075e
```

```Remove Container and Retry:
 docker rm ubuntu_container
docker rmi ubuntu:latest
ubuntu_container
Untagged: ubuntu:latest
Deleted: sha256:d1e2e92c075e5ca139d51a140fff46f84315c0fdce203eab2807c7e495eff4f9
```
Разница между DISK USAGE и CONTENT SIZE объясняется тем, что DISK USAGE включает общие слои, используемые другими образами, а CONTENT SIZE — это уникальный размер данного образа. Размер tar-файла примерно равен CONTENT SIZE, потому что docker save упаковывает только уникальные слои образа и метаданные, без дублирования.

При попытке удалить образ ubuntu:latest возникает ошибка, потому что существует контейнер ubuntu_container, созданный на основе этого образа. Даже если контейнер остановлен, он сохраняет ссылку на образ. Docker блокирует удаление образа, чтобы не нарушить целостность существующих контейнеров (их нельзя будет запустить повторно). Только после удаления контейнера (docker rm ubuntu_container) образ можно удалить без принуждения.

Команда docker save создаёт архив, содержащий все слои файловой системы образа, а также метаданные (конфигурацию образа, историю, теги). Этот архив можно восстановить командой docker load, получив точную копию образа. В отличие от docker export, который экспортирует только файловую систему контейнера, docker save сохраняет структуру образа, включая его историю и слои.



## Task 2

```
 docker run -d -p 80:80 --name nginx_container nginx
curl http://localhost
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
9eef040df109: Pull complete
a9d395129dce: Pull complete
75a1d70aee50: Pull complete
79697674b897: Pull complete
206356c42440: Pull complete
18a071c04bd1: Pull complete
df9da45c1db2: Pull complete
d99947bc9177: Download complete                                                                                                              
23abb0f9ce55: Download complete
Digest: sha256:bc45d248c4e1d1709321de61566eb2b64d4f0e32765239d66573666be7f13349
Status: Downloaded newer image for nginx:latest
d47b0c229b00faf18831148a7a61f63ede18de9e13a04cf411b58e3ab8f8806f
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working.
Further configuration is required for the web server, reverse proxy,
API gateway, load balancer, content cache, or other features.</p>

<p>For online documentation and support please refer to
<a href="https://nginx.org/">nginx.org</a>.<br/>
To engage with the community please visit
<a href="https://community.nginx.org/">community.nginx.org</a>.<br/>
For enterprise grade support, professional services, additional
security features and capabilities please refer to
<a href="https://f5.com/nginx">f5.com/nginx</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

````
docker cp index.html nginx_container:/usr/share/nginx/html/
Successfully copied 2.05kB to nginx_container:/usr/share/nginx/html/
````
````
curl http://localhost
<html>
<head>
<title>The best</title>
</head>
<body>
<h1>website</h1>
</body>
</html>
````

````
 docker commit nginx_container my_website:latest
docker images my_website
sha256:763fc76c001745f4300c3b5f7fe512df1d0280b520c192ba0187fa7e430bb0df
                                                                                                                         i Info →   U  In Use
IMAGE               ID             DISK USAGE   CONTENT SIZE   EXTRA
my_website:latest   763fc76c0017        237MB           63MB
````

````
docker rm -f nginx_container
docker run -d -p 80:80 --name my_website_container my_website:latest
curl http://localhost
nginx_container
0e156e1ecd908a43f0294cf77757f8b51d855e4db377da90f81a7f6178bae85f
curl: (56) Recv failure: Connection reset by peer
````

````
docker diff my_website_container
C /run
C /run/nginx.pid
C /etc
C /etc/nginx
C /etc/nginx/conf.d
C /etc/nginx/conf.d/default.conf
````

Вывод показывает изменения в файловой системе контейнера относительно образа, из которого он создан.
- `A` (Added) — файл/папка добавлены
- `C` (Changed) — изменены
- `D` (Deleted) — удалены

В моём случае все строки начинаются с `C`, то есть файлы были изменены:
- `/run/nginx.pid` — создаётся при запуске nginx, содержит PID процесса.
- `/etc/nginx/conf.d/default.conf` — возможно, nginx при старте модифицирует конфигурацию (например, обновляет ссылки).

## Task3

````Create Bridge Network
 docker network create lab_network
docker network ls
c1d8f3391a98df737a5c6f828855501be976e326eec3ffcb3d28a48020ee6f89
NETWORK ID     NAME          DRIVER    SCOPE
705be9b23fdf   bridge        bridge    local
e51dbc16f981   host          host      local
c1d8f3391a98   lab_network   bridge    local
97e0362325f6   none          null      local
````

````Deploy Connected Containers:
 docker run -dit --network lab_network --name container1 alpine ash
docker run -dit --network lab_network --name container2 alpine ash
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
589002ba0eae: Pull complete
caa817ad3aea: Download complete
9e595aac14e0: Download complete                                                                                                              
Digest: sha256:25109184c71bdad752c8312a8623239686a9a2071e8825f20acb8f2198c3f659
Status: Downloaded newer image for alpine:latest
a7ecf055b8e1098413d0566fa36f23f18d9d67abc02410408f93ab7a4fd1500f
2005daf84cc8ddf5895e93f42a6bcf017b85c9d37c9d3e3f527a046ee6843acd
````

````Test Container-to-Container Communication:
docker exec container1 ping -c 3 container2
PING container2 (172.18.0.3): 56 data bytes
64 bytes from 172.18.0.3: seq=0 ttl=64 time=1.857 ms
64 bytes from 172.18.0.3: seq=1 ttl=64 time=0.145 ms
64 bytes from 172.18.0.3: seq=2 ttl=64 time=0.140 ms

--- container2 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.140/0.714/1.857 ms
````

````
 docker network inspect lab_network
[
    {
        "Name": "lab_network",
        "Id": "c1d8f3391a98df737a5c6f828855501be976e326eec3ffcb3d28a48020ee6f89",
        "Created": "2026-03-12T11:09:46.405984359+03:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv4": true,
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Options": {},
        "Labels": {},
        "Containers": {
            "2005daf84cc8ddf5895e93f42a6bcf017b85c9d37c9d3e3f527a046ee6843acd": {
                "Name": "container2",
                "EndpointID": "3b8bd0f8116469cad5b47694392afe958083ac123121a31b73a1e0e41d899f4d",
                "MacAddress": "0e:85:51:18:e3:ad",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            },
            "a7ecf055b8e1098413d0566fa36f23f18d9d67abc02410408f93ab7a4fd1500f": {
                "Name": "container1",
                "EndpointID": "b386ab8b08ad2f6fd9c045cd29444e3f9bf7752e0a865cdb69c68355b6cc780b",
                "MacAddress": "26:1c:1e:a4:bb:97",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            }
        },
        "Status": {
            "IPAM": {
                "Subnets": {
                    "172.18.0.0/16": {
                        "IPsInUse": 5,
                        "DynamicIPsAvailable": 65531
                    }
                }
            }
        }
    }
]
````

````
 docker exec container1 nslookup container2
Server:         127.0.0.11
Address:        127.0.0.11:53

Non-authoritative answer:

Non-authoritative answer:
Name:   container2
Address: 172.18.0.3
````

Docker запускает встроенный DNS-сервер, доступный контейнерам по адресу 127.0.0.11. Когда контейнеры подключаются к пользовательской bridge-сети (lab_network), Docker автоматически регистрирует их имена в этом DNS. Благодаря этому контейнеры могут обращаться друг к другу по именам, а не по IP. В выводе nslookup видно, что имя container2 успешно резолвится в его IP 172.18.0.3. Это основа для service discovery в микросервисных архитектурах

## Task4

````
 docker volume create app_data
docker volume ls
app_data
DRIVER    VOLUME NAME
local     app_data
````

````
docker run -d -p 80:80 -v app_data:/usr/share/nginx/html --name web_new nginx
728deaa7cb2605a3caa4bef9694e05f43e4b8e1f3ec2015ab2c08ed52bf28d9b
docker: Error response from daemon: failed to set up container networking: driver failed programming external connectivity on endpoint web_new (8054ded746e3325411592c626404c1265866456073b3b6214180cea2ef95b3f9): Bind for 0.0.0.0:80 failed: port is already allocated
````

````
curl http://localhost
<html>
<head>
<title>The best</title>
</head>
<body>
<h1>website</h1>
</body>
</html>
````

````
 docker volume inspect app_data
[
    {
        "CreatedAt": "2026-03-12T19:43:59+03:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/app_data/_data",
        "Name": "app_data",
        "Options": null,
        "Scope": "local"
    }
]
````

Контейнеры по временны. Они могут быть остановлены, удалены или пересозданы в любой момент 

Внутренняя файловая система контейнера существует только во время его жизни. При удалении контейнера все данные, записанные внутри него, теряются безвозвратно.

Многие приложения должны сохранять состояние между перезапусками. Потеря данных может привести к серьёзным последствиям.

Использование volumes позволяет отделить данные от жизненного цикла контейнера: данные хранятся на хосте или в удалённом хранилище и могут быть переиспользованы новыми контейнерами.

Это также упрощает обновление приложений: можно удалить старый контейнер и запустить новый с той же версией образа, но подключив существующий том — данные останутся.

