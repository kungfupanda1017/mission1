# Docker 미션 1 제출물

## 1. 프로젝트 개요
Nginx를 기반으로 한 간단한 웹 서버를 Docker 컨테이너로 실행하는 미션입니다.

## 2. 작업 과정
- **index.html 작성**: "Hello, Docker Mission 1" 내용을 담은 HTML 파일 생성
- **Dockerfile 작성**: nginx:latest 이미지를 기반으로 index.html을 복사하도록 설정
- **이미지 빌드**: `docker build -t my-web-app .` 명령 사용
- **컨테이너 실행**: `docker run -d -p 9000:80 my-web-app` 명령으로 9000번 포트 개방

## 3. Docker Hub 이미지 주소
- 이미지 링크: https://hub.docker.com/r/kungfupanda1017
/my-web-app

## 4. 실행 결과 (터미널 로그)
```
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
my-web-app    latest    a1b2c3d4e5f6   10 minutes ago  142MB

$ docker ps
CONTAINER ID   IMAGE        STATUS          PORTS                  NAMES
e7f8g9h0i1j2   my-web-app   Up 5 minutes    0.0.0.0:9000->80/tcp   web-server
```
