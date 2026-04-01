# cdsy2026

코디세이 미션1

## 1. 프로젝트 개요

## 2. 실행 환경

## 3. 수행 체크리스트

* [ ] 터미널
* [ ] 권한
* [ ] Docker
* [ ] Dockerfile
* [ ] 포트
* [ ] 마운트
* [ ] 볼륨
* [ ] Git/GitHub

## 4. 수행 로그

### 터미널 기본 조작

```bash

$ pwd

/c/Users/yangcody/cdsy2026

$ mkdir practice

$ cd practice

$ pwd

/c/Users/yangcody/cdsy2026/practice

$ ls -la

total 4

drwxr-xr-x 1 lenovo 197121 0 Apr  1 00:08 ./

drwxr-xr-x 1 lenovo 197121 0 Apr  1 00:08 ../

$ touch file1.txt

$ cat file1.txt

$ cp file1.txt file2.txt

$ mv file2.txt file3.txt

$ mkdir dir1

$ mv file3.txt dir1/

$ rm file1.txt

$ rm -r dir1
```

### 권한 실습

```bash

$ cd practice

$ touch test.txt

$ mkdir testdir

$ ls -l

total 0

-rw-r--r-- 1 lenovo 197121 0 Apr  1 00:37 test.txt

drwxr-xr-x 1 lenovo 197121 0 Apr  1 00:37 testdir/

$ chmod 777 test.txt

$ chmod 700 testdir

$ ls -l

total 0

-rwxrwxrwx 1 lenovo 197121 0 Apr  1 00:37 test.txt

drwx------ 1 lenovo 197121 0 Apr  1 00:37 testdir/
```

### Docker 설치 및 점검
```bash
$ docker --version
Docker version 29.3.1, build c2be9cc

$ docker info
Client:
 Version:    29.3.1
 Context:    desktop-linux
 Debug Mode: false
 Plugins:
  agent: Docker AI Agent Runner (Docker Inc.)
    Version:  v1.34.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-agent.exe
  ai: Docker AI Agent - Ask Gordon (Docker Inc.)
    Version:  v1.20.1
    Path:     C:\Program Files\Docker\cli-plugins\docker-ai.exe
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.32.1-desktop.1
    Path:     C:\Program Files\Docker\cli-plugins\docker-buildx.exe
  compose: Docker Compose (Docker Inc.)
    Version:  v5.1.1
    Path:     C:\Program Files\Docker\cli-plugins\docker-compose.exe
  debug: Get a shell into any image or container (Docker Inc.)
    Version:  0.0.47
    Path:     C:\Program Files\Docker\cli-plugins\docker-debug.exe
  desktop: Docker Desktop commands (Docker Inc.)
    Version:  v0.3.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-desktop.exe
  dhi: CLI for managing Docker Hardened Images (Docker Inc.)
    Version:  v0.0.2
    Path:     C:\Program Files\Docker\cli-plugins\docker-dhi.exe
  extension: Manages Docker extensions (Docker Inc.)
    Version:  v0.2.31
    Path:     C:\Program Files\Docker\cli-plugins\docker-extension.exe
  init: Creates Docker-related starter files for your project (Docker Inc.)
    Version:  v1.4.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-init.exe
  mcp: Docker MCP Plugin (Docker Inc.)
    Version:  v0.40.3
    Path:     C:\Program Files\Docker\cli-plugins\docker-mcp.exe
  model: Docker Model Runner (Docker Inc.)
    Version:  v1.1.28
    Path:     C:\Users\lenovo\.docker\cli-plugins\docker-model.exe
  offload: Docker Offload (Docker Inc.)
    Version:  v0.5.77
    Path:     C:\Program Files\Docker\cli-plugins\docker-offload.exe
  pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)
    Version:  v0.0.24
    Path:     C:\Program Files\Docker\cli-plugins\docker-pass.exe
  sandbox: Docker Sandbox (Docker Inc.)
    Version:  v0.12.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-sandbox.exe
  sbom: View the packaged-based Software Bill Of Materials (SBOM) for an image (Anchore Inc.)
    Version:  0.6.0
    Path:     C:\Program Files\Docker\cli-plugins\docker-sbom.exe
  scout: Docker Scout (Docker Inc.)
    Version:  v1.20.3
    Path:     C:\Program Files\Docker\cli-plugins\docker-scout.exe

Server:
 Containers: 4
  Running: 0
  Paused: 0
  Stopped: 4
 Images: 2
 Server Version: 29.3.1
 Storage Driver: overlayfs
  driver-type: io.containerd.snapshotter.v1
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Discovered Devices:
  cdi: docker.com/gpu=webgpu
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 nvidia runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: dea7da592f5d1d2b7755e3a161be07f43fad8f75
 runc version: v1.3.4-0-gd6d73eb8
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.6.87.2-microsoft-standard-WSL2
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 8
 Total Memory: 7.617GiB
 Name: docker-desktop
 ID: 1d44c52d-818b-48e8-a4f5-da5193072a67
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 HTTP Proxy: http.docker.internal:3128
 HTTPS Proxy: http.docker.internal:3128
 No Proxy: hubproxy.docker.internal
 Labels:
  com.docker.desktop.address=npipe://\\.\pipe\docker_cli
 Experimental: false
 Insecure Registries:
  hubproxy.docker.internal:5555
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Firewall Backend: iptables
```
### Docker 기본 명령 실행
```bash
$ docker pull hello-world

Using default tag: latest

latest: Pulling from library/hello-world

Digest: sha256:452a468a4bf985040037cb6d5392410206e47db9bf5b7278d281f94d1c2d0931

Status: Image is up to date for hello-world:latest

docker.io/library/hello-world:latest

$ docker images

&#x20;                                                                                                i Info →   U  In Use

IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA

hello-world:latest   452a468a4bf9       25.9kB         9.49kB    U

ubuntu:latest        186072bba1b2        119MB         31.7MB    U

$ docker run hello-world

Hello from Docker!

This message shows that your installation appears to be working correctly.

$ docker ps

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

$ docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES

76beaf25fbd4   hello-world   "/hello"   26 seconds ago   Exited (0) 25 seconds ago             elated\_bohr

1faf346438c7   ubuntu        "bash"     24 minutes ago   Exited (0) 24 minutes ago             youthful\_joliot

9f5b56e66c41   ubuntu        "bash"     25 minutes ago   Exited (0) 24 minutes ago             elegant\_ishizaka

04290d1ea602   hello-world   "/hello"   25 minutes ago   Exited (0) 25 minutes ago             stupefied\_turing

e0dd622b7df4   hello-world   "/hello"   26 minutes ago   Exited (0) 26 minutes ago             charming\_fermat

$ docker logs 76beaf25fbd4

Hello from Docker!

This message shows that your installation appears to be working correctly.

$ docker stats

```
### 컨테이너 실행 실습

