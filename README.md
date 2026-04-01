# cdsy2026

코디세이 미션1

## 1\. 프로젝트 개요

## 2\. 실행 환경

## 3\. 수행 체크리스트

* \[ ] 터미널
* \[ ] 권한
* \[ ] Docker
* \[ ] Dockerfile
* \[ ] 포트
* \[ ] 마운트
* \[ ] 볼륨
* \[ ] Git/GitHub

## 4\. 수행 로그

### 터미널 기본 조작

bash

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

### 권한 실습

bash

$ cd practice

$ touch test.txt

$ mkdir testdir

$ ls -l

total 0

\-rw-r--r-- 1 lenovo 197121 0 Apr  1 00:37 test.txt

drwxr-xr-x 1 lenovo 197121 0 Apr  1 00:37 testdir/

$ chmod 777 test.txt

$ chmod 700 testdir

$ ls -l

total 0

\-rwxrwxrwx 1 lenovo 197121 0 Apr  1 00:37 test.txt

drwx------ 1 lenovo 197121 0 Apr  1 00:37 testdir/



### Docker 설치 및 점검

bash

$ docker --version

Docker version 29.3.1, build c2be9cc

$ docker info

Client:

&#x20;Version:    29.3.1

&#x20;Context:    desktop-linux

&#x20;Debug Mode: false

&#x20;Plugins:

&#x20; agent: Docker AI Agent Runner (Docker Inc.)

&#x20;   Version:  v1.34.0

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-agent.exe

&#x20; ai: Docker AI Agent - Ask Gordon (Docker Inc.)

&#x20;   Version:  v1.20.1

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-ai.exe

&#x20; buildx: Docker Buildx (Docker Inc.)

&#x20;   Version:  v0.32.1-desktop.1

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-buildx.exe

&#x20; compose: Docker Compose (Docker Inc.)

&#x20;   Version:  v5.1.1

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-compose.exe

&#x20; debug: Get a shell into any image or container (Docker Inc.)

&#x20;   Version:  0.0.47

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-debug.exe

&#x20; desktop: Docker Desktop commands (Docker Inc.)

&#x20;   Version:  v0.3.0

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-desktop.exe

&#x20; dhi: CLI for managing Docker Hardened Images (Docker Inc.)

&#x20;   Version:  v0.0.2

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-dhi.exe

&#x20; extension: Manages Docker extensions (Docker Inc.)

&#x20;   Version:  v0.2.31

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-extension.exe

&#x20; init: Creates Docker-related starter files for your project (Docker Inc.)

&#x20;   Version:  v1.4.0

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-init.exe

&#x20; mcp: Docker MCP Plugin (Docker Inc.)

&#x20;   Version:  v0.40.3

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-mcp.exe

&#x20; model: Docker Model Runner (Docker Inc.)

&#x20;   Version:  v1.1.28

&#x20;   Path:     C:\\Users\\lenovo\\.docker\\cli-plugins\\docker-model.exe

&#x20; offload: Docker Offload (Docker Inc.)

&#x20;   Version:  v0.5.77

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-offload.exe

&#x20; pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)

&#x20;   Version:  v0.0.24

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-pass.exe

&#x20; sandbox: Docker Sandbox (Docker Inc.)

&#x20;   Version:  v0.12.0

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-sandbox.exe

&#x20; sbom: View the packaged-based Software Bill Of Materials (SBOM) for an image (Anchore Inc.)

&#x20;   Version:  0.6.0

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-sbom.exe

&#x20; scout: Docker Scout (Docker Inc.)

&#x20;   Version:  v1.20.3

&#x20;   Path:     C:\\Program Files\\Docker\\cli-plugins\\docker-scout.exe



Server:

&#x20;Containers: 4

&#x20; Running: 0

&#x20; Paused: 0

&#x20; Stopped: 4

&#x20;Images: 2

&#x20;Server Version: 29.3.1

&#x20;Storage Driver: overlayfs

&#x20; driver-type: io.containerd.snapshotter.v1

&#x20;Logging Driver: json-file

&#x20;Cgroup Driver: cgroupfs

&#x20;Cgroup Version: 2

&#x20;Plugins:

&#x20; Volume: local

&#x20; Network: bridge host ipvlan macvlan null overlay

&#x20; Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog

&#x20;CDI spec directories:

&#x20; /etc/cdi

&#x20; /var/run/cdi

&#x20;Discovered Devices:

&#x20; cdi: docker.com/gpu=webgpu

&#x20;Swarm: inactive

&#x20;Runtimes: io.containerd.runc.v2 nvidia runc

&#x20;Default Runtime: runc

&#x20;Init Binary: docker-init

&#x20;containerd version: dea7da592f5d1d2b7755e3a161be07f43fad8f75

&#x20;runc version: v1.3.4-0-gd6d73eb8

&#x20;init version: de40ad0

&#x20;Security Options:

&#x20; seccomp

&#x20;  Profile: builtin

&#x20; cgroupns

&#x20;Kernel Version: 6.6.87.2-microsoft-standard-WSL2

&#x20;Operating System: Docker Desktop

&#x20;OSType: linux

&#x20;Architecture: x86\_64

&#x20;CPUs: 8

&#x20;Total Memory: 7.617GiB

&#x20;Name: docker-desktop

&#x20;ID: 1d44c52d-818b-48e8-a4f5-da5193072a67

&#x20;Docker Root Dir: /var/lib/docker

&#x20;Debug Mode: false

&#x20;HTTP Proxy: http.docker.internal:3128

&#x20;HTTPS Proxy: http.docker.internal:3128

&#x20;No Proxy: hubproxy.docker.internal

&#x20;Labels:

&#x20; com.docker.desktop.address=npipe://\\\\.\\pipe\\docker\_cli

&#x20;Experimental: false

&#x20;Insecure Registries:

&#x20; hubproxy.docker.internal:5555

&#x20; ::1/128

&#x20; 127.0.0.0/8

&#x20;Live Restore Enabled: false

&#x20;Firewall Backend: iptables







\### Docker 기본 명령 실행

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

## 5\. Dockerfile

## 6\. 포트 매핑

## 7\. 마운트

## 8\. 볼륨

## 9\. Git 설정

## 10\. 트러블슈팅

