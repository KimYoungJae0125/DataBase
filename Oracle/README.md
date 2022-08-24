# Oracle 설치

### Mac OS 기준
#### CPU : Intel

### [참고]

<details>
<summary> 맥에서 오라클 사용은 도커를 써야해요</summary>

> - Mac OS 에서는 맥 버전 오라클을 지원하지 않는다.
> - 그렇기 때문에 가상 환경을 만들어주는 도커를 이용하여 설치를 할 것이다.
> - 도커는 리눅스 기반 가상 컨테이너로 리눅스 환경을 가진 가상 공간을 만들어준다

</details>

<br>

## 1. 도커  설치
https://github.com/KimYoungJae0125/Computer-Setting/blob/main/Mac-Setting/Docker-Setting/Docker-Setting.md

<br>

## 2. 도커에서 Oracle 이미지 찾기
```shell
$ docker search oracle
```

### [참고]

<details>
<summary> 특정 버전을 찾을 시

</summary>

> ```shell
> $ docker search oracle{version}
> ex) $ docker search oracle-xe-11g
> ```
> - oracle-xe-11g 이미지를 찾게 된다.

</details>


<br>

## 3. Oracle 설치
```shell
$ docker pull jaspeen/oracle-xe-11g
```

<details>
<summary>console</summary>

```shell
Using default tag: latest
latest: Pulling from jaspeen/oracle-xe-11g
Image docker.io/jaspeen/oracle-xe-11g:latest uses outdated schema1 manifest format. Please upgrade to a schema2 image for better future compatibility. More information at https://docs.docker.com/registry/spec/deprecated-schema-v1/
863735b9fd15: Pull complete 
4fbaa2f403df: Pull complete 
44be94a95984: Pull complete 
a3ed95caeb02: Pull complete 
05b9ddeb40d9: Pull complete 
b44894d2d2af: Pull complete 
1492d1fc5b9f: Pull complete 
c0f3c6ec8986: Pull complete 
fbfc89a21b1b: Pull complete 
740047056d21: Pull complete 
Digest: sha256:0a4b0456cd5be4982ab28ca9426672acee6d90734873d15124698c5c07055aa9
Status: Downloaded newer image for jaspeen/oracle-xe-11g:latest
docker.io/jaspeen/oracle-xe-11g:latest
```

</details>

<br>

## 4. Oracle 이미지 설치 확인
```shell
$ docker images
```

```shell
REPOSITORY              TAG       IMAGE ID       CREATED         SIZE
jaspeen/oracle-xe-11g   latest    52fbd1fe2d7a   6 years ago     792MB
```

### [참고]

<details>
<summary>도커에서 이미지란?</summary>

> - 도커 컨테이너에서 프로세스를 실행시키기 위한 파일들이 모여있는 것   
> - 위의 jaspeen/oracle-xe-11g 이미지에는 oracle-xe-11g 실행에 관련 된 파일 정보들이 들어있다.

</details>


<br>

### 5. Oracle 컨테이너 생성 및 실행
```shell
$ docker run --name oracle -d -p 1521:1521 jaspeen/oracle-xe-11g
```

### 5-1. Oracle 컨테이너 실행 확인
```shell
$ docker ps
```

```shell
CONTAINER ID   IMAGE                   COMMAND             CREATED         STATUS         PORTS                              NAMES
1d040bc54d63   jaspeen/oracle-xe-11g   "/entrypoint.sh "   6 seconds ago   Up 5 seconds   0.0.0.0:1521->1521/tcp, 8080/tcp   oracle
```

### [참고]

<details>
<summary>도커에서 컨테이너란</summary>

> - 이미지를 실행한 상태, 이미지만 가지고는 도커에서 프로세스를 수행시키지 못 한다.   
> - 자바로 예를 들자면, 이미지는 war 파일 컨테이너는 war 파일을 실행한 것이라 생각하면 된다.   
> - 하나의 컨테이너는 하나의 서버를 가지고 있는 것과 동일하며, 해당 컨테이너가 삭제 될 경우 해당 컨테이너 내부의 정보가 모두 삭제된다.   
> - 물론 컨테이너를 삭제하지 않고, 잠시 중단만 시키는 것은 데이터가 삭제 되지 않고 남아있는다.

</details>

<br>

### 6. Oracle 컨테이너 접속
```shell
$ docker exec -it oracle sqlplus
```

```shell
SQL*Plus: Release 11.2.0.2.0 Production on Wed Aug 24 07:46:29 2022

Copyright (c) 1982, 2011, Oracle.  All rights reserved.

Enter user-name: system
Enter password: 

Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production
```
- user-name : system
- password : oracle

<details>

<summary>fail</summary>

```shell
Enter user-name:  oracle_start
Enter password: 
ERROR:
ORA-01017: invalid username/password; logon denied
```

</details>

### [참고]

<details>

<summary>종료하기</summary>

```shell
$ exit
```
```shell
Disconnected from Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production
```

<detilas>