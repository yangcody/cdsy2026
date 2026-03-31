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

\### 터미널 기본 조작

bash$ pwd

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

\### 권한 실습

bash$ cd practice

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

## 5\. Dockerfile

## 6\. 포트 매핑

## 7\. 마운트

## 8\. 볼륨

## 9\. Git 설정

## 10\. 트러블슈팅

