## 가독성 체크 결과 📋

전체 검토했습니다. 수정 포인트 먼저 정리할게요.

---

## 발견된 문제점

| 위치 | 문제 | 수정 방향 |
|------|------|-----------|
| 5섹션 | 권한 원리 설명이 표 없이 날것으로 삽입됨 | 마크다운 표로 정리 |
| 9섹션 | 포트 매핑 원리/절대경로 설명이 커스텀 이미지 섹션 안에 섞임 | 10-1로 이동 |
| 10섹션 | 코드블록 닫힘(```) 누락 | 수정 |
| 10-1섹션 | 이미지vs컨테이너만 있고 나머지 원리 내용 없음 | 내용 보완 |
| 심층인터뷰 | 말로 준비하므로 전체 제거 | 삭제 |
| 전체 | 섹션 번호 체계 정리 필요 | 통일 |

---

## ✅ 최종 확정본 전체

```markdown
# Mission 1 - Docker & Git 실습

## 1. 프로젝트 개요
- **미션 목표**: Linux 터미널 조작, Docker 운영, Git/GitHub 연동을 실습하고
  그 과정을 기술 문서로 기록한다.
- **제출 저장소**: https://github.com/kungfupanda1017/mission1

---

## 2. 실행 환경

- **OS**: Ubuntu WSL2 (Linux 6.18.58.1-microsoft-standard-WSL2)
- **Docker**: 29.9.2
- **Git**: 2.53.0
- **Architecture**: x86_64 (64비트)

```bash
# Docker 버전 확인
$ docker --version

# Git 버전 확인
$ git --version
```

---

## 3. 수행 항목 체크리스트

| 항목 | 완료 여부 |
|------|----------|
| 터미널 기본 조작 | ✅ |
| 파일 권한 변경 | ✅ |
| Docker 설치 및 점검 | ✅ |
| Docker 기본 운영 명령 | ✅ |
| 컨테이너 실행 실습 | ✅ |
| 커스텀 이미지 제작 | ✅ |
| 포트 매핑 및 접속 | ✅ |
| Docker 볼륨 영속성 검증 | ✅ |
| Git 설정 및 GitHub 연동 | ✅ |

---

## 4. 터미널 조작 로그

### 현재 위치 확인
```bash
$ pwd
/home/lenovo/mission1
```

### 목록 확인 (숨김 파일 포함)
```bash
$ ls -al
total 32
drwxr-xr-x 3 lenovo lenovo 4096 ...
-rw-r--r-- 1 lenovo lenovo 1234 ... README.md
```

### 폴더 이동 / 생성 / 복사 / 삭제
```bash
# 폴더 생성
$ mkdir test_dir

# 파일 생성
$ touch test_file.txt

# 파일 복사
$ cp test_file.txt test_file_backup.txt

# 파일 이동/이름변경
$ mv test_file.txt renamed_file.txt

# 파일 내용 확인
$ cat renamed_file.txt

# 파일 삭제
$ rm renamed_file.txt

# 폴더 삭제
$ rm -r test_dir
```

---

## 5. 권한 실습

### 파일 권한 숫자 원리

권한은 **소유자 / 그룹 / 기타** 3자리로 구성되며
각 자리는 **읽기(4) + 쓰기(2) + 실행(1)** 의 합으로 표현한다.

| 숫자 | 권한 조합 | 기호 |
|------|-----------|------|
| 7 | 4+2+1 (읽기+쓰기+실행) | rwx |
| 5 | 4+0+1 (읽기+실행) | r-x |
| 4 | 4+0+0 (읽기만) | r-- |
| 0 | 없음 | --- |

```
chmod 755 = rwxr-xr-x
            ↑   ↑   ↑
          소유자 그룹 기타
          (7)  (5)  (5)

chmod 700 = rwx------
            ↑   ↑   ↑
          소유자만 모든 권한, 그룹/기타 접근 불가
```

### 파일 권한 변경 전/후 비교
```bash
# 변경 전 확인
$ ls -l test_file_backup.txt
-rw-r--r-- 1 lenovo lenovo 0 ... test_file_backup.txt

# 권한 변경 (실행 권한 추가)
$ chmod 755 test_file_backup.txt

# 변경 후 확인
$ ls -l test_file_backup.txt
-rwxr-xr-x 1 lenovo lenovo 0 ... test_file_backup.txt
```

### 디렉토리 권한 변경 전/후 비교
```bash
# 변경 전
$ ls -ld test_dir/
drwxr-xr-x 2 lenovo lenovo 4096 ... test_dir/

# 권한 변경
$ chmod 700 test_dir/

# 변경 후
$ ls -ld test_dir/
drwx------ 2 lenovo lenovo 4096 ... test_dir/
```

---

## 6. Docker 설치 및 기본 점검

```bash
# Docker 버전 확인
$ docker --version
Docker version 29.9.2

# Docker 데몬 동작 확인
$ docker info
Client: Docker Engine - Community
 Version: 27.x.x
 ...
Server:
 Containers: 2
  Running: 1
  ...
```

---

## 7. Docker 기본 운영 명령

### 이미지 목록 확인
```bash
$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
nginx         latest    xxxxxxxx       2 weeks ago    187MB
ubuntu        latest    xxxxxxxx       3 weeks ago    77.9MB
hello-world   latest    xxxxxxxx       ...            13.3kB
```

### 컨테이너 목록 확인
```bash
# 실행 중인 컨테이너
$ docker ps

# 전체 컨테이너 (종료 포함)
$ docker ps -a
CONTAINER ID   IMAGE         STATUS                    NAMES
xxxxxxxxxxxx   hello-world   Exited (0) 5 minutes ago  ...
```

### 로그 및 리소스 확인
```bash
# 로그 확인
$ docker logs [컨테이너명]

# 리소스 확인
$ docker stats --no-stream
```

---

## 8. 컨테이너 실행 실습

### hello-world 실행
```bash
$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

### ubuntu 컨테이너 실행 및 내부 진입
```bash
$ docker run -it ubuntu bash

root@xxxxxxxxxxxx:/# ls
bin  boot  dev  etc  home  lib  ...

root@xxxxxxxxxxxx:/# echo "Hello from container"
Hello from container
```

### attach vs exec 차이 정리

| 구분 | 명령어 | 특징 |
|------|--------|------|
| attach | `docker attach [컨테이너명]` | 기존 프로세스에 연결, exit 시 컨테이너 종료 |
| exec | `docker exec -it [컨테이너명] bash` | 새 프로세스 실행, exit 해도 컨테이너 유지 |

---

## 9. 커스텀 이미지 제작

### 선택 방식: NGINX 베이스 + 정적 콘텐츠 교체

### Dockerfile
```dockerfile
FROM nginx:latest

# 커스텀 HTML 페이지 복사
COPY index.html /usr/share/nginx/html/index.html

# 포트 노출
EXPOSE 80
```

### 커스텀 포인트 목적

| 항목 | 목적 |
|------|------|
| `FROM nginx:latest` | 검증된 웹서버 베이스 이미지 사용 |
| `COPY index.html` | 나만의 페이지로 콘텐츠 교체 |
| `EXPOSE 80` | 외부 접속 포트 명시 |

### 빌드 및 실행
```bash
# 이미지 빌드
$ docker build -t my-web-image .
Successfully built xxxxxxxx
Successfully tagged my-web-image:latest

# 컨테이너 실행 (포트 매핑)
$ docker run -d -p 8080:80 --name my-web my-web-image
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### 접속 확인
```bash
$ curl http://localhost:8080
<!DOCTYPE html>
<html>
  <body>
    <h1>Hello from my Docker container!</h1>
  </body>
</html>
```
> ![접속 화면](스크린샷%202026-11-11%20124054.png)

---

## 10. 포트 매핑 실습

### 포트 매핑 원리

컨테이너는 독립된 네트워크 공간에서 실행되므로
외부(호스트)에서 직접 접속할 수 없다.
`-p 호스트포트:컨테이너포트` 옵션으로 연결 통로를 열어줘야 한다.

```
외부 브라우저
    ↓
호스트 포트 (8080)
    ↓  ← -p 8080:80 으로 연결
컨테이너 내부 포트 (80)
    ↓
NGINX 웹서버
```

| 옵션 예시 | 의미 |
|-----------|------|
| `-p 8080:80` | 호스트 8080 → 컨테이너 80 으로 연결 |
| `-p 8081:80` | 호스트 8081 → 컨테이너 80 으로 연결 |

> 컨테이너 내부 포트(80)는 같아도
> 호스트 포트(8080, 8081)를 다르게 하면 동시에 실행 가능하다.

### 동일 이미지 다중 포트 실습

**목표:** 같은 이미지를 두 포트에 배포하여 동일한 결과 확인

| 단계 | 명령어 | 설명 |
|------|--------|------|
| 1 | `docker stop nginx-test2` | 기존 컨테이너 중지 |
| 2 | `docker rm nginx-test2` | 기존 컨테이너 삭제 |
| 3 | `docker run -d -p 8081:80 --name nginx-test2 my-web-image:latest` | 동일 이미지로 재실행 |

#### 실행 결과

| 접속 주소 | 사용 이미지 | 출력 내용 |
|-----------|-------------|-----------|
| localhost:8080 | my-web-image:latest | Hello from my Docker container! |
| localhost:8081 | my-web-image:latest | Hello from my Docker container! |

---

## 11. Docker 볼륨 영속성 검증

```bash
# 볼륨 생성
$ docker volume create my-volume
my-volume

# 볼륨 연결하여 컨테이너 실행 + 데이터 저장
$ docker run -it --rm -v my-volume:/data ubuntu bash
root@xxxx:/# echo "볼륨 테스트 데이터" > /data/test.txt
root@xxxx:/# exit

# 컨테이너 삭제 후 새 컨테이너에서 데이터 확인
$ docker run -it --rm -v my-volume:/data ubuntu bash
root@xxxx:/# cat /data/test.txt
볼륨 테스트 데이터   ← 데이터 유지 확인! ✅
```

---

## 12. 핵심 기술 원리

### 이미지 vs 컨테이너

| 구분 | 역할 | 특징 |
|------|------|------|
| 이미지 | 설계도 | 읽기 전용, 변경 불가 |
| 컨테이너 | 설계도로 만든 실제 제품 | 실행 가능, 삭제 가능 |

- 하나의 이미지로 컨테이너를 여러 개 실행할 수 있다
- 컨테이너를 삭제해도 이미지는 그대로 남는다
- 이미지를 수정하려면 `docker build`로 새로 빌드해야 한다

```
이미지   =  붕어빵 틀 (설계도)
컨테이너 =  붕어빵    (실제 제품)

틀 하나로 붕어빵 여러 개 생산 가능 → 동일 이미지로 다중 컨테이너 실행
붕어빵을 먹어도 틀은 그대로      → 컨테이너 삭제해도 이미지 유지
```

### 절대경로 vs 상대경로

| 구분 | 형태 | 특징 |
|------|------|------|
| 절대경로 | `/home/lenovo/mission1` | 어디서 실행해도 항상 같은 위치 |
| 상대경로 | `./mission1` 또는 `../` | 현재 위치 기준으로 이동 |

```bash
# 절대경로 사용 예시 (현재 위치와 무관하게 동작)
$ cd /home/lenovo/mission
markdown
📋 복사
# 절대경로 사용 예시 (현재 위치와 무관하게 동작)
$ cd /home/lenovo/mission1

# 상대경로 사용 예시 (현재 위치가 /home/lenovo 일 때)
$ cd mission1
스크립트나 Dockerfile 작성 시에는
절대경로를 사용하는 것이 오류를 줄일 수 있다.

13. Git 설정 및 GitHub 연동
Git 사용자 정보 설정
bash
📋 복사
$ git config --global user.name "kungfupanda1017"
$ git config --global user.email "your-email@example.com"
$ git config --global init.defaultBranch main
Git 설정 확인
bash
📋 복사
$ git config --list
user.name=kung*********
user.email=woopy****@*mail.com
init.defaultbranch=main
...
GitHub 연동 및 푸시 증거
bash
📋 복사
$ git remote -v
origin  https://github.com/kungfupanda1017/mission1.git (fetch)
origin  https://github.com/kungfupanda1017/mission1.git (push)

$ git push origin main
...
To github.com:kungfupanda1017/mission1.git
   bbefe65..fc92b97  main -> main   ✅
14. 검증 방법 요약
항목	검증 명령	결과 위치
터미널 조작	pwd, ls -al, mkdir 등	4섹션 참고
파일 권한	ls -l, chmod	5섹션 참고
Docker 설치	docker --version, docker info	6섹션 참고
이미지/컨테이너	docker images, docker ps -a	7섹션 참고
컨테이너 실행	docker run hello-world	8섹션 참고
커스텀 이미지	docker build, curl	9섹션 참고
포트 매핑	docker run -p, curl	10섹션 참고
볼륨 영속성	docker volume create, cat	11섹션 참고
Git/GitHub	git config --list, git push	13섹션 참고
📁 프로젝트 구조
code
📋 복사
mission1/
├── Dockerfile       # nginx:latest 기반 커스텀 이미지
├── index.html       # 웹 페이지 (Hello from my Docker container!)
├── test.txt         # chmod 실습용 파일
└── README.md        # 프로젝트 문서
🐳 Docker 이미지 목록
이미지	용도
my-web-image:latest	커스텀 Nginx 이미지
nginx:latest	베이스 이미지
ubuntu:latest	컨테이너 실행 실습용
hello-world:latest	Docker 설치 확인용
⚠️ 보안 주의: 토큰, 비밀번호, 개인키는 이 문서에 포함하지 않습니다.