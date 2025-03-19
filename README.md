# 도커기반 스프링부트-리액트 기본 템플릿
> 1. 주의! 이 파일은 다운로드하여 시작하기위한 기본 템플릿입니다.
> 2. 이 파일을 git clone 받고 remote 위치를 새로운 레포지토리로 변경하고 사용해야합니다.

> **설정**
> 1. 기본설정 완료하였습니다.
> 2. backend와 frontend .gitignore 파일 각각 관리합니다.
> 3. mysql port 충돌문제로 3307로 변경돼있습니다. 참고바랍니다.
> 4. 템플릿 이용시 backend 삭제하고 인텔리제이로 열어서 backend생성해서 설치하기
> 5. backend/ 에 .env 설정파일 생성, Dockerfile 생성

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
command: 부분 추가해야 한글입력가능

> [세팅 참고 가이드](https://khdscor.tistory.com/116)
