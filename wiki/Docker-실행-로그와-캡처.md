# Docker 실행 로그와 캡처

Docker 기본 동작부터 Docker Compose 멀티 서비스와 환경 변수 변경까지 실제 수행한 캡처 73개를 실행 순서대로 정리했습니다.

> 캡처하지 않은 원문 항목 08, 15, 44, 46은 제외했습니다. 명령어의 상세 설명은 [통합 학습 가이드](E1-1-개발환경-실습-가이드)를 참고하세요.

## Docker 기본과 커스텀 이미지

<details>
<summary><strong>캡처 보기</strong></summary>

### 01. `docker --version`

![`docker --version`](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-01-version.png)

### 02. `docker info`

![`docker info`](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-02-info.png)

### 03. `hello-world` pull 및 image 목록

![`hello-world` pull 및 image 목록](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-03-pull-image.png)

### 04. `hello-world` 실행

![`hello-world` 실행](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-04-hello-run.png)

### 05. `docker ps`, `docker ps -a`

![`docker ps`, `docker ps -a`](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-05-container-list.png)

### 06. 잘못된 Container 이름으로 logs 조회

![잘못된 Container 이름으로 logs 조회](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-06-logs-name-error.png)

### 07. 올바른 Container logs 조회

![올바른 Container logs 조회](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-07-logs-success.png)

### 09. Dockerfile 작성 결과

![Dockerfile 작성 결과](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-09-dockerfile.png)

### 10. `docker build`

![`docker build`](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-10-image-build.png)

### 11. 생성된 `codyssey-web` image 확인

![생성된 `codyssey-web` image 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-11-image-list.png)

### 12. `1.o` tag 오류와 재빌드

![`1.o` tag 오류와 재빌드](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-12-tag-error-fix.png)

### 13. Nginx Container 실행

![Nginx Container 실행](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-13-web-container-run.png)

### 14. Host에서 HTTP 응답 확인

![Host에서 HTTP 응답 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-14-http-response.png)

</details>

## Bind Mount와 Volume

<details>
<summary><strong>캡처 보기</strong></summary>

### 16. Bind Mount Container 실행

![Bind Mount Container 실행](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-16-bind-run.png)

### 17. `bind-web` 상태 확인

![`bind-web` 상태 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-17-bind-status.png)

### 18. 파일 생성 전 `404` 확인

![파일 생성 전 `404` 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-18-bind-before-404.png)

### 19. Host 파일 변경 즉시 반영

![Host 파일 변경 즉시 반영](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-19-bind-after-update.png)

### 20. Volume 생성과 목록 확인

![Volume 생성과 목록 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-20-volume-create.png)

### 21. Volume 연결 Container 실행

![Volume 연결 Container 실행](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-21-volume-container-run.png)

### 22. Volume에 데이터 작성·조회

![Volume에 데이터 작성·조회](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-22-volume-write-read.png)

### 23. 첫 번째 Container 삭제

![첫 번째 Container 삭제](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-23-volume-container-remove.png)

### 24. Container 삭제 결과 확인

![Container 삭제 결과 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-24-volume-container-removed.png)

### 25. Container 삭제 후 Volume 존재 확인

![Container 삭제 후 Volume 존재 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-25-volume-exists.png)

### 26. 새 Container에 Volume 재연결

![새 Container에 Volume 재연결](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-26-volume-reconnect.png)

### 27. 새 Container에서 기존 데이터 확인

![새 Container에서 기존 데이터 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-27-volume-persistence.png)

### 28. 영속 데이터 재확인

![영속 데이터 재확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-28-volume-result-repeat.png)

</details>

## Ubuntu Container와 리소스

<details>
<summary><strong>캡처 보기</strong></summary>

### 29. Ubuntu 대화형 Container 실행

![Ubuntu 대화형 Container 실행](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-29-ubuntu-run.png)

### 30. PID 1 종료와 Container 상태

![PID 1 종료와 Container 상태](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-30-ubuntu-exit-status.png)

### 31. Container 재시작과 `attach`

![Container 재시작과 `attach`](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-31-ubuntu-attach.png)

### 32. `docker exec -it` 새 Bash

![`docker exec -it` 새 Bash](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-32-ubuntu-exec.png)

### 33. attach에서 exit 후 상태

![attach에서 exit 후 상태](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-33-ubuntu-attach-exit.png)

### 34. `docker stats` 리소스 확인

![`docker stats` 리소스 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-34-stats.png)

</details>

## Docker Compose 단일 서비스

<details>
<summary><strong>캡처 보기</strong></summary>

### 35. 기존 custom image 확인

![기존 custom image 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-35-compose-image.png)

### 36. 단일 service Compose 파일

![단일 service Compose 파일](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-36-single-compose-file.png)

### 37. Compose 설정 검증

