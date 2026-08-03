# E1-1. 개발자 작업 환경 구축

> Linux CLI, Git/GitHub, Docker, Docker Compose를 직접 구성하고 실행 결과를 검증한 실습 저장소입니다.

## 🖥️ 1. 실행 환경

| 항목 | 환경 / 버전 |
| --- | --- |
| OS | macOS Sequoia (`Darwin 24.6.0`) |
| Shell | zsh (`/bin/zsh`) |
| Docker Engine | `28.5.2` |
| Docker Compose | `2.40.3` |
| Git | `2.53.0` |
| Web image | `nginx:alpine` |

## 📋 2. 수행 항목 체크리스트

- [x] Linux 기본 명령어로 파일·디렉터리 생성, 복사, 이동, 삭제
- [x] 파일 및 디렉터리 권한 확인·변경 (`chmod`)
- [x] Git 초기 설정, 저장소 생성, GitHub 원격 저장소 연결
- [x] GitHub 인증 방식을 HTTPS에서 SSH로 전환
- [x] Docker 이미지 조회·다운로드 및 컨테이너 생명주기 실습
- [x] `Dockerfile` 기반 Nginx 커스텀 이미지 빌드
- [x] 포트 매핑과 HTTP 응답 검증
- [x] Bind Mount 실시간 반영 및 Volume 영속성 검증
- [x] Docker Compose 단일 서비스 실행·정리
- [x] Docker Compose 멀티 컨테이너 통신 및 서비스 디스커버리 검증
- [x] `.env` 변경 후 컨테이너 재생성과 설정 반영 검증

## 🧪 3. 수행 로그 및 검증 요약

> **이미지 첨부 방법:** 캡처 파일을 `docs/images/`에 권장 파일명으로 저장한 뒤, 각 위치의 `<!-- ![...](...) -->`에서 주석 기호만 제거합니다. 캡처에는 명령어와 검증 결과가 한 화면에 보이도록 구성하고 계정 이메일·SSH key·token은 가립니다.

### 3-1. Linux CLI와 권한

```bash
pwd
ls -al
touch new.txt && mkdir test
cp new.txt test/ && mv test/new.txt test/result.txt
chmod 700 Codyssey
chmod 777 Codyssey/new.txt
```

| 검증 대상 | 변경 전 | 변경 후 | 결과 |
| --- | --- | --- | --- |
| `Codyssey` 디렉터리 | `drwxr-xr-x` (`755`) | `drwx------` (`700`) | 소유자만 접근 가능 |
| `new.txt` 파일 | `-rw-r--r--` (`644`) | `-rwxrwxrwx` (`777`) | 권한 변경 확인 |

> 📸 **캡처 01 — 기본 명령어 실행:** `docs/images/01-linux-cli.png`
>
> 📸 **캡처 02 — 권한 변경 전·후:** `docs/images/02-linux-permission.png`

<!-- ![Linux 기본 명령어 실행](docs/images/01-linux-cli.png) -->
<!-- ![파일과 디렉터리 권한 변경 전후](docs/images/02-linux-permission.png) -->

[👉 상세 보기](../../wiki/Linux-CLI와-파일-권한)

### 3-2. Git과 GitHub 연결

```bash
git config --global user.name "<name>"
git config --global user.email "<email>"
git init
git remote add origin git@github.com:yhana972/Codyssey_E1-1.git
ssh -T git@github.com
git push -u origin main
```

**검증:** 원격 저장소의 fetch/push URL이 SSH 형식으로 설정되고 GitHub 인증 및 `main` push에 성공했습니다.

> 📸 **캡처 03 — GitHub SSH 연결:** `docs/images/03-git-ssh.png`
>
> `ssh -T`, `git remote -v`, push 성공 결과를 포함합니다.

<!-- ![GitHub SSH 인증과 원격 저장소 연결](docs/images/03-git-ssh.png) -->

[👉 상세 보기](../../wiki/Git과-GitHub-SSH)

### 3-3. Docker 기본 동작과 커스텀 이미지

```bash
docker version
docker run hello-world
docker build -t codyssey-web:1.0 ./docker-web
docker run -d --name codyssey-web -p 8080:80 codyssey-web:1.0
curl -i http://localhost:8080
```

**검증:** `codyssey-web:1.0` 이미지 빌드, Nginx 컨테이너 실행, `HTTP/1.1 200 OK` 응답을 확인했습니다.

> 📸 **캡처 04 — Image build:** `docs/images/04-docker-build.png`
>
> 📸 **캡처 05 — Container와 HTTP 응답:** `docs/images/05-docker-http.png`

<!-- ![Docker 커스텀 이미지 빌드](docs/images/04-docker-build.png) -->
<!-- ![Docker 컨테이너 상태와 HTTP 200 응답](docs/images/05-docker-http.png) -->

[👉 상세 보기](../../wiki/Docker-이미지와-컨테이너)

### 3-4. Bind Mount와 Volume 영속성

```bash
# 호스트 파일 변경을 컨테이너에 즉시 반영
docker run -d --name bind-web -p 8081:80 \
  --mount type=bind,source="$(pwd)/docker-web/app",target=/usr/share/nginx/html \
  codyssey-web:1.0

# Docker 관리 볼륨의 데이터 유지 검증
docker volume create codyssey-data
docker run -d --name volume-web-1 -p 8082:80 \
  --mount type=volume,source=codyssey-data,target=/usr/share/nginx/html/data \
  codyssey-web:1.0
```

