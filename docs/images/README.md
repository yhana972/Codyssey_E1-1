# 실습 캡처 이미지 안내

README와 GitHub Wiki에서 사용하는 실습 이미지 저장 위치입니다. 아래 이름을 그대로 사용하면 문서의 이미지 링크를 별도로 수정하지 않아도 됩니다.

## Linux 터미널 캡처 체크리스트

| 번호 | 파일명 | 캡처할 내용 | 상태 |
| ---: | --- | --- | :---: |
| 01 | `terminal/terminal-01-pwd.png` | 현재 작업 경로 `pwd` | ✅ |
| 02 | `terminal/terminal-02-list-all.png` | `ls -a`, `ls -al` | ✅ |
| 03 | `terminal/terminal-03-touch-file.png` | `touch` 파일 생성 | ✅ |
| 04 | `terminal/terminal-04-mkdir.png` | `mkdir` 디렉터리 생성 | ✅ |
| 05 | `terminal/terminal-05-copy-file.png` | 파일 복사 | ✅ |
| 06 | `terminal/terminal-06-copy-directory.png` | 디렉터리 재귀 복사 | ✅ |
| 07 | `terminal/terminal-07-move-file.png` | 파일 이동 | ✅ |
| 08 | `terminal/terminal-08-move-directory.png` | 디렉터리 이동 | ✅ |
| 09 | `terminal/terminal-09-rename-file.png` | 파일 이름 변경 | ✅ |
| 10 | `terminal/terminal-10-rename-directory.png` | 디렉터리 이름 변경 | ✅ |
| 11 | `terminal/terminal-11-remove-file.png` | 파일 삭제 | ✅ |
| 12 | `terminal/terminal-12-remove-directory.png` | 디렉터리 재귀 삭제 | ✅ |
| 13 | `terminal/terminal-13-file-content.png` | 파일 생성·편집·내용 확인 | ✅ |
| 14 | `terminal/terminal-14-directory-permission.png` | 디렉터리 권한 `755 → 700` | ✅ |
| 15 | `terminal/terminal-15-file-permission.png` | 파일 권한 `644 → 777` | ✅ |
| 16 | `terminal/terminal-16-rm-recursive-reference.png` | `rm -r` 참고 자료 | 미촬영 |
| 17 | `terminal/terminal-17-permission-reference.png` | 파일 권한 표기 참고 자료 | 미촬영 |

## Git·Docker 캡처 체크리스트

| 파일명 | 캡처할 내용 | 필수 |
| --- | --- | :---: |
| `git/git-01-config-user.png` | Git 사용자 이름·이메일 설정 | ✅ |
| `git/git-02-config-list.png` | `git config --list` 결과 | ✅ |
| `git/git-03-initial-push.png` | 저장소 초기화와 최초 push | ✅ |
| `git/git-04-remote-https-to-ssh.png` | Remote URL 변경 전·후 | ✅ |
| `git/git-05-ssh-auth-success.png` | `ssh -T git@github.com` 인증 성공 | ✅ |
| `git/git-06-ssh-push-success.png` | SSH 방식 push 성공 | ✅ |
| `04-docker-build.png` | `docker build` 성공과 생성된 image | ✅ |
| `05-docker-http.png` | `docker ps`와 `curl`의 `200 OK` | ✅ |
| `06-bind-mount.png` | Host 파일 수정 전·후 웹 반영 | ✅ |
| `07-volume-persistence.png` | Container 삭제·재생성 후 데이터 유지 | ✅ |
| `08-compose-ps.png` | `docker compose ps`의 서비스·포트 상태 | ✅ |
| `09-compose-network.png` | `nslookup web`과 `probe → web` 응답 | ✅ |
| `10-compose-env-change.png` | port와 `APP_MODE` 변경 전·후 | ✅ |
| `11-troubleshooting.png` | 대표 오류 메시지와 해결 후 결과 | 선택 |

## 캡처 기준

- 명령어와 결과가 같은 화면에 보이도록 캡처합니다.
- 터미널 글자가 읽히도록 불필요한 영역은 잘라냅니다.
- 이미지 폭은 약 `1200~1600px`, 형식은 `PNG`를 권장합니다.
- 이메일, token, SSH private key, 개인 경로 등 민감 정보는 반드시 가립니다.
- 같은 명령을 여러 번 캡처하기보다 검증 결과가 가장 명확한 화면을 선택합니다.

## 문서에 표시하기

이미지를 저장한 뒤 `README.md`에서 아래 형식의 주석을 찾습니다.

```markdown
<!-- ![설명](docs/images/terminal/terminal-01-pwd.png) -->
```

앞뒤의 주석 기호를 제거하면 이미지가 표시됩니다.

```markdown
![설명](docs/images/terminal/terminal-01-pwd.png)
```
