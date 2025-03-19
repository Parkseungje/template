# 도커기반 스프링부트-리액트 기본 템플릿
> 1. 주의! 이 파일은 다운로드하여 시작하기위한 기본 템플릿입니다.
> 2. 이 파일을 git clone 받고 remote 위치를 새로운 레포지토리로 변경하고 사용해야합니다.

> **설정**
> 1. 기본설정 완료하였습니다.
> 2. backend와 frontend .gitignore 파일 각각 관리합니다.
> 3. mysql port 충돌문제로 3307로 변경돼있습니다. 참고바랍니다.
> 4. 템플릿 이용시 backend 삭제하고 인텔리제이로 열어서 backend생성해서 설치하기
> 5. backend/ 에 .env 설정파일 생성, Dockerfile 생성

> [세팅 참고 가이드](https://khdscor.tistory.com/116)

## 도커 mysql 한글입력 설정

**docker-compose.yaml 설정**
```
mysql:
     image: mysql:8.0.34
     networks:
       - khds_network
     volumes:
       - ./backend/db/conf.d:/etc/mysql/conf.d
       - ./backend/db/data:/var/lib/mysql
       - ./backend/db/initdb.d:/docker-entrypoint-initdb.d
     env_file: ./backend/.env
     command:
       - --character-set-server=utf8mb4
       - --collation-server=utf8mb4_unicode_ci
       - --skip-character-set-client-handshake
     ports:
       - "3307:3307"
     restart: always
```
command: 부분 추가해야 한글 인코딩

---

**mysql 이미지 locale 변경**

1. mysql 컨테이너에 bash로 접속
```
docker exec -it [컨테이너명] bash
```

2. vim 설치
```
microdnf install -y vim
```
3. ko_KR.UTF-8 Locale을 사용하기위해 설치
```
microdnf install -y langpacks-ko
```
4. 로케일 설치 확인 
```
locale -a
```
5. exit으로 나온다

6. backend/.env 변경
```
 TZ=Asia/Seoul
 MYSQL_HOST=localhost
 MYSQL_PORT=3307
 MYSQL_ROOT_PASSWORD=rootpassword
 MYSQL_DATABASE=uplog
 MYSQL_USER=mysqluser
 MYSQL_PASSWORD=mysqlpw
 LANG=C.UTF-8
 LC_ALL=C.UTF-8
```
이렇게
`LANG=C.UTF-8`
`LC_ALL=C.UTF-8`
추가한다.

7. 컨테이너 재시작
```
docker-compose up -d --force-recreate
```



