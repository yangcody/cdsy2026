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
절대 경로는 시스템 전체에서 항상 동일한 위치를 가리키는 경로(/로 시작)로서 안정적·명시적이므로 스케줄러·시스템 설정에 적합,
상대 경로는 현재 작업 디렉터리에서의 위치(./, ../ 등)로서, 유연하게 이식할수 있으므로 프로젝트 내부 협업이나 이동 가능한 코드에 적합.

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
숫자 표기는 owner/group/others 순서로 각 권한을 3비트(읽기/쓰기/실행)로 표현.
각 비트 값은 읽기(r)=4, 쓰기(w)=2, 실행(x)=1이며, 세 값을 더해서 0~7 중 하나의 숫자가 됨
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

├── app/

│   └── index.html

├── docker/        

│   └── Dockerfile

├── README.md     # 기술 문서 (핵심)

app/은 HTML 등 웹 서버 소스 저장, docker/에는 Docker 관련 파일 저장, 
README.md 파일에는 전체 프로젝트 설명을 기록하는 구조로 각각 디렉토리와 파일을 설정함

```dockerfile
FROM nginx:alpine
COPY app/ /usr/share/nginx/html/
```

```bash
$ docker build -t my-web:1.0 .
[+] Building 2.1s (7/7) FINISHED                                                                 docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                             0.1s
 => => transferring dockerfile: 90B                                                                              0.0s 
 => [internal] load metadata for docker.io/library/nginx:alpine                                                  1.4s 
 => [internal] load .dockerignore                                                                                0.0s
 => => transferring context: 2B                                                                                  0.0s 
 => [internal] load build context                                                                                0.0s 
 => => transferring context: 118B                                                                                0.0s 
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:e7257f1ef28ba17cf7c248cb8ccf6f0c6e0228ab9c315c152f9c203cd3  0.0s 
 => => resolve docker.io/library/nginx:alpine@sha256:e7257f1ef28ba17cf7c248cb8ccf6f0c6e0228ab9c315c152f9c203cd3  0.0s 
 => CACHED [2/2] COPY app/ /usr/share/nginx/html/                                                                0.0s 
 => exporting to image                                                                                           0.2s 
 => => exporting layers                                                                                          0.0s 
 => => exporting manifest sha256:c95562d4420dce78c187cab45312d498c51d4cad0c400993304f4b00b43bf341                0.0s 
 => => exporting config sha256:d198bcca978df0537e98850222e263a9802226208819aa2972e0eb1741bf611c                  0.0s
 => => exporting attestation manifest sha256:75cf50d7a6df9c0ed59bdd97d5473cfd702fa42664e5ca0cf0d5e3339c173bc4    0.0s 
 => => exporting manifest list sha256:bd51294ba87ee6a9935cd94b75a52a16ae35bdfcd9fa95091f6e7235790bc164           0.0s 
 => => naming to docker.io/library/my-web:1.0                                                                    0.0s 
 => => unpacking to docker.io/library/my-web:1.0     
$ docker run -d -p 8080:80 --name my-web my-web:1.0
```

docker에서 run으로 container를 개별 생성하는 방식 대신,
docker-compose.yml 파일을 생성 후 docker 실행명령을 저장하여 구성관리 하는 방식을 사용하면 
각종 설정의 재현가능성을 높여, 팀 공유를 용이하게 한다.
```bash
docker compose up
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

이 과정에서 “host port already in use” 발생한다면,
1) "docker ps" 명령으로 동일 포트를 사용 중인 컨테이너 식별 후 작동 정지 및 제거
2) 호스트 OS에서 해당 포트 사용하는 프로세스 확인하기 위해,
윈도우는 "netstat -ano | findstr :8080", 
macOS나 리눅스에서 "lsof -i :8080" 또는 "netstat -tulnp | grep 8080" 사용
3) 기존 실행한 컨테이너 종료 후 다른 포트로 실행

## 7. 바인드 마운트 반영
```bash
$ docker run -d -p 8080:80 -v $(pwd)/app:/usr/share/nginx/html --name my-web-bind my-web:1.0
5ac31a15ba128b035ddb3dc6a5e6886ed34fefa5ce36ffd9862a563c737fccb6
$ curl http://localhost:8080
<h1>Hello Docker</h1>
```

html 내용 변경(Hello Docker > Bind Mount Test)

```bash
$ curl http://localhost:8080
<h1>Bind Mount Test</h1>

$ docker exec -it my-web-bind cat /usr/share/nginx/html/index.html
<h1>Bind Mount Test</h1>

$ docker stop my-web-bind && docker rm my-web-bind
my-web-bind
my-web-bind
```

## 8. Docker 볼륨 영속성 검증
컨테이너의 일시적 쓰기 계층에 데이터를 두면 삭제 시 사라지므로, 
영속성을 위해 볼륨이나 바인드 마운트, 외부 스토리지를 사용해야 함

아래 예시에서는 mydata라는 volume을 생성하여,
vol-test 컨테이너를 mydata에 연결하고 컨테이너 내부에 데이터 저장 후 컨테이너 삭제,
새로운 컨테이너 생성하여 mydata에 연결 후 volume에 저장된 데이터를 불러오기 함

```bash
$ docker volume create mydata
mydata

$ docker volume ls
DRIVER    VOLUME NAME
local     mydata

$ docker run -d --name vol-test -v mydata:/data ubuntu sleep infinity
aad477dac14fbf4867ef1f513aec1c438cad1c91f552374725f14bfaf5ae7a6f

$ docker exec -it vol-test bash
root@aad477dac14f:/# echo hello > /data/test.txt
root@aad477dac14f:/# cat /data/test.txt
hello
root@aad477dac14f:/# exit
exit

$ docker rm -f vol-test
vol-test

$ docker run -d --name vol-test2 -v mydata:/data ubuntu sleep infinity
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

$ git add README.md

$ git commit -m "docs: bind mount"
[main 59a60b7] docs: bind mount
 1 file changed, 14 insertions(+), 1 deletion(-)

$ git push origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 561 bytes | 561.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/yangcody/cdsy2026.git
   ea413cb..59a60b7  main -> main
```

## 10. 트러블슈팅

- 바인드 마운트 컨테이너 실행 후 로컬 파일 변경하였으나 반영 안 되는 문제 발견,
Bash Shell에서는 실패 하였으나 윈도우 powershell에서는 정상 동작함을 확인,
절대 경로로 변환하여 재실행하였으나 실패,
ChatGPT의 도움으로 윈도우 Git Bash에서는 디렉토리 이름에서 "/"를 자동으로 "\" 변환하는 것을 파악하고,
해결방안을 찾을수 있었음

```bash
$ export MSYS_NO_PATHCONV=1
```

- github에 대한 이해 부족으로 코디세이에서 masOS로 일부만 push 하고 종료 하지 않은 상태에서, 집에서 pc에 새로 설치해서 clone이나 pull 없이 작업 후 push 하면서 repository가 중복/충돌하는 문제 발생, 챗gpt 통해서 문제를 진단하고 github 초기화 하여 다시 push 하여 문제 해결