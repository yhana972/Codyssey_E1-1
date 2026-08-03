# Docker 실습 이미지

Notion 원문에서 실제로 촬영한 Docker 실습 이미지 73개를 실행 순서대로 매핑합니다. 미촬영 항목 `08`, `15`, `44`, `46`은 목록에서 제외했습니다.

## Docker 기본과 커스텀 이미지

| 번호 | 파일명 | 대응 로그 |
| ---: | --- | --- |
| 01 | `docker-01-version.png` | `docker --version` |
| 02 | `docker-02-info.png` | `docker info` |
| 03 | `docker-03-pull-image.png` | `hello-world` pull 및 image 목록 |
| 04 | `docker-04-hello-run.png` | `hello-world` 실행 |
| 05 | `docker-05-container-list.png` | `docker ps`, `docker ps -a` |
| 06 | `docker-06-logs-name-error.png` | 잘못된 Container 이름으로 logs 조회 |
| 07 | `docker-07-logs-success.png` | 올바른 Container logs 조회 |
| 09 | `docker-09-dockerfile.png` | Dockerfile 작성 결과 |
| 10 | `docker-10-image-build.png` | `docker build` |
| 11 | `docker-11-image-list.png` | 생성된 `codyssey-web` image 확인 |
| 12 | `docker-12-tag-error-fix.png` | `1.o` tag 오류와 재빌드 |
| 13 | `docker-13-web-container-run.png` | Nginx Container 실행 |
| 14 | `docker-14-http-response.png` | Host에서 HTTP 응답 확인 |

## Bind Mount와 Volume

| 번호 | 파일명 | 대응 로그 |
| ---: | --- | --- |
| 16 | `docker-16-bind-run.png` | Bind Mount Container 실행 |
| 17 | `docker-17-bind-status.png` | `bind-web` 상태 확인 |
| 18 | `docker-18-bind-before-404.png` | 파일 생성 전 `404` 확인 |
| 19 | `docker-19-bind-after-update.png` | Host 파일 변경 즉시 반영 |
| 20 | `docker-20-volume-create.png` | Volume 생성과 목록 확인 |
| 21 | `docker-21-volume-container-run.png` | Volume 연결 Container 실행 |
| 22 | `docker-22-volume-write-read.png` | Volume에 데이터 작성·조회 |
| 23 | `docker-23-volume-container-remove.png` | 첫 번째 Container 삭제 |
| 24 | `docker-24-volume-container-removed.png` | Container 삭제 결과 확인 |
| 25 | `docker-25-volume-exists.png` | Container 삭제 후 Volume 존재 확인 |
| 26 | `docker-26-volume-reconnect.png` | 새 Container에 Volume 재연결 |
| 27 | `docker-27-volume-persistence.png` | 새 Container에서 기존 데이터 확인 |
| 28 | `docker-28-volume-result-repeat.png` | 영속 데이터 재확인 |

## Ubuntu Container와 리소스

| 번호 | 파일명 | 대응 로그 |
| ---: | --- | --- |
| 29 | `docker-29-ubuntu-run.png` | Ubuntu 대화형 Container 실행 |
| 30 | `docker-30-ubuntu-exit-status.png` | PID 1 종료와 Container 상태 |
| 31 | `docker-31-ubuntu-attach.png` | Container 재시작과 `attach` |
| 32 | `docker-32-ubuntu-exec.png` | `docker exec -it` 새 Bash |
| 33 | `docker-33-ubuntu-attach-exit.png` | attach에서 exit 후 상태 |
| 34 | `docker-34-stats.png` | `docker stats` 리소스 확인 |

## Docker Compose 단일 서비스

| 번호 | 파일명 | 대응 로그 |
| ---: | --- | --- |
| 35 | `docker-35-compose-image.png` | 기존 custom image 확인 |
| 36 | `docker-36-single-compose-file.png` | 단일 service Compose 파일 |
| 37 | `docker-37-single-compose-config.png` | Compose 설정 검증 |
| 38 | `docker-38-single-compose-up.png` | 단일 service 실행 |
| 39 | `docker-39-single-compose-ps.png` | Compose service 상태 |
| 40 | `docker-40-single-docker-ps.png` | 일반 Docker 명령으로 상태 확인 |
| 41 | `docker-41-single-network.png` | Compose 기본 network |
| 42 | `docker-42-single-http.png` | 단일 service HTTP 응답 |
| 43 | `docker-43-single-logs.png` | Compose service log |
| 45 | `docker-45-single-down.png` | 단일 service 종료·삭제 |

## Docker Compose 멀티 서비스와 환경 변수

| 번호 | 파일명 | 대응 로그 |
| ---: | --- | --- |
| 47 | `docker-47-template-directory.png` | Nginx template 디렉터리 생성 |
| 48 | `docker-48-nginx-template.png` | Nginx 설정 template 작성 |
| 49 | `docker-49-env-file.png` | `.env` 작성 |
| 50 | `docker-50-env-example.png` | `.env.example` 작성 |
| 51 | `docker-51-gitignore-env.png` | `.env` Git 제외 확인 |
| 52 | `docker-52-multi-compose-file.png` | 멀티 service Compose 파일 |
| 53 | `docker-53-compose-environment.png` | Compose가 읽은 환경 변수 |
| 54 | `docker-54-multi-compose-config.png` | 최종 Compose 설정 검증 |
| 55 | `docker-55-compose-services.png` | service 목록 확인 |
| 56 | `docker-56-multi-compose-up.png` | 멀티 service 실행 |
| 57 | `docker-57-multi-compose-ps.png` | 멀티 service 상태 |
| 58 | `docker-58-multi-docker-ps.png` | 일반 Docker 명령으로 상태 확인 |
| 59 | `docker-59-multi-network.png` | Compose 기본 network 상세 |
| 60 | `docker-60-web-environment.png` | Web Container 환경 변수 |
| 61 | `docker-61-probe-environment.png` | Probe Container 환경 변수 |
| 62 | `docker-62-nginx-rendered-config.png` | 치환된 Nginx 설정 |
| 63 | `docker-63-host-http.png` | Host에서 Web 응답 확인 |
| 64 | `docker-64-service-dns.png` | `web` service DNS 조회 |
| 65 | `docker-65-interservice-http.png` | Probe에서 Web HTTP 요청 |
| 66 | `docker-66-multi-logs.png` | 멀티 service log |
| 67 | `docker-67-env-changed.png` | `.env` 값 변경 |
| 68 | `docker-68-changed-config.png` | 변경된 Compose 설정 검증 |
| 69 | `docker-69-force-recreate.png` | Container 강제 재생성 |
| 70 | `docker-70-changed-port-mapping.png` | 변경된 port mapping |
| 71 | `docker-71-old-port-failure.png` | 기존 Host port 접속 실패 |
| 72 | `docker-72-new-port-success.png` | 새 port와 production mode 응답 |
| 73 | `docker-73-changed-environment.png` | 변경된 Container 환경 변수 |
| 74 | `docker-74-interservice-after-change.png` | 변경 후 Container 간 통신 |
| 75 | `docker-75-multi-stats.png` | 멀티 Container 리소스 |
| 76 | `docker-76-multi-down.png` | 멀티 service 종료·삭제 |
| 77 | `docker-77-multi-cleanup.png` | Container·network 삭제 검증 |

등록된 73개 이미지는 README의 대표 캡처와 GitHub Wiki의 전체 실행 캡처 페이지에서 사용합니다.