**검증:** Bind Mount의 실시간 파일 반영과 컨테이너 삭제·재생성 후 `codyssey-data`의 데이터 유지를 확인했습니다.

> 📸 **캡처 06 — Bind Mount 반영:** `docs/images/06-bind-mount.png`
>
> 📸 **캡처 07 — Volume 영속성:** `docs/images/07-volume-persistence.png`

<!-- ![Bind Mount 실시간 변경 반영](docs/images/06-bind-mount.png) -->
<!-- ![컨테이너 재생성 후 Volume 데이터 유지](docs/images/07-volume-persistence.png) -->

[👉 상세 보기](../../wiki/Docker-스토리지-Bind-Mount와-Volume)

### 3-5. Docker Compose와 환경 변수

```bash
docker compose config --environment
docker compose config --services
docker compose up -d
docker compose ps
curl -i http://localhost:8083
docker compose exec probe nslookup web
docker compose exec probe wget -qO- "$WEB_URL"
docker compose down
```

| 검증 | 초기값 | 변경값 | 결과 |
| --- | --- | --- | --- |
| Host → Container 포트 | `8083 → 8080` | `8084 → 9090` | 새 포트 `200 OK`, 기존 포트 접속 실패 |
| `APP_MODE` | `development` | `production` | 응답 헤더와 컨테이너 환경 변수에 반영 |
| 서비스 간 통신 | `http://web:8080` | `http://web:9090` | `probe → web` 요청 성공 |

> 📸 **캡처 08 — Compose 실행 상태:** `docs/images/08-compose-ps.png`
>
> 📸 **캡처 09 — 서비스 간 통신:** `docs/images/09-compose-network.png`
>
> 📸 **캡처 10 — 환경 변수 변경 검증:** `docs/images/10-compose-env-change.png`

<!-- ![Docker Compose 서비스 실행 상태](docs/images/08-compose-ps.png) -->
<!-- ![Compose 서비스 디스커버리와 컨테이너 간 통신](docs/images/09-compose-network.png) -->
<!-- ![환경 변수 변경 전후 HTTP 응답](docs/images/10-compose-env-change.png) -->

<details>
<summary><strong>핵심 검증 로그 보기</strong></summary>

```text
web, probe: Up
HTTP/1.1 200 OK
X-App-Mode: development → production
WEB_URL=http://web:8080 → http://web:9090
docker compose down 후 컨테이너·기본 네트워크 제거 확인
```

</details>

[👉 상세 보기](../../wiki/Docker-Compose와-환경-변수)

## 🚨 4. 트러블슈팅 요약

| 문제 | 원인 | 해결 |
| --- | --- | --- |
| `pull access denied for codyssey-web` | 빌드 태그를 `1.o`로 오타 입력한 뒤 `1.0`으로 실행 | `docker images`로 태그를 확인하고 `codyssey-web:1.0`으로 재빌드·실행 |
| 컨테이너 로그 조회 실패 | 이미지 이름을 컨테이너 이름으로 사용 | `docker ps -a`의 `NAMES`를 확인하거나 `--name`으로 명시 |
| 기존 컨테이너에 Volume 추가 불가 | 컨테이너 생성 후 Mount/포트 설정은 변경 불가 | 기존 컨테이너를 중지하고 올바른 Mount 설정으로 새 컨테이너 생성 |
| `port is already allocated` | 두 컨테이너가 같은 Host port 점유 | Host port를 `8081`, `8082`처럼 분리 |
| 설정 변경 후 이전 포트가 계속 사용됨 | `.env` 변경값이 기존 컨테이너에 미반영 | `docker compose up -d --force-recreate`로 재생성 |

> 📸 **선택 캡처 11 — 오류와 해결 결과:** `docs/images/11-troubleshooting.png`

<!-- ![오류 메시지와 해결 후 정상 실행 결과](docs/images/11-troubleshooting.png) -->

[👉 전체 해결 과정](../../wiki/트러블슈팅)

## 📚 5. GitHub Wiki 안내

개념, 명령어 옵션, 전체 실행 절차와 트러블슈팅은 Wiki 원문에서 확인할 수 있습니다.

- [📖 통합 학습 가이드](../../wiki/E1-1-개발환경-실습-가이드)
- [Linux CLI와 파일 권한](../../wiki/Linux-CLI와-파일-권한)
- [Git과 GitHub SSH](../../wiki/Git과-GitHub-SSH)
- [Docker 이미지와 컨테이너](../../wiki/Docker-이미지와-컨테이너)
- [Docker 스토리지: Bind Mount와 Volume](../../wiki/Docker-스토리지-Bind-Mount와-Volume)
- [Docker Compose와 환경 변수](../../wiki/Docker-Compose와-환경-변수)
- [트러블슈팅](../../wiki/트러블슈팅)

> Wiki 게시용 원문: [`wiki/E1-1-개발환경-실습-가이드.md`](wiki/E1-1-개발환경-실습-가이드.md)