```bash

$ docker run hello-world

Hello from Docker!

$ docker run -it ubuntu bash

root@651cb4500a52:/# ls

bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

root@651cb4500a52:/# echo hello

hello

root@651cb4500a52:/# exit

exit

$ docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED              STATUS                          PORTS     NAMES

651cb4500a52   ubuntu        "bash"     52 seconds ago       Exited (0) 9 seconds ago                  stoic\_jang     

e6439c1662ba   hello-world   "/hello"   About a minute ago   Exited (0) About a minute ago             clever\_buck    

76beaf25fbd4   hello-world   "/hello"   14 minutes ago       Exited (0) 14 minutes ago                 elated\_bohr    

1faf346438c7   ubuntu        "bash"     39 minutes ago       Exited (0) 39 minutes ago                 youthful\_joliot

9f5b56e66c41   ubuntu        "bash"     39 minutes ago       Exited (0) 39 minutes ago                 elegant\_ishizaka

04290d1ea602   hello-world   "/hello"   40 minutes ago       Exited (0) 40 minutes ago                 stupefied\_turing

e0dd622b7df4   hello-world   "/hello"   40 minutes ago       Exited (0) 40 minutes ago                 charming\_fermat

$ docker run -dit --name test-ubuntu ubuntu

120ea18eb6a4a7f00a60e9dc8aea788eda866934686d68ee59cbf1cb843fe10d

$ docker ps

CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS         PORTS     NAMES

120ea18eb6a4   ubuntu    "/bin/bash"   10 seconds ago   Up 9 seconds             test-ubuntu

$ docker exec -it test-ubuntu bash

root@120ea18eb6a4:/# echo inside-container

inside-container

root@120ea18eb6a4:/# exit

exit
```


## 5. Dockerfile 기반 웹 서버

- 베이스 이미지: nginx:alpine
- 커스텀 내용: HTML 파일 복사

```dockerfile
FROM nginx:alpine
COPY app/ /usr/share/nginx/html/
```

```bash
$ docker build -t my-web:1.0 .
$ docker run -d -p 8080:80 --name my-web my-web:1.0
```

## 6. 포트 매핑 및 접속 증거
```bash
docker ps
CONTAINER ID   IMAGE        COMMAND                   CREATED          STATUS          PORTS                          
           NAMES
5519ada2e7ac   my-web:1.0   "/docker-entrypoint.…"   26 minutes ago   Up 26 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web
120ea18eb6a4   ubuntu       "/bin/bash"               50 minutes ago   Up 50 minutes                                  
           test-ubuntu
$ curl http://localhost:8080
<h1>Hello Docker, from yangcody</h1>
```

## 7. 마운트

## 8. 볼륨

## 9. Git 설정

## 10. 트러블슈팅