![Compose 설정 검증](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-37-single-compose-config.png)

### 38. 단일 service 실행

![단일 service 실행](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-38-single-compose-up.png)

### 39. Compose service 상태

![Compose service 상태](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-39-single-compose-ps.png)

### 40. 일반 Docker 명령으로 상태 확인

![일반 Docker 명령으로 상태 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-40-single-docker-ps.png)

### 41. Compose 기본 network

![Compose 기본 network](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-41-single-network.png)

### 42. 단일 service HTTP 응답

![단일 service HTTP 응답](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-42-single-http.png)

### 43. Compose service log

![Compose service log](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-43-single-logs.png)

### 45. 단일 service 종료·삭제

![단일 service 종료·삭제](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-45-single-down.png)

</details>

## Docker Compose 멀티 서비스와 환경 변수

<details>
<summary><strong>캡처 보기</strong></summary>

### 47. Nginx template 디렉터리 생성

![Nginx template 디렉터리 생성](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-47-template-directory.png)

### 48. Nginx 설정 template 작성

![Nginx 설정 template 작성](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-48-nginx-template.png)

### 49. `.env` 작성

![`.env` 작성](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-49-env-file.png)

### 50. `.env.example` 작성

![`.env.example` 작성](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-50-env-example.png)

### 51. `.env` Git 제외 확인

![`.env` Git 제외 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-51-gitignore-env.png)

### 52. 멀티 service Compose 파일

![멀티 service Compose 파일](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-52-multi-compose-file.png)

### 53. Compose가 읽은 환경 변수

![Compose가 읽은 환경 변수](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-53-compose-environment.png)

### 54. 최종 Compose 설정 검증

![최종 Compose 설정 검증](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-54-multi-compose-config.png)

### 55. service 목록 확인

![service 목록 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-55-compose-services.png)

### 56. 멀티 service 실행

![멀티 service 실행](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-56-multi-compose-up.png)

### 57. 멀티 service 상태

![멀티 service 상태](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-57-multi-compose-ps.png)

### 58. 일반 Docker 명령으로 상태 확인

![일반 Docker 명령으로 상태 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-58-multi-docker-ps.png)

### 59. Compose 기본 network 상세

![Compose 기본 network 상세](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-59-multi-network.png)

### 60. Web Container 환경 변수

![Web Container 환경 변수](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-60-web-environment.png)

### 61. Probe Container 환경 변수

![Probe Container 환경 변수](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-61-probe-environment.png)

### 62. 치환된 Nginx 설정

![치환된 Nginx 설정](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-62-nginx-rendered-config.png)

### 63. Host에서 Web 응답 확인

![Host에서 Web 응답 확인](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-63-host-http.png)

### 64. `web` service DNS 조회

![`web` service DNS 조회](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-64-service-dns.png)

### 65. Probe에서 Web HTTP 요청

![Probe에서 Web HTTP 요청](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-65-interservice-http.png)

### 66. 멀티 service log

![멀티 service log](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-66-multi-logs.png)

</details>

## 환경 변수 변경과 종료 검증

<details>
<summary><strong>캡처 보기</strong></summary>

### 67. `.env` 값 변경

![`.env` 값 변경](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-67-env-changed.png)

### 68. 변경된 Compose 설정 검증

![변경된 Compose 설정 검증](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-68-changed-config.png)

### 69. Container 강제 재생성

![Container 강제 재생성](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-69-force-recreate.png)

### 70. 변경된 port mapping

![변경된 port mapping](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-70-changed-port-mapping.png)

### 71. 기존 Host port 접속 실패

![기존 Host port 접속 실패](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-71-old-port-failure.png)

### 72. 새 port와 production mode 응답

![새 port와 production mode 응답](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-72-new-port-success.png)

### 73. 변경된 Container 환경 변수

![변경된 Container 환경 변수](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-73-changed-environment.png)

### 74. 변경 후 Container 간 통신

![변경 후 Container 간 통신](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-74-interservice-after-change.png)

### 75. 멀티 Container 리소스

![멀티 Container 리소스](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-75-multi-stats.png)

### 76. 멀티 service 종료·삭제

![멀티 service 종료·삭제](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-76-multi-down.png)

### 77. Container·network 삭제 검증

![Container·network 삭제 검증](https://raw.githubusercontent.com/yhana972/Codyssey_E1-1/main/docs/images/docker/docker-77-multi-cleanup.png)

</details>

## 관련 문서

- [통합 학습 가이드](E1-1-개발환경-실습-가이드)
- [Docker 이미지와 컨테이너](Docker-이미지와-컨테이너)
- [Docker 스토리지: Bind Mount와 Volume](Docker-스토리지-Bind-Mount와-Volume)
- [Docker Compose와 환경 변수](Docker-Compose와-환경-변수)
