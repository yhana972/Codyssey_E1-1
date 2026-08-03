# 실습 캡처 이미지 안내

README와 GitHub Wiki에서 사용하는 실습 이미지 저장 위치입니다. 아래 이름을 그대로 사용하면 문서의 이미지 링크를 별도로 수정하지 않아도 됩니다.

## 캡처 체크리스트

| 번호 | 파일명 | 캡처할 내용 | 필수 |
| ---: | --- | --- | :---: |
| 01 | `01-linux-cli.png` | `pwd`, `ls -al`, 파일·디렉터리 생성 결과 | ✅ |
| 02 | `02-linux-permission.png` | `chmod` 실행 전·후 권한 비교 | ✅ |
| 03 | `03-git-ssh.png` | `ssh -T`, `git remote -v`, push 성공 | ✅ |
| 04 | `04-docker-build.png` | `docker build` 성공과 생성된 image | ✅ |
| 05 | `05-docker-http.png` | `docker ps`와 `curl`의 `200 OK` | ✅ |
| 06 | `06-bind-mount.png` | Host 파일 수정 전·후 웹 반영 | ✅ |
| 07 | `07-volume-persistence.png` | Container 삭제·재생성 후 데이터 유지 | ✅ |
| 08 | `08-compose-ps.png` | `docker compose ps`의 서비스·포트 상태 | ✅ |
| 09 | `09-compose-network.png` | `nslookup web`과 `probe → web` 응답 | ✅ |
| 10 | `10-compose-env-change.png` | port와 `APP_MODE` 변경 전·후 | ✅ |
| 11 | `11-troubleshooting.png` | 대표 오류 메시지와 해결 후 결과 | 선택 |

## 캡처 기준

- 명령어와 결과가 같은 화면에 보이도록 캡처합니다.
- 터미널 글자가 읽히도록 불필요한 영역은 잘라냅니다.
- 이미지 폭은 약 `1200~1600px`, 형식은 `PNG`를 권장합니다.
- 이메일, token, SSH private key, 개인 경로 등 민감 정보는 반드시 가립니다.
- 같은 명령을 여러 번 캡처하기보다 검증 결과가 가장 명확한 화면을 선택합니다.

## 문서에 표시하기

이미지를 저장한 뒤 `README.md`에서 아래 형식의 주석을 찾습니다.

```markdown
<!-- ![설명](docs/images/01-linux-cli.png) -->
```

앞뒤의 주석 기호를 제거하면 이미지가 표시됩니다.

```markdown
![설명](docs/images/01-linux-cli.png)
```
