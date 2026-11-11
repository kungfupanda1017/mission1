모든 정보 확인 완료! 이제 README.md 작성할게요! 🎉

아래 내용을 복사해서 적용하세요:

---

**① 먼저 README.md 파일 열기:**
```bash
code ~/mission1/README.md
```

**② 아래 내용 전체 복사 후 붙여넣기:**

---

```markdown
# 미션1: 개발 워크스테이션 구축

## 📋 프로젝트 개요
WSL2 + Ubuntu 환경에서 Docker 및 Git 기반의  
개발 워크스테이션을 구축하는 미션입니다.

---

## 🛠️ 환경 정보

| 항목 | 버전 |
|------|------|
| OS | Ubuntu 26.04.1 LTS (Resolute Raccoon) |
| Docker | 29.9.2 |
| Git | 2.53.0 |
| 메모리 | 7.414GiB |
| Storage Driver | overlayfs |

---

## ✅ 완료 항목

### 1. WSL2 + Ubuntu 환경 구축
- Windows에 WSL2 설치 후 Ubuntu 22.04 구성

### 2. Docker 설치 및 검증
```bash
docker run hello-world
```

### 3. 커스텀 Docker 이미지 빌드
```bash
# Dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
```
```bash
docker build -t my-web-image .
```

### 4. 컨테이너 실행 및 웹 접속 확인
```bash
docker run -d -p 8080:80 --name my-web-container nginx
```
- 브라우저에서 `http://localhost:8080` 접속 확인 ✅

### 5. 바인드 마운트 실습
```bash
docker run -d -p 8080:80 \
  -v ~/mission1:/usr/share/nginx/html \
  --name my-web-container nginx
```
- 로컬 파일 수정 시 컨테이너에 실시간 반영 확인 ✅

### 6. Docker 볼륨 생성 및 영속성 검증
```bash
docker volume create my-vol
docker volume inspect my-vol
```
- 마운트 경로: `/var/lib/docker/volumes/my-vol/_data` ✅

### 7. 파일 권한 제어 실습 (chmod)
```bash
chmod 755 test.txt   # rwxr-xr-x
chmod 644 test.txt   # rw-r--r--
chmod 444 test.txt   # r--r--r--
```
- 최종 권한: `-rw-r--r--` (644) ✅

### 8. Git 설정 및 GitHub 연동
```bash
git config --global user.name "kungfupanda1017"
git config --global user.email "woopy2015@gmail.com"
ssh-keygen -t ed25519 -C "woopy2015@gmail.com"
```
- SSH Key 생성 후 GitHub 등록 완료 ✅

### 9. GitHub Push 완료
```bash
git init
git add .
git commit -m "feat: 미션1 개발 워크스테이션 구축 완료"
git push origin main
```
- 저장소: https://github.com/kungfupanda1017/mission1 ✅

---

## 🔧 트러블슈팅

### 문제 1: Git Push 실패 - Permission denied (publickey)

**증상**
```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
```

**원인**
- SSH Key를 생성했지만 GitHub에 공개키를 등록하지 않은 상태에서 push 시도

**해결 방법**
```bash
# 1. 공개키 내용 확인
cat ~/.ssh/id_ed25519.pub

# 2. GitHub → Settings → SSH and GPG keys
#    → New SSH key → 공개키 내용 붙여넣기

# 3. 연결 테스트
ssh -T git@github.com

# 4. 정상 응답 확인
# Hi kungfupanda1017! You've successfully authenticated.
```

---

### 문제 2: 포트 접속 실패 - localhost:8080 연결 안 됨

**증상**
- 브라우저에서 `http://localhost:8080` 접속 시 연결 거부

**원인**
- 컨테이너 실행 시 포트 매핑 옵션(`-p`)을 누락한 채 실행

**해결 방법**
```bash
# 1. 실행 중인 컨테이너 확인
docker ps

# 2. 포트 매핑 없이 실행된 컨테이너 중지 및 삭제
docker stop my-web-container
docker rm my-web-container

# 3. 포트 매핑 옵션 추가하여 재실행
docker run -d -p 8080:80 --name my-web-container nginx

# 4. 포트 매핑 확인
docker ps
# 0.0.0.0:8080->80/tcp 확인 ✅
```

---

## 📁 프로젝트 구조

```
mission1/
├── Dockerfile       # nginx:alpine 기반 커스텀 이미지
├── index.html       # 웹 페이지 (Hello, Docker!)
├── test.txt         # chmod 실습용 파일
└── README.md        # 프로젝트 문서
```

---

## 🐳 Docker 이미지 목록

| 이미지 | 용도 |
|--------|------|
| `my-web-image:latest` | 커스텀 Nginx 이미지 |
| `my-web-app:latest` | DockerHub 배포 이미지 |
| `nginx:latest` | 베이스 이미지 |
| `alpine:latest` | 경량 Linux 이미지 |

---

## 👤 작성자
- GitHub: [@kungfupanda1017](https://github.com/kungfupanda1017)
- 완료일: 2026년 11월 11일
```

---

**③ 저장 후 GitHub에 최종 Push:**
```bash
cd ~/mission1
git add README.md
git commit -m "docs: README.md 작성 완료"
git push origin main
