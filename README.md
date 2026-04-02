# cdsy2026

코디세이 미션1

## 1. 프로젝트 개요
- Docker 기반 개발 환경 구축
- 컨테이너 실행 및 웹 서버 구성
- 볼륨 및 마운트 검증

## 2. 실행 환경
- OS: Windows / MacOS
- Shell: Git Bash / PowerShell
- Docker: 29.3.1
- Git: 2.53.0

## 3. 수행 체크리스트
- [x] 터미널 기본 조작 및 폴더 구성
- [x] 권한 실습
- [x] Docker 설치 및 점검
- [x] Docker 실행(hello-world)
- [x] 컨테이너 실행 실습
- [x] Dockerfile 기반 웹 서버
- [x] 포트 매핑 접속
- [x] 바인드 마운트
- [x] 볼륨 영속성
- [x] Git 설정 및 GitHub 연동

## 4. 수행 로그

### 터미널 기본 조작 및 폴더 구성
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

Server:
 Containers: 4
  Running: 0
  Paused: 0
  Stopped: 4
   Images: 2
```

### Docker 실행(hello-world)
이미지 = 설계도, 컨테이너 = 그 이미지를 기반으로 만든 실행 중인 가변 인스턴스(실행 환경).
(빌드) 이미지는 Dockerfile로 빌드, 컨테이너는 빌드 대상이 아니며 이미지를 기반으로 생성
(실행) 이미지는 직접 실행되는 개념이 아님, 컨테이너는 이미지에서 생성된 프로세스 집합과 쓰기 가능한 레이어를 포함한 실행 단위
(변경) 이미지는 기본적으로 불변이며 변경하려면 Dockerfile 수정 후 재빌드, 컨테이너는 실행 중 파일/설정 등을 변경 가능하나 하지만 제거하면 사라지므로 영구적 변경하려면 볼륨 사용

```bash
$ docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
Digest: sha256:452a468a4bf985040037cb6d5392410206e47db9bf5b7278d281f94d1c2d0931
Status: Image is up to date for hello-world:latest
docker.io/library/hello-world:latest

$ docker images
                                                                                               i Info →   U  In Use

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

$docker container prune
$docker image prune -a
```

## 5. 기존 Dockerfile 기반 커스텀 이미지 제작(웹 서버)
- 베이스 이미지: nginx:alpine
- 커스텀 내용: HTML 파일 복사

### 프로젝트 디렉토리 구조
cdsy2026/
├── app/           # 웹 서버 소스 (HTML 등)
│   └── index.html
├── docker/        # Docker 관련 파일
│   └── Dockerfile
├── README.md      # 기술 문서 (핵심)

```dockerfile
FROM nginx:alpine
COPY app/ /usr/share/nginx/html/
```

```bash
$ docker build -t my-web:1.0 .
$ docker run -d -p 8080:80 --name my-web my-web:1.0
```

## 6. 포트 매핑 및 접속 증거
각각의 컨테이너는 호스트와 격리된 고유한 네트워크 공간을 가지기 때문에 내부 포트는 기본적으로 외부에서 접근 불가, 
따라서 호스트나 외부 클라이언트가 컨테이너 내부에서 실행 중인 서비스를 사용하려면 트래픽을 특정한 컨테이너 포트로 전달하는 포트 포워딩 등의 방법이 필요, 
이러한 구조에서 컨테이너의 자동적인 외부 노출에 따른 보안 위험을 줄일수 있음

```bash
$ docker ps
CONTAINER ID   IMAGE        COMMAND                   CREATED          STATUS          PORTS                          
           NAMES
5519ada2e7ac   my-web:1.0   "/docker-entrypoint.…"   26 minutes ago   Up 26 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web
120ea18eb6a4   ubuntu       "/bin/bash"               50 minutes ago   Up 50 minutes                                  
           test-ubuntu

$ curl http://localhost:8080
<h1>Hello Docker, from yangcody</h1>
```

## 7. 마운트

## 8. Docker 볼륨 영속성 검증
```bash
$ docker volume create mydata
mydata

$ docker volume ls
DRIVER    VOLUME NAME
local     mydata

$ docker run -d \
--name vol-test \
-v mydata:/data \
ubuntu sleep infinity
aad477dac14fbf4867ef1f513aec1c438cad1c91f552374725f14bfaf5ae7a6f

$ docker exec -it vol-test bash
root@aad477dac14f:/# echo hello > /data/test.txt
root@aad477dac14f:/# cat /data/test.txt
hello
root@aad477dac14f:/# exit
exit

$ docker rm -f vol-test
vol-test

$ docker run -d \
--name vol-test2 \
-v mydata:/data \
ubuntu sleep infinity
dab6489b4f1511aee66d50b691b5972fdf6ef1ea4694a2c56631cc4c7fd6645b

$ docker exec -it vol-test2 cat /data/test.txt
hello
```

## 9. Git 설정 및 GitHub 연동
```bash
$ git config --global user.name "yangcody"
$ git config --global user.email "your-email@example.com"
$ git config --global init.defaultBranch main

$ git config --list
init.defaultbranch=master
user.name=yangcody
user.email=astylus@naver.com
```
## 10. 트러블슈팅

