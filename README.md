# 🛠️ E1-1: 내 컴퓨터에 개발자용 '작업실' 꾸미기

> **목표:** Linux 터미널 조작부터 파일 권한 관리, Docker 핵심 실습(Dockerfile, 포트 매핑, 바인드 마운트, 볼륨 영속성) 및 Git/GitHub 연동까지 핵심 개발 환경 구축 과정을 직접 실습하고 기록합니다.

---

## 🖥️ 실행 환경 (Environment)

현재 프로젝트가 진행되는 개발 환경 정보입니다.

| 항목 (Category) | 사양 / 버전 (Specification / Version) |
| :--- | :--- |
| **OS** | macOS Sequoia (Darwin Kernel v24.6.0) |
| **Shell** | zsh (`/bin/zsh`) |
| **Docker Engine** | `v28.5.2` |
| **Docker Compose** | `v2.40.3` |
| **Git** | `v2.53.0` |

---

## 📋 수행 항목 체크리스트 (Tasks Checklist)

### 1. 🐧 리눅스 & 터미널 기초 (Linux & Terminal)
- [x] 터미널 기본 명령어 조작 (`cd`, `ls`, `mkdir`, `pwd` 등)
- [x] 파일 및 디렉토리 권한 설정 (`chmod`, `chown`)

### 2. 🐳 Docker 기본 & 컨테이너 운용 (Docker Fundamentals)
- [ ] Docker 설치 상태 및 런타임 환경 점검
- [ ] Docker 이미지 검색, 다운로드 및 관리 (`docker pull`, `docker images`)
- [ ] Docker 컨테이너 생성, 실행 및 삭제 (`docker run`, `docker rm`)
- [ ] `hello-world` 테스트 컨테이너 실행 및 검증
- [ ] `Ubuntu` 컨테이너 내부 대화형(Interactive) 실습 (`docker exec` / `-it`)

### 3. 🏗️ 커스텀 이미지 & 볼륨 관리 (Dockerfile & Data Management)
- [ ] `Dockerfile` 작성 (기본 인프라 정의)
- [ ] 커스텀 Docker 이미지 빌드 (`docker build -t ...`)
- [ ] 호스트-컨테이너 간 포트 매핑 (`-p host:container`)
- [ ] 바인드 마운트(Bind Mount)를 활용한 실시간 코드 동기화
- [ ] Docker 볼륨(Volume)을 활용한 데이터 영속성(Persistence) 확보

### 4. 🐙 버전 관리 & 보안 (Git & Security)
- [ ] Git 로컬 사용자 설정 (`git config user.name / email`)
- [ ] GitHub 리포지토리 연동 (`git remote add origin`)
- [ ] 보안 점검 (민감 정보 `.gitignore` 처리 및 환경 변수 분리)

---

## 🌟 선택 과제 (Bonus Tasks)

- [ ] **Docker Compose 단일 서비스**: `docker-compose.yml`을 활용한 컨테이너 오케스트레이션
- [ ] **Docker Compose 멀티 컨테이너**: Web + DB 등 다중 서비스 연동 환경 구축
- [ ] **환경 변수 활용**: `.env` 파일을 통한 구성 정보 동적 주입
- [ ] **GitHub SSH 연결**: SSH Key 생성 및 GitHub 계정 보안 인증 등록

---
# ✅ 수행 결과 및 검증

## 1. 🐧 리눅스 & 터미널 기초
<details>
<summary><strong>1-1. 현재 작업 경로 확인</strong></summary>

현재 터미널에서 작업 중인 디렉토리의 절대 경로를 확인했습니다.

`pwd`는 **Print Working Directory**의 약자로, 현재 작업 중인 디렉토리의 경로를 출력하는 명령어입니다.

```bash
yhana9728258@c4r5s1 ~ % pwd
/Users/yhana9728258
```

현재 작업 위치가 사용자 홈 디렉토리인 `/Users/yhana9728258`임을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-2. 파일 및 디렉토리 목록 확인</strong></summary>

현재 디렉토리에 존재하는 파일과 디렉토리 목록을 확인했습니다.

`ls`는 현재 디렉토리의 파일과 디렉토리 목록을 출력하는 명령어입니다.

- `-a`: 숨김 파일을 포함한 모든 항목 출력
- `-l`: 권한, 소유자, 파일 크기, 수정 시간 등 상세 정보 출력
- `-al`: 숨김 파일을 포함하여 상세 정보 출력

```bash
yhana9728258@c4r5s1 ~ % ls -a
.			.Trash			Downloads
..			.vscode			Library
.CFUserTextEncoding	.zsh_history		Movies
.DS_Store		.zsh_sessions		Music
.gitconfig		Desktop			Pictures
.lesshst		Documents		Public
```

`ls -a` 명령어를 실행하여 `.gitconfig`, `.zsh_history`, `.vscode`와 같은 숨김 파일과 디렉토리를 확인했습니다.

```bash
yhana9728258@c4r5s1 ~ % ls -al
total 48
drwxr-x---+ 18 yhana9728258  yhana9728258   576  7 28 21:18 .
drwxr-xr-x   8 root          admin          256  7 28 18:52 ..
-r--------   1 yhana9728258  yhana9728258     8  7 28 18:59 .CFUserTextEncoding
-rw-r--r--@  1 yhana9728258  yhana9728258  6148  7 28 21:25 .DS_Store
-rw-r--r--   1 yhana9728258  yhana9728258    49  7 28 21:11 .gitconfig
-rw-------   1 yhana9728258  yhana9728258    20  7 28 21:11 .lesshst
drwx------+  2 yhana9728258  yhana9728258    64  7 28 18:53 .Trash
drwxr-xr-x   3 yhana9728258  yhana9728258    96  7 28 18:53 .vscode
-rw-------   1 yhana9728258  yhana9728258    28  7 28 19:37 .zsh_history
drwx------   6 yhana9728258  yhana9728258   192  7 28 20:55 .zsh_sessions
drwx------+  5 yhana9728258  yhana9728258   160  7 28 21:25 Desktop
drwx------+  3 yhana9728258  yhana9728258    96  7 28 18:52 Documents
drwx------+  5 yhana9728258  yhana9728258   160  7 28 20:22 Downloads
drwx------@ 80 yhana9728258  yhana9728258  2560  7 28 19:56 Library
drwx------   3 yhana9728258  yhana9728258    96  7 28 18:52 Movies
drwx------+  3 yhana9728258  yhana9728258    96  7 28 18:52 Music
drwx------+  4 yhana9728258  yhana9728258   128  7 28 18:53 Pictures
drwxr-xr-x+  4 yhana9728258  yhana9728258   128  7 28 18:52 Public
```

`ls -al` 명령어를 실행하여 파일 종류, 권한, 소유자, 그룹, 크기 및 수정 시간을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-3. 파일 생성</strong></summary>

빈 파일을 생성하기 위해 `touch` 명령어를 사용했습니다.

`touch`는 지정한 파일이 존재하지 않으면 빈 파일을 생성합니다.

```bash
yhana9728258@c4r5s1 ~ % touch test.txt
yhana9728258@c4r5s1 ~ % ls -a
.			.vscode			Movies
..			.zsh_history		Music
.CFUserTextEncoding	.zsh_sessions		Pictures
.DS_Store		Desktop			Public
.gitconfig		Documents		test.txt
.lesshst		Downloads
.Trash			Library
```

`touch test.txt` 명령어를 실행한 후 `test.txt` 파일이 생성된 것을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-4. 디렉토리 생성</strong></summary>

새로운 디렉토리를 생성하기 위해 `mkdir` 명령어를 사용했습니다.

`mkdir`는 **Make Directory**의 약자로, 지정한 이름의 디렉토리를 생성합니다.

```bash
yhana9728258@c4r5s1 ~ % mkdir test
yhana9728258@c4r5s1 ~ % ls
Desktop		Downloads	Movies		Pictures	test
Documents	Library		Music		Public		test.txt
```

`mkdir test` 명령어를 실행한 후 `test` 디렉토리가 생성된 것을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-5. 디렉토리 복사</strong></summary>

디렉토리를 복사하기 위해 `cp` 명령어와 `-r` 옵션을 사용했습니다.

`-r` 옵션은 디렉토리 내부의 파일과 하위 디렉토리를 포함하여 재귀적으로 복사합니다.

```bash
yhana9728258@c4r5s1 ~ % ls
Desktop		Downloads	Movies		Pictures	test
Documents	Library		Music		Public		test.txt

yhana9728258@c4r5s1 ~ % cp -r test cp_test

yhana9728258@c4r5s1 ~ % ls
cp_test		Downloads	Music		test
Desktop		Library		Pictures	test.txt
Documents	Movies		Public
```

`test` 디렉토리를 `cp_test`라는 이름으로 복사했습니다.

실행 후 원본 디렉토리인 `test`와 복사한 디렉토리인 `cp_test`가 모두 존재하는 것을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-6. 파일 복사</strong></summary>

파일을 복사하기 위해 `cp` 명령어를 사용했습니다.

```bash
yhana9728258@c4r5s1 ~ % ls
cp_test		Downloads	Music		test
Desktop		Library		Pictures	test.txt
Documents	Movies		Public

yhana9728258@c4r5s1 ~ % cp test.txt cp_test.txt

yhana9728258@c4r5s1 ~ % ls
cp_test		Documents	Movies		Public
cp_test.txt	Downloads	Music		test
Desktop		Library		Pictures	test.txt
```

`test.txt` 파일을 `cp_test.txt`라는 이름으로 복사했습니다.

실행 후 원본 파일인 `test.txt`와 복사한 파일인 `cp_test.txt`가 모두 존재하는 것을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-7. 파일 이동</strong></summary>

파일을 다른 디렉토리로 이동하기 위해 `mv` 명령어를 사용했습니다.

`mv`는 **Move**의 약자로, 파일과 디렉토리를 이동하거나 이름을 변경할 때 사용합니다.

```bash
yhana9728258@c4r5s1 ~ % ls
cp_test		Documents	Movies		Public
cp_test.txt	Downloads	Music		test
Desktop		Library		Pictures	test.txt

yhana9728258@c4r5s1 ~ % mv cp_test.txt cp_test

yhana9728258@c4r5s1 ~ % ls
cp_test		Downloads	Music		test
Desktop		Library		Pictures	test.txt
Documents	Movies		Public

yhana9728258@c4r5s1 ~ % cd cp_test
yhana9728258@c4r5s1 cp_test % ls
cp_test.txt
```

현재 디렉토리에 있던 `cp_test.txt` 파일을 `cp_test` 디렉토리 내부로 이동했습니다.

이동 후 `cp_test` 디렉토리로 들어가 파일이 정상적으로 이동된 것을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-8. 디렉토리 이동</strong></summary>

디렉토리를 다른 디렉토리 내부로 이동하기 위해 `mv` 명령어를 사용했습니다.

```bash
yhana9728258@c4r5s1 ~ % ls
cp_test		Downloads	Music		test
Desktop		Library		Pictures	test.txt
Documents	Movies		Public

yhana9728258@c4r5s1 ~ % mv cp_test ./test

yhana9728258@c4r5s1 ~ % ls
Desktop		Downloads	Movies		Pictures	test
Documents	Library		Music		Public		test.txt

yhana9728258@c4r5s1 ~ % cd test
yhana9728258@c4r5s1 test % ls
cp_test
```

`cp_test` 디렉토리를 `test` 디렉토리 내부로 이동했습니다.

이동 후 `test` 디렉토리 안에 `cp_test` 디렉토리가 존재하는 것을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-9. 파일 이름 변경</strong></summary>

`mv` 명령어를 사용하여 파일 이름을 변경했습니다.

```bash
yhana9728258@c4r5s1 ~ % ls
Desktop		Downloads	Movies		Pictures	test
Documents	Library		Music		Public		test.txt

yhana9728258@c4r5s1 ~ % mv test.txt change_name_test.txt

yhana9728258@c4r5s1 ~ % ls
change_name_test.txt	Library			Public
Desktop			Movies			test
Documents		Music
Downloads		Pictures
```

`test.txt` 파일의 이름을 `change_name_test.txt`로 변경했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-10. 디렉토리 이름 변경</strong></summary>

`mv` 명령어를 사용하여 디렉토리 이름을 변경했습니다.

```bash
yhana9728258@c4r5s1 ~ % ls
change_name_test.txt	Library			Public
Desktop			Movies			test
Documents		Music
Downloads		Pictures

yhana9728258@c4r5s1 ~ % mv test change_name_folder_test

yhana9728258@c4r5s1 ~ % ls
change_name_folder_test	Downloads		Pictures
change_name_test.txt	Library			Public
Desktop			Movies
Documents		Music
```

`test` 디렉토리의 이름을 `change_name_folder_test`로 변경했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-11. 파일 삭제</strong></summary>

파일을 삭제하기 위해 `rm` 명령어를 사용했습니다.

`rm`은 **Remove**의 약자로, 지정한 파일을 삭제합니다.

```bash
yhana9728258@c4r5s1 ~ % ls
change_name_folder_test	Downloads		Pictures
change_name_test.txt	Library			Public
Desktop			Movies
Documents		Music

yhana9728258@c4r5s1 ~ % rm change_name_test.txt

yhana9728258@c4r5s1 ~ % ls
change_name_folder_test	Downloads		Music
Desktop			Library			Pictures
Documents		Movies			Public
```

`change_name_test.txt` 파일을 삭제한 후 목록에서 파일이 사라진 것을 확인했습니다.

> `rm`으로 삭제한 파일은 일반적으로 휴지통으로 이동하지 않고 즉시 삭제되므로 사용 시 주의해야 합니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-12. 디렉토리 삭제</strong></summary>

디렉토리와 내부 파일을 삭제하기 위해 `rm -r` 명령어를 사용했습니다.

`-r` 옵션은 디렉토리 내부의 파일과 하위 디렉토리를 재귀적으로 삭제합니다.

```bash
yhana9728258@c4r5s1 ~ % ls
change_name_folder_test	Downloads		Music
Desktop			Library			Pictures
Documents		Movies			Public

yhana9728258@c4r5s1 ~ % rm -r change_name_folder_test

yhana9728258@c4r5s1 ~ % ls
Desktop		Downloads	Movies		Pictures
Documents	Library		Music		Public
```

`change_name_folder_test` 디렉토리와 내부 항목이 모두 삭제된 것을 확인했습니다.

> `rm -r`은 디렉토리 내부의 파일도 함께 삭제하므로 실행 전에 삭제할 경로를 반드시 확인해야 합니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-13. 파일 내용 확인 및 편집</strong></summary>

빈 파일을 생성하고 파일 내용을 확인한 후, `vim` 편집기를 사용하여 내용을 작성했습니다.

- `touch`: 빈 파일 생성
- `cat`: 파일 내용 출력
- `vim`: 터미널 기반 파일 편집기 실행

```bash
yhana9728258@c4r5s1 Codyssey % touch new.txt
yhana9728258@c4r5s1 Codyssey % ls
new.txt

yhana9728258@c4r5s1 Codyssey % cat new.txt

yhana9728258@c4r5s1 Codyssey % vim new.txt

yhana9728258@c4r5s1 Codyssey % ls
new.txt

yhana9728258@c4r5s1 Codyssey % cat new.txt
Hi, My name is NaHyeon!
```

처음 생성한 `new.txt`는 빈 파일이므로 `cat new.txt`를 실행했을 때 출력되는 내용이 없었습니다.

이후 `vim new.txt` 명령어를 사용하여 내용을 작성하고 저장했습니다.

다시 `cat new.txt`를 실행하여 다음 문장이 저장된 것을 확인했습니다.

```text
Hi, My name is NaHyeon!
```

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-14. 경로 이동</strong></summary>

터미널의 현재 작업 위치를 변경하기 위해 `cd` 명령어를 사용했습니다.

`cd`는 **Change Directory**의 약자로, 지정한 디렉토리로 현재 작업 위치를 이동합니다.

```bash
yhana9728258@c4r5s1 ~ % cd cp_test
yhana9728258@c4r5s1 cp_test % ls
cp_test.txt
```

`cd cp_test` 명령어를 실행하여 현재 작업 위치를 `cp_test` 디렉토리로 이동했습니다.

터미널 프롬프트가 `~`에서 `cp_test`로 변경된 것을 통해 현재 위치가 변경된 것을 확인했습니다.

자주 사용하는 경로 이동 명령어는 다음과 같습니다.

| 명령어 | 설명 |
| :--- | :--- |
| `cd 디렉토리명` | 지정한 디렉토리로 이동 |
| `cd ..` | 상위 디렉토리로 이동 |
| `cd ~` | 사용자 홈 디렉토리로 이동 |
| `cd -` | 바로 이전에 작업하던 디렉토리로 이동 |
| `cd /` | 파일 시스템의 최상위 디렉토리로 이동 |

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-15. 디렉토리 권한 확인 및 변경</strong></summary>

디렉토리의 기존 권한을 확인하고 `chmod` 명령어를 사용하여 권한을 변경했습니다.

`chmod`는 **Change Mode**의 약자로, 파일이나 디렉토리의 접근 권한을 변경하는 명령어입니다.

권한은 다음과 같이 표시됩니다.

| 권한 | 의미 | 숫자 |
| :---: | :--- | :---: |
| `r` | 읽기 권한 | 4 |
| `w` | 쓰기 권한 | 2 |
| `x` | 실행 또는 디렉토리 접근 권한 | 1 |
| `-` | 권한 없음 | 0 |

권한은 다음 사용자 범주 순서로 표시됩니다.

```text
소유자(User) / 그룹(Group) / 기타 사용자(Others)
```

#### 권한 변경 전

```bash
yhana9728258@c4r5s1 ~ % ls -l
total 0
drwxr-xr-x   3 yhana9728258  yhana9728258    96  7 28 22:36 Codyssey
drwx------+  4 yhana9728258  yhana9728258   128  7 28 22:37 Desktop
drwx------+  3 yhana9728258  yhana9728258    96  7 28 18:52 Documents
drwx------+  5 yhana9728258  yhana9728258   160  7 28 20:22 Downloads
drwx------@ 81 yhana9728258  yhana9728258  2592  7 28 21:53 Library
drwx------   3 yhana9728258  yhana9728258    96  7 28 18:52 Movies
drwx------+  3 yhana9728258  yhana9728258    96  7 28 18:52 Music
drwx------+  4 yhana9728258  yhana9728258   128  7 28 18:53 Pictures
drwxr-xr-x+  4 yhana9728258  yhana9728258   128  7 28 18:52 Public
```

변경 전 `Codyssey` 디렉토리의 권한은 다음과 같습니다.

```text
drwxr-xr-x
```

이를 숫자로 표현하면 `755`입니다.

- 소유자: `rwx` → 읽기, 쓰기, 접근 가능
- 그룹: `r-x` → 읽기, 접근 가능
- 기타 사용자: `r-x` → 읽기, 접근 가능

#### 권한 변경

```bash
yhana9728258@c4r5s1 ~ % chmod 700 Codyssey
```

`chmod 700 Codyssey` 명령어를 실행하여 소유자만 디렉토리를 읽고, 수정하고, 접근할 수 있도록 변경했습니다.

#### 권한 변경 후

```bash
yhana9728258@c4r5s1 ~ % ls -l
total 0
drwx------   3 yhana9728258  yhana9728258    96  7 28 22:36 Codyssey
drwx------+  4 yhana9728258  yhana9728258   128  7 28 22:37 Desktop
drwx------+  3 yhana9728258  yhana9728258    96  7 28 18:52 Documents
drwx------+  5 yhana9728258  yhana9728258   160  7 28 20:22 Downloads
drwx------@ 81 yhana9728258  yhana9728258  2592  7 28 21:53 Library
drwx------   3 yhana9728258  yhana9728258    96  7 28 18:52 Movies
drwx------+  3 yhana9728258  yhana9728258    96  7 28 18:52 Music
drwx------+  4 yhana9728258  yhana9728258   128  7 28 18:53 Pictures
drwxr-xr-x+  4 yhana9728258  yhana9728258   128  7 28 18:52 Public
```

권한 변경 전후는 다음과 같습니다.

```text
변경 전: drwxr-xr-x → 755
변경 후: drwx------ → 700
```

`Codyssey` 디렉토리의 그룹 및 기타 사용자 권한이 제거된 것을 확인했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-16. 파일 권한 확인 및 변경</strong></summary>

파일의 기존 권한을 확인하고 `chmod` 명령어를 사용하여 권한을 변경했습니다.

#### 권한 변경 전

```bash
yhana9728258@c4r5s1 Codyssey % ls -l
total 8
-rw-r--r--  1 yhana9728258  yhana9728258  24  7 28 22:36 new.txt
```

변경 전 `new.txt` 파일의 권한은 다음과 같습니다.

```text
-rw-r--r--
```

이를 숫자로 표현하면 `644`입니다.

- 소유자: `rw-` → 읽기, 쓰기 가능
- 그룹: `r--` → 읽기 가능
- 기타 사용자: `r--` → 읽기 가능

#### 권한 변경

```bash
yhana9728258@c4r5s1 Codyssey % chmod 777 new.txt
```

`chmod 777 new.txt` 명령어를 실행하여 모든 사용자에게 읽기, 쓰기 및 실행 권한을 부여했습니다.

#### 권한 변경 후

```bash
yhana9728258@c4r5s1 Codyssey % ls -l
total 8
-rwxrwxrwx  1 yhana9728258  yhana9728258  24  7 28 22:36 new.txt
```

권한 변경 전후는 다음과 같습니다.

```text
변경 전: -rw-r--r-- → 644
변경 후: -rwxrwxrwx → 777
```

소유자, 그룹 및 기타 사용자 모두 파일을 읽고, 수정하고, 실행할 수 있도록 권한이 변경된 것을 확인했습니다.

> `777` 권한은 모든 사용자가 파일을 수정할 수 있기 때문에 보안상 위험합니다. 이번 실습에서는 권한 변화를 확인하기 위한 목적으로 사용했습니다.

<!-- 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>1-17. 실습 결과 요약</strong></summary>

이번 실습을 통해 다음과 같은 터미널 명령어를 직접 실행하고 결과를 확인했습니다.

| 명령어 | 수행 내용 |
| :--- | :--- |
| `pwd` | 현재 작업 경로 확인 |
| `ls` | 파일 및 디렉토리 목록 확인 |
| `ls -a` | 숨김 파일을 포함한 목록 확인 |
| `ls -al` | 숨김 파일과 상세 정보 확인 |
| `touch` | 빈 파일 생성 |
| `mkdir` | 디렉토리 생성 |
| `cp` | 파일 복사 |
| `cp -r` | 디렉토리 복사 |
| `mv` | 파일 및 디렉토리 이동 또는 이름 변경 |
| `rm` | 파일 삭제 |
| `rm -r` | 디렉토리와 내부 항목 삭제 |
| `cat` | 파일 내용 확인 |
| `vim` | 파일 내용 편집 |
| `cd` | 현재 작업 경로 변경 |
| `chmod` | 파일 및 디렉토리 권한 변경 |

</details>

## 2. 🐳 Docker 기본 및 컨테이너 운용
<details>
<summary><strong>2-0. Docker 기본 개념</strong></summary>

## Docker란?

**Docker는 애플리케이션을 신속하게 구축, 테스트 및 배포할 수 있는 오픈소스 컨테이너 기반 가상화 플랫폼입니다.**

### ⚓ Docker가 등장한 이유

Docker는 개발 환경과 운영 환경의 차이로 인해 발생하는 문제를 해결하기 위해 사용됩니다.

#### 1) 환경 일치

개발자 컴퓨터, 테스트 서버, 실제 운영 서버의 운영체제와 프로그램 버전이 달라 발생하는 오류를 줄일 수 있습니다.

애플리케이션과 실행 환경을 하나로 묶어 배포하기 때문에 어느 컴퓨터에서 실행하더라도 동일한 환경을 유지할 수 있습니다.

#### 2) 쉬운 설치

MySQL, MongoDB와 같은 데이터베이스나 복잡한 서버 프로그램을 명령어를 사용하여 빠르게 설치하고 실행할 수 있습니다.

```bash
docker run 이미지명
```

이미지에 필요한 설정과 프로그램이 포함되어 있기 때문에 사용자가 직접 모든 프로그램을 설치하고 설정하는 과정을 줄일 수 있습니다.

#### 3) 리소스 절약

Docker 컨테이너는 가상머신보다 적은 컴퓨터 자원을 사용합니다.

각 컨테이너가 별도의 운영체제를 실행하지 않고 호스트 운영체제의 커널을 공유하기 때문에 가볍고 빠르게 실행할 수 있습니다.

이를 통해 한 대의 컴퓨터에서 여러 개의 독립된 서비스를 효율적으로 실행할 수 있습니다.

### ⚙️ Docker의 핵심 구성 요소

Docker의 핵심 구성 요소는 `Dockerfile`, 이미지, 컨테이너입니다.

#### 1. Dockerfile

`Dockerfile`은 애플리케이션 실행에 필요한 패키지, 명령어, 환경 변수 등의 설정을 작성한 텍스트 파일입니다.

요리 과정에 비유하면 Docker 이미지를 만들기 위한 **레시피**에 해당합니다.

```dockerfile
FROM nginx:latest
COPY ./html /usr/share/nginx/html
```

#### 2. Docker 이미지

Docker 이미지는 `Dockerfile`을 빌드하여 만든 실행 환경의 원본입니다.

컨테이너 실행에 필요한 프로그램, 라이브러리 및 설정 정보가 포함된 **스냅샷 또는 설계도** 역할을 합니다.

하나의 이미지를 이용해 여러 개의 컨테이너를 생성할 수 있습니다.

```bash
docker build -t 이미지명 .
```

#### 3. Docker 컨테이너

Docker 컨테이너는 Docker 이미지를 기반으로 실제 생성되고 실행되는 인스턴스입니다.

이미지가 실행 환경의 설계도라면, 컨테이너는 해당 설계도를 기반으로 실제 실행된 애플리케이션 환경입니다.

```bash
docker run 이미지명
```

### 🚀 Docker의 기본 동작 흐름

Docker는 다음 순서로 동작합니다.

1. 개발자가 애플리케이션 실행 환경을 정의한 `Dockerfile`을 작성합니다.
2. `Dockerfile`을 빌드하여 Docker 이미지를 생성합니다.
3. 생성된 이미지를 다른 컴퓨터나 서버로 전달합니다.
4. 이미지를 실행하여 Docker 컨테이너를 생성합니다.
5. 컨테이너 내부에서 애플리케이션이 실행됩니다.

```text
Dockerfile
    ↓ docker build
Docker 이미지
    ↓ docker run
Docker 컨테이너
    ↓
애플리케이션 실행
```

<!-- Docker 동작 흐름 이미지 삽입 위치 -->

</details>

<details>
<summary><strong>2-0-1. Docker 컨테이너란?</strong></summary>

## Docker Container란?

**Docker 컨테이너는 애플리케이션과 애플리케이션 실행에 필요한 라이브러리 및 의존성을 하나로 묶어, 어디서나 동일하게 실행되도록 격리한 실행 환경입니다.**

Docker 이미지를 실행하면 컨테이너가 생성되며, 컨테이너 내부에서 애플리케이션이 실제로 동작합니다.


### Docker 컨테이너의 핵심 특징

#### 1. 독립된 격리 환경

각 컨테이너는 호스트 컴퓨터 및 다른 컨테이너와 분리된 독립적인 환경에서 실행됩니다.

각 컨테이너는 독립된 파일 시스템, 프로세스 및 네트워크 환경을 사용할 수 있기 때문에 하나의 컴퓨터 안에서도 서로 다른 서비스를 분리하여 실행할 수 있습니다.

```text
호스트 컴퓨터
├── Web 컨테이너
├── Database 컨테이너
└── Redis 컨테이너
```

#### 2. 뛰어난 이식성

컨테이너에는 애플리케이션 실행에 필요한 환경과 의존성이 함께 포함됩니다.

따라서 개발자의 컴퓨터에서 실행한 환경을 테스트 서버와 운영 서버에서도 동일하게 실행할 수 있습니다.

이를 통해 다음과 같은 문제를 줄일 수 있습니다.

> 내 컴퓨터에서는 정상적으로 실행되는데 서버에서는 실행되지 않는다.

#### 3. 가볍고 빠른 실행 속도

컨테이너는 가상머신처럼 각각의 운영체제를 별도로 부팅하지 않습니다.

호스트 운영체제의 커널을 공유하기 때문에 생성과 실행 속도가 빠르고 사용하는 자원도 비교적 적습니다.

컨테이너 내부에서 실행 중인 기본 프로세스가 시작되면 컨테이너가 실행되고, 기본 프로세스가 종료되면 컨테이너도 종료됩니다.

```bash
docker run 이미지명
```

### Docker 이미지와 컨테이너 비교

| 구분 | Docker 이미지 | Docker 컨테이너 |
| :--- | :--- | :--- |
| 의미 | 컨테이너 생성에 사용하는 실행 환경의 원본 | 이미지를 기반으로 실제 생성된 실행 환경 |
| 상태 | 정적인 파일 | 실행 가능한 인스턴스 |
| 역할 | 설계도 또는 템플릿 | 실제 실행된 애플리케이션 |
| 생성 명령어 | `docker build` | `docker run` |
| 개수 | 하나의 이미지를 저장 | 하나의 이미지로 여러 컨테이너 생성 가능 |

```text
Docker 이미지
├── 컨테이너 1
├── 컨테이너 2
└── 컨테이너 3
```

<!-- Docker 이미지와 컨테이너 비교 이미지 삽입 위치 -->

</details>

--- 

<details>
<summary><strong>2-1. Docker 설치 및 실행 상태 확인</strong></summary>

OrbStack을 실행한 후 Docker가 정상적으로 설치되고 실행 중인지 확인했습니다.

### Docker 버전 확인

`docker --version`은 현재 설치된 Docker의 버전 정보를 확인하는 명령어입니다.

```bash
docker --version
```

### Docker 실행 환경 확인

`docker info`는 Docker Engine의 전체 실행 환경과 현재 상태를 확인하는 명령어입니다.

```bash
docker info
```

`docker info`를 통해 Docker 서버가 정상적으로 실행 중인지 확인할 수 있습니다.

<!-- docker --version 실행 결과 이미지 -->

<!-- docker info 실행 결과 이미지 -->

</details>

---

<details>
<summary><strong>2-2. Docker 이미지 다운로드</strong></summary>

Docker Hub에서 `hello-world` 이미지를 다운로드했습니다.

```bash
docker pull hello-world
```

`hello-world`는 Docker 설치와 실행 상태를 확인하기 위해 사용하는 매우 작은 테스트 이미지입니다.

이미지를 실행하면 Docker가 정상적으로 이미지를 내려받고 컨테이너를 실행할 수 있는지 확인할 수 있습니다.

### 다운로드한 이미지 확인

```bash
docker images
```

`docker images` 명령어를 실행하여 로컬 환경에 저장된 Docker 이미지 목록을 확인했습니다.

목록에서 `hello-world` 이미지가 정상적으로 다운로드된 것을 확인했습니다.

<!-- Docker 이미지 다운로드 및 목록 확인 이미지 -->

</details>

---

<details>
<summary><strong>2-3. Docker 컨테이너 실행</strong></summary>

다운로드한 `hello-world` 이미지를 사용하여 컨테이너를 실행했습니다.

```bash
docker run hello-world
```

`docker run` 명령어는 다음 작업을 순서대로 수행합니다.

1. 로컬 환경에 이미지가 존재하는지 확인
2. 이미지가 없으면 Docker Hub에서 이미지 다운로드
3. 이미지를 기반으로 새로운 컨테이너 생성
4. 생성된 컨테이너 시작
5. 컨테이너에 설정된 기본 프로그램 실행

### 컨테이너의 기본 프로그램

컨테이너가 시작될 때 가장 먼저 실행되는 프로세스를 의미합니다.

이 프로세스는 컨테이너 내부의 애플리케이션을 실행하며, 기본 프로세스가 종료되면 컨테이너도 함께 종료됩니다.

`hello-world` 컨테이너의 기본 프로그램은 Docker 설치 성공 메시지를 한 번 출력한 후 종료됩니다.

<!-- hello-world 컨테이너 실행 결과 이미지 -->

</details>

---

<details>
<summary><strong>2-4. 실행 중인 컨테이너 확인</strong></summary>

현재 실행 중인 컨테이너를 확인하기 위해 `docker ps` 명령어를 사용했습니다.

```bash
docker ps
```

`docker ps`는 현재 실행 중인 컨테이너만 출력합니다.

앞에서 실행한 `hello-world` 컨테이너가 목록에 나타나지 않는 이유는 `hello-world`의 기본 프로세스가 메시지를 출력한 후 바로 종료되기 때문입니다.

컨테이너는 내부의 기본 프로세스가 실행되는 동안에만 실행 상태를 유지합니다.

### 종료된 컨테이너까지 확인

실행 중인 컨테이너뿐만 아니라 종료된 컨테이너까지 모두 확인하기 위해 `-a` 옵션을 사용했습니다.

```bash
docker ps -a
```

`-a`는 `--all`의 축약 옵션으로, 현재 실행 중인 컨테이너와 종료된 컨테이너를 모두 출력합니다.

### 컨테이너 상태 확인

```text
Exited (0)
```

`Exited (0)`은 컨테이너의 기본 프로세스가 오류 없이 정상적으로 종료되었다는 의미입니다.

종료 코드가 `0`이 아닌 경우에는 오류 또는 비정상 종료가 발생했을 가능성이 있습니다.

<!-- docker ps 실행 결과 이미지 -->

<!-- docker ps -a 실행 결과 이미지 -->

</details>

---

<details>
<summary><strong>2-5. 컨테이너 로그 확인</strong></summary>

컨테이너가 실행 중에 출력한 내용을 다시 확인하기 위해 `docker logs` 명령어를 사용했습니다.

```bash
docker logs 컨테이너명
```

`docker logs`는 실행 중인 컨테이너뿐만 아니라 종료된 컨테이너의 로그도 확인할 수 있습니다.

컨테이너가 종료되었더라도 삭제되지 않았다면 해당 컨테이너의 로그는 남아 있기 때문입니다.

### 로그 확인 실패

처음에는 다음과 같이 `hello-world`를 지정하여 로그를 확인하려고 했습니다.

```bash
docker logs hello-world
```

하지만 `hello-world`는 이미지 이름이며, 실제 생성된 컨테이너의 이름이 아닐 수 있기 때문에 로그 조회에 실패했습니다.

Docker 이미지와 컨테이너는 서로 다른 개념입니다.

- 이미지: 컨테이너를 생성하기 위한 실행 환경의 원본
- 컨테이너: 이미지를 기반으로 실제 생성되고 실행되는 인스턴스

<!-- docker logs 실패 결과 이미지 -->

### 컨테이너 이름 확인

생성된 컨테이너 이름을 확인하기 위해 다음 명령어를 실행했습니다.

```bash
docker ps -a
```

출력 결과의 `NAMES` 항목에서 Docker가 자동으로 생성한 컨테이너 이름을 확인했습니다.

### 로그 확인 성공

확인한 컨테이너 이름을 사용하여 로그를 조회했습니다.

```bash
docker logs 컨테이너명
```

예시는 다음과 같습니다.

```bash
docker logs practical_turing
```

실행 결과에서 `hello-world` 컨테이너가 출력했던 Docker 설치 성공 메시지를 다시 확인했습니다.

<!-- docker logs 성공 결과 이미지 -->

### 컨테이너 이름을 직접 지정하는 방법

컨테이너를 생성할 때 `--name` 옵션을 사용하면 원하는 이름을 직접 지정할 수 있습니다.

```bash
docker run --name hello-world-container hello-world
```

이후에는 지정한 이름으로 로그를 확인할 수 있습니다.

```bash
docker logs hello-world-container
```

</details>

## 3.커스텀 이미지 & 볼륨 관리 
> Nginx 공식 이미지를 기반으로 정적 웹 서버용 커스텀 Docker 이미지를 제작하고, 컨테이너로 실행하여 웹 페이지가 정상적으로 제공되는지 확인했습니다.
---

<details>
<summary><strong>3-1. 웹 서버 프로젝트 폴더 생성</strong></summary>

Dockerfile과 웹 서버 소스 코드를 분리하여 관리하기 위해 프로젝트 디렉토리를 생성했습니다.

```bash
mkdir -p docker-web/app
cd docker-web
```

### 명령어 설명

- `mkdir`: 새로운 디렉토리를 생성하는 명령어
- `-p`: 상위 디렉토리가 없으면 함께 생성하는 옵션
- `docker-web/app`: `docker-web` 디렉토리 안에 `app` 디렉토리 생성
- `cd docker-web`: 현재 작업 위치를 `docker-web` 디렉토리로 이동

생성된 프로젝트 구조는 다음과 같습니다.

```text
docker-web/
└── app/
```

이후 `docker-web` 디렉토리에는 `Dockerfile`을 작성하고, `app` 디렉토리에는 웹 페이지 소스 코드를 저장합니다.

<!-- 프로젝트 폴더 생성 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-2. 웹 서버 소스 코드 작성</strong></summary>

Nginx 웹 서버에서 제공할 정적 웹 페이지를 작성했습니다.

작성한 파일은 다음 경로에 저장했습니다.

```text
docker-web/app/index.html
```

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0"
    >
    <title>Hello, Codyssey World!</title>

    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #fff0f5;
            margin: 0;
        }

        .cute-card {
            width: 200px;
            height: 200px;
            background: #ffb6c1;
            border-radius: 30px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            box-shadow: 0 10px 20px rgba(255, 182, 193, 0.5);
            transition: 0.3s ease;
            cursor: pointer;
        }

        .cute-card:hover {
            transform: translateY(-10px) scale(1.05);
            background: #ff69b4;
        }

        .emoji {
            font-size: 50px;
            margin-bottom: 10px;
        }

        .text {
            color: white;
            font-family: "Malgun Gothic", sans-serif;
            font-weight: bold;
            font-size: 18px;
        }
    </style>
</head>

<body>
    <div class="cute-card">
        <div class="emoji">🥺</div>
        <div class="text">방가와요!</div>
        <div class="text">Docker 정상 운영 중</div>
    </div>
</body>
</html>
```

웹 페이지 중앙에 카드가 표시되며, 마우스를 올리면 카드가 위로 이동하고 크기와 배경색이 변경되도록 구성했습니다.

<!-- index.html 작성 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-3. Dockerfile 작성</strong></summary>

Nginx 공식 이미지를 기반으로 커스텀 이미지를 만들기 위해 `Dockerfile`을 작성했습니다.

작성 위치는 다음과 같습니다.

```text
docker-web/Dockerfile
```

```dockerfile
FROM nginx:alpine

LABEL org.opencontainers.image.title="codyssey-web"
LABEL org.opencontainers.image.description="Codyssey Docker workstation web server"

COPY app/ /usr/share/nginx/html/

EXPOSE 80
```

### `FROM nginx:alpine`

```dockerfile
FROM nginx:alpine
```

커스텀 이미지의 기반 이미지로 Nginx 공식 이미지를 사용합니다.

Nginx가 이미 설치되고 기본 설정까지 완료된 이미지를 사용하기 때문에, Linux 설치부터 Nginx 패키지 설치 및 설정까지 직접 수행할 필요가 없습니다.

`alpine`은 Alpine Linux를 기반으로 제작된 Nginx 이미지 변형을 의미합니다.

Alpine Linux는 크기가 작고 필요한 구성만 포함하므로 일반적인 Nginx 이미지보다 비교적 가볍습니다.

---

### `LABEL`

```dockerfile
LABEL org.opencontainers.image.title="codyssey-web"
LABEL org.opencontainers.image.description="Codyssey Docker workstation web server"
```

Docker 이미지에 제목과 설명 등의 메타데이터를 추가합니다.

메타데이터는 이미지 자체의 실행 내용이 아니라, 이미지의 이름과 목적 등을 설명하기 위한 정보입니다.

작성한 메타데이터는 다음 명령어로 확인할 수 있습니다.

```bash
docker inspect codyssey-web:1.0
```

---

### `COPY`

```dockerfile
COPY app/ /usr/share/nginx/html/
```

호스트 컴퓨터의 `app` 디렉토리 안에 있는 웹 소스 코드를 Docker 이미지 내부로 복사합니다.

Nginx는 기본적으로 다음 경로에 있는 파일을 웹 콘텐츠로 제공합니다.

```text
/usr/share/nginx/html/
```

따라서 `app/index.html` 파일이 이미지 내부의 Nginx 기본 웹 경로로 복사되고, 컨테이너 실행 시 해당 페이지가 제공됩니다.

> `COPY`는 컨테이너 실행 시점이 아니라 이미지 빌드 시점에 수행됩니다. 이미지 빌드가 끝난 후 호스트의 HTML 파일을 수정해도 기존 이미지에는 자동으로 반영되지 않습니다. 변경 내용을 적용하려면 이미지를 다시 빌드해야 합니다.

---

### `EXPOSE`

```dockerfile
EXPOSE 80
```

컨테이너 내부의 애플리케이션이 80번 포트를 사용한다는 사실을 명시합니다.

다만 `EXPOSE`만으로는 호스트 컴퓨터에 포트가 실제 공개되지 않습니다.

호스트와 컨테이너의 포트를 연결하려면 컨테이너 실행 시 `docker run` 명령어에 `-p` 옵션을 사용해야 합니다.

```bash
docker run -p 8080:80 이미지명
```

<!-- Dockerfile 작성 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-4. 커스텀 Docker 이미지 빌드</strong></summary>

작성한 Dockerfile을 이용하여 정적 웹 서버용 커스텀 이미지를 생성했습니다.

```bash
docker build -t codyssey-web:1.0 .
```

### 명령어 설명

- `docker build`: Dockerfile을 읽어 새로운 Docker 이미지를 생성
- `-t`: 이미지의 이름과 태그를 지정하는 옵션
- `codyssey-web`: 이미지 이름
- `1.0`: 이미지 태그
- `.`: 현재 디렉토리를 빌드 컨텍스트로 사용

### 빌드 컨텍스트

마지막의 `.`은 현재 디렉토리에 있는 파일을 Docker 빌드 과정에서 사용할 수 있도록 전달한다는 의미입니다.

현재 디렉토리 구조는 다음과 같습니다.

```text
docker-web/
├── Dockerfile
└── app/
    └── index.html
```

Docker는 현재 디렉토리의 `Dockerfile`을 읽고, `COPY app/ /usr/share/nginx/html/` 명령어를 통해 `app` 디렉토리의 내용을 이미지에 포함합니다.

<!-- 커스텀 이미지 빌드 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-5. 생성된 Docker 이미지 확인</strong></summary>

커스텀 이미지가 로컬 Docker 이미지 저장소에 정상적으로 생성되었는지 확인했습니다.

```bash
docker images codyssey-web
```

`docker images` 뒤에 이미지 이름을 지정하면 해당 이름과 일치하는 이미지만 확인할 수 있습니다.

확인해야 할 주요 항목은 다음과 같습니다.

| 항목 | 의미 |
| :--- | :--- |
| `REPOSITORY` | Docker 이미지 이름 |
| `TAG` | 이미지 버전 또는 용도 |
| `IMAGE ID` | 이미지 고유 식별자 |
| `CREATED` | 이미지 생성 시점 |
| `SIZE` | 이미지 크기 |

이미지 이름이 `codyssey-web`, 태그가 `1.0`으로 생성되었는지 확인했습니다.

<!-- 생성된 Docker 이미지 확인 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-6. 커스텀 이미지로 컨테이너 실행</strong></summary>

생성한 `codyssey-web:1.0` 이미지를 기반으로 실제 컨테이너를 생성하고 실행했습니다.

```bash
docker run -d --name codyssey-web -p 8080:80 codyssey-web:1.0
```

### `docker run`

이미지는 애플리케이션을 실행하기 위한 정적인 설계도입니다.

`docker run` 명령어를 실행하면 해당 이미지를 기반으로 실제 동작하는 컨테이너가 생성되고 실행됩니다.

```text
Docker 이미지
    ↓ docker run
Docker 컨테이너
    ↓
Nginx 웹 서버 실행
```

---

### `-d`

```bash
-d
```

`detached` 모드의 축약 옵션입니다.

컨테이너를 터미널의 백그라운드에서 실행하기 때문에 컨테이너가 실행된 상태에서도 현재 터미널을 계속 사용할 수 있습니다.

---

### `--name`

```bash
--name codyssey-web
```

생성되는 컨테이너 이름을 `codyssey-web`으로 지정합니다.

이름을 지정하면 컨테이너 ID 대신 이름을 이용하여 관리할 수 있습니다.

```bash
docker logs codyssey-web
docker stop codyssey-web
docker start codyssey-web
docker rm codyssey-web
```

---

### `-p 8080:80`

```bash
-p 8080:80
```

호스트 컴퓨터의 8080번 포트와 컨테이너 내부의 80번 포트를 연결합니다.

```text
웹 브라우저
    ↓
localhost:8080
    ↓
호스트 8080 포트
    ↓
컨테이너 80 포트
    ↓
Nginx 웹 서버
```

따라서 웹 브라우저에서 다음 주소로 접속하면 컨테이너 내부의 Nginx 웹 페이지를 확인할 수 있습니다.

```text
http://localhost:8080
```

<!-- 컨테이너 실행 명령 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-7. 컨테이너 실행 오류 및 원인 분석</strong></summary>

처음 컨테이너를 실행했을 때 다음 오류가 발생했습니다.

```bash
docker run -d --name codyssey-web -p 8080:80 codyssey-web:1.0
```

```text
docker: Error response from daemon: pull access denied for codyssey-web,
repository does not exist or may require 'docker login':
denied: requested access to the resource is denied

Run 'docker run --help' for more information
```

### 오류 원인

컨테이너 실행 시 지정한 이미지 태그는 다음과 같습니다.

```text
codyssey-web:1.0
```

하지만 실제로 빌드된 이미지의 태그는 숫자 `0`이 아니라 알파벳 `o`가 사용된 다음 값이었습니다.

```text
codyssey-web:1.o
```

로컬에 `codyssey-web:1.0` 이미지가 존재하지 않자 Docker는 원격 이미지 저장소인 Docker Hub에서 해당 이미지를 다운로드하려고 시도했습니다.

그러나 Docker Hub에는 해당 이미지가 없거나 접근 권한이 없었기 때문에 `pull access denied` 오류가 발생했습니다.

```text
요청한 이미지: codyssey-web:1.0
실제 로컬 이미지: codyssey-web:1.o
```

<!-- Docker 컨테이너 실행 오류 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-8. 잘못 생성된 이미지 삭제 및 재빌드</strong></summary>

잘못된 태그인 `1.o`로 생성된 이미지를 삭제했습니다.

```bash
docker rmi codyssey-web:1.o
```

### 명령어 설명

- `docker rmi`: Docker 이미지를 삭제하는 명령어
- `codyssey-web:1.o`: 삭제할 이미지 이름과 태그

이미지를 삭제한 후 올바른 태그인 `1.0`을 사용하여 다시 빌드했습니다.

```bash
docker build -t codyssey-web:1.0 .
```

재빌드 후 이미지 태그가 올바르게 생성되었는지 다시 확인했습니다.

```bash
docker images codyssey-web
```

출력 결과에서 다음 이미지가 존재하는지 확인했습니다.

```text
codyssey-web:1.0
```

<!-- 잘못된 이미지 삭제 및 재빌드 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-9. 컨테이너 실행 성공 및 웹 페이지 확인</strong></summary>

올바른 태그로 이미지를 다시 빌드한 후 컨테이너를 실행했습니다.

```bash
docker run -d --name codyssey-web -p 8080:80 codyssey-web:1.0
```

실행 중인 컨테이너를 확인했습니다.

```bash
docker ps
```

`docker ps` 출력 결과에서 다음 내용을 확인했습니다.

- 컨테이너 이름: `codyssey-web`
- 사용 이미지: `codyssey-web:1.0`
- 컨테이너 상태: `Up`
- 포트 연결: `0.0.0.0:8080->80/tcp`

웹 브라우저에서 다음 주소로 접속했습니다.

```text
http://localhost:8080
```

작성한 HTML 페이지와 `Docker 정상 운영 중` 문구가 정상적으로 표시되는 것을 확인했습니다.

<!-- 컨테이너 실행 성공 결과 이미지 삽입 위치 -->

<!-- docker ps 실행 결과 이미지 삽입 위치 -->

<!-- 웹 브라우저 접속 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>3-10. 실습 결과 요약</strong></summary>

이번 실습에서는 Nginx 공식 이미지를 기반으로 정적 웹 서버용 커스텀 이미지를 제작했습니다.

| 수행 항목 | 사용 명령어 또는 설정 |
| :--- | :--- |
| 프로젝트 디렉토리 생성 | `mkdir -p docker-web/app` |
| 정적 웹 페이지 작성 | `app/index.html` |
| 기반 이미지 설정 | `FROM nginx:alpine` |
| 이미지 메타데이터 설정 | `LABEL` |
| 웹 소스 코드 복사 | `COPY app/ /usr/share/nginx/html/` |
| 컨테이너 사용 포트 명시 | `EXPOSE 80` |
| 커스텀 이미지 빌드 | `docker build -t codyssey-web:1.0 .` |
| 생성 이미지 확인 | `docker images codyssey-web` |
| 컨테이너 실행 | `docker run -d --name codyssey-web -p 8080:80 codyssey-web:1.0` |
| 실행 상태 확인 | `docker ps` |
| 잘못된 이미지 삭제 | `docker rmi codyssey-web:1.o` |
| 웹 서버 접속 | `http://localhost:8080` |

Dockerfile을 통해 웹 서버 실행 환경을 이미지로 정의하고, 이미지를 빌드하여 실제 컨테이너를 실행했습니다.

또한 이미지 태그 오타로 인해 로컬 이미지를 찾지 못하고 Docker Hub에서 이미지를 내려받으려다 실패한 오류를 분석하고, 잘못된 이미지를 삭제한 뒤 올바른 태그로 재빌드하여 해결했습니다.

</details>

## 4. 💾 바인드 마운트와 Docker 볼륨

> 바인드 마운트를 사용하여 호스트의 웹 소스 코드 변경 사항이 컨테이너에 실시간으로 반영되는지 확인하고, Docker 볼륨을 사용하여 컨테이너를 삭제한 후에도 데이터가 유지되는지 검증했습니다.

---

<details>
<summary><strong>4-0. 바인드 마운트와 Docker 볼륨 기본 개념</strong></summary>

### 🛠️ 바인드 마운트

바인드 마운트는 호스트 컴퓨터의 특정 파일 또는 디렉토리를 컨테이너 내부 경로에 직접 연결하는 기능입니다.

```text
호스트의 app 디렉토리
        ↕
컨테이너의 Nginx 웹 콘텐츠 디렉토리
```

#### 핵심 역할

호스트 컴퓨터의 소스 코드 디렉토리와 컨테이너 내부 디렉토리를 실시간으로 연결합니다.

일반적인 Docker 이미지 방식에서는 소스 코드를 수정할 때마다 다음 과정을 반복해야 합니다.

```text
소스 코드 수정
    ↓
Docker 이미지 재빌드
    ↓
기존 컨테이너 삭제
    ↓
새 컨테이너 실행
```

바인드 마운트를 사용하면 호스트 파일을 수정하고 저장하는 즉시 컨테이너에서도 변경된 파일을 확인할 수 있습니다.

```text
소스 코드 수정 및 저장
    ↓
컨테이너에 즉시 반영
```

따라서 개발 중 반복적인 이미지 빌드와 컨테이너 재생성 과정을 줄일 수 있습니다.

> 바인드 마운트는 개발 중인 소스 코드를 컨테이너에 실시간으로 연결하기 위해 주로 사용합니다.

---

### 💾 Docker 볼륨

Docker 볼륨은 Docker가 직접 생성하고 관리하는 데이터 저장 공간입니다.

컨테이너 내부에만 데이터를 저장하면 컨테이너 삭제 시 해당 데이터도 함께 사라질 수 있습니다.

볼륨을 컨테이너에 연결하면 데이터가 컨테이너와 분리되어 저장됩니다.

```text
Docker 컨테이너
        ↕
Docker 볼륨
```

컨테이너를 삭제하더라도 볼륨을 별도로 삭제하지 않는 한 데이터는 유지됩니다.

따라서 MySQL, PostgreSQL과 같은 데이터베이스의 데이터나 서비스 운영 중 유지해야 하는 파일을 저장할 때 사용합니다.

> Docker 볼륨은 컨테이너의 생성 및 삭제 여부와 관계없이 데이터를 안전하게 보존하기 위해 사용합니다.

---

### 바인드 마운트와 Docker 볼륨 비교

| 구분 | 바인드 마운트 | Docker 볼륨 |
| :--- | :--- | :--- |
| 저장 위치 | 사용자가 지정한 호스트 경로 | Docker가 관리하는 저장 공간 |
| 주요 목적 | 개발 중 소스 코드 실시간 반영 | 운영 데이터 및 DB 데이터 보존 |
| 파일 접근 | 호스트에서 직접 접근 가능 | Docker 명령어나 연결된 컨테이너를 통해 접근 |
| 컨테이너 삭제 시 | 호스트 파일 유지 | 볼륨을 삭제하지 않으면 데이터 유지 |
| 대표 사용 사례 | HTML, CSS, JavaScript, 애플리케이션 소스 | MySQL, PostgreSQL, 업로드 파일, 영속 데이터 |

---

### 사용하는 이유

바인드 마운트와 볼륨을 사용하는 목적은 중요한 파일과 데이터를 컨테이너의 생명주기에서 분리하기 위해서입니다.

```text
중요한 데이터는 별도로 보존
        +
컨테이너는 필요할 때 생성·삭제
```

컨테이너는 필요할 때마다 삭제하고 다시 생성할 수 있지만, 소스 코드와 서비스 데이터는 호스트 또는 Docker 볼륨에 유지할 수 있습니다.

---

### 실무 사용 예시

하나의 웹 서비스를 구성할 때 바인드 마운트와 Docker 볼륨을 함께 사용할 수 있습니다.

1. 웹 소스 코드인 `app/` 디렉토리는 바인드 마운트로 연결합니다.
2. MySQL 데이터는 Docker 볼륨에 저장합니다.
3. 여러 컨테이너와 마운트 설정은 Docker Compose로 함께 관리합니다.

```text
웹 애플리케이션 소스
    └── 바인드 마운트

MySQL 데이터
    └── Docker 볼륨

전체 서비스 실행 및 관리
    └── Docker Compose
```

<!-- 바인드 마운트와 Docker 볼륨 개념 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-1. 바인드 마운트 컨테이너 실행</strong></summary>

호스트 컴퓨터의 `app` 디렉토리를 컨테이너 내부의 Nginx 웹 콘텐츠 경로에 연결하여 컨테이너를 실행했습니다.

```bash
docker run -d \
  --name bind-web \
  -p 8081:80 \
  --mount "type=bind,source=$(pwd)/app,target=/usr/share/nginx/html,readonly" \
  codyssey-web:1.0
```

### 명령어 구성

#### `-d`

```bash
-d
```

컨테이너를 백그라운드에서 실행하는 `detached` 모드입니다.

---

#### `--name bind-web`

```bash
--name bind-web
```

생성되는 컨테이너의 이름을 `bind-web`으로 지정합니다.

---

#### `-p 8081:80`

```bash
-p 8081:80
```

호스트 컴퓨터의 8081번 포트와 컨테이너 내부의 80번 포트를 연결합니다.

```text
http://localhost:8081
        ↓
호스트 8081번 포트
        ↓
컨테이너 80번 포트
        ↓
Nginx 웹 서버
```

---

#### `type=bind`

```bash
type=bind
```

이번 마운트가 Docker 볼륨이 아니라 호스트 경로를 직접 연결하는 바인드 마운트임을 지정합니다.

---

#### `source=$(pwd)/app`

```bash
source=$(pwd)/app
```

컨테이너에 연결할 호스트의 원본 디렉토리를 지정합니다.

`$(pwd)`는 현재 작업 디렉토리의 절대 경로로 치환됩니다.

현재 디렉토리가 다음과 같다면,

```text
/Users/yhana9728258/docker-web
```

실제 연결 경로는 다음과 같이 해석됩니다.

```text
/Users/yhana9728258/docker-web/app
```

---

#### `target=/usr/share/nginx/html`

```bash
target=/usr/share/nginx/html
```

호스트의 `app` 디렉토리를 연결할 컨테이너 내부 경로입니다.

Nginx는 기본적으로 다음 경로에 있는 파일을 웹 콘텐츠로 제공합니다.

```text
/usr/share/nginx/html
```

바인드 마운트가 연결되면 이미지 빌드 시 복사된 기존 디렉토리 대신 호스트의 `app` 디렉토리 내용이 해당 경로에서 보이게 됩니다.

---

#### `readonly`

```bash
readonly
```

컨테이너에서는 연결된 파일을 읽을 수 있지만 수정할 수 없도록 설정합니다.

호스트에서 파일을 수정하는 것은 가능하며, 호스트의 변경 사항은 컨테이너에서 즉시 확인할 수 있습니다.

<!-- 바인드 마운트 컨테이너 실행 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-2. 바인드 마운트 컨테이너 실행 상태 확인</strong></summary>

`bind-web` 컨테이너가 정상적으로 실행 중인지 확인했습니다.

```bash
docker ps --filter name=bind-web
```

### 명령어 설명

- `docker ps`: 현재 실행 중인 컨테이너 목록 확인
- `--filter`: 조건에 맞는 컨테이너만 출력
- `name=bind-web`: 컨테이너 이름에 `bind-web`이 포함된 항목 검색

출력 결과에서 다음 항목을 확인합니다.

- 컨테이너 이름이 `bind-web`인지
- 컨테이너 상태가 `Up`인지
- 호스트 8081번 포트가 컨테이너 80번 포트와 연결되었는지

```text
0.0.0.0:8081->80/tcp
```

> `docker ps`는 컨테이너의 실행 상태와 포트 연결을 확인하는 명령어입니다. 실제 마운트 세부 설정은 `docker inspect`를 사용해야 확인할 수 있습니다.

마운트 설정을 상세하게 확인하려면 다음 명령어를 사용할 수 있습니다.

```bash
docker inspect bind-web
```

<!-- bind-web 컨테이너 실행 상태 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-3. 호스트 파일 생성 전 웹 서버 응답 확인</strong></summary>

바인드 마운트의 실시간 반영 여부를 검증하기 전에 `bind-test.txt` 파일이 존재하지 않는 상태의 응답을 확인했습니다.

```bash
curl -i http://localhost:8081/bind-test.txt
```

### `curl`

`curl`은 URL을 통해 서버에 요청을 보내고 응답을 확인할 수 있는 명령줄 도구입니다.

```bash
curl URL
```

---

### `-i`

```bash
-i
```

`include`의 축약 옵션으로, 서버가 반환한 응답 본문과 함께 HTTP 응답 헤더도 출력합니다.

따라서 다음과 같은 HTTP 상태 정보를 확인할 수 있습니다.

```text
HTTP/1.1 404 Not Found
```

### 먼저 404 응답을 확인한 이유

호스트에 `bind-test.txt` 파일을 만들기 전에는 해당 파일이 웹 서버에 존재하지 않았다는 사실을 증거로 남기기 위해 확인했습니다.

이후 호스트에 파일을 생성하고 다시 같은 URL로 요청하여 응답이 변경되는지 비교합니다.

```text
파일 생성 전
    ↓
404 Not Found

호스트에 파일 생성
    ↓
200 OK
```

<!-- bind-test.txt 생성 전 404 응답 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-4. 호스트의 바인드 마운트 디렉토리에 파일 생성</strong></summary>

호스트의 `app` 디렉토리에 `bind-test.txt` 파일을 생성했습니다.

```bash
yhana9728258@c4r10s2 docker-web % touch ./app/bind-test.txt
yhana9728258@c4r10s2 docker-web % vim ./app/bind-test.txt
yhana9728258@c4r10s2 docker-web % cat ./app/bind-test.txt
바인드 마운드 업데이트 성공!
```

### 작업 과정

1. `touch` 명령어로 빈 파일을 생성했습니다.
2. `vim` 편집기를 사용하여 내용을 작성했습니다.
3. `cat` 명령어로 저장된 내용을 확인했습니다.

```bash
touch ./app/bind-test.txt
```

호스트의 `app` 디렉토리에 빈 파일을 생성합니다.

```bash
vim ./app/bind-test.txt
```

파일을 열어 다음 내용을 작성하고 저장합니다.

```text
바인드 마운드 업데이트 성공!
```

```bash
cat ./app/bind-test.txt
```

호스트 파일에 내용이 정상적으로 저장되었는지 확인합니다.

<!-- 호스트 bind-test.txt 파일 생성 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-5. 호스트 파일 변경 후 웹 서버 응답 확인</strong></summary>

이미지를 다시 빌드하거나 컨테이너를 재시작하지 않은 상태에서 같은 URL로 요청했습니다.

```bash
curl -i http://localhost:8081/bind-test.txt
```

응답 본문에서 호스트 파일에 작성한 내용을 확인했습니다.

```text
바인드 마운드 업데이트 성공!
```

### 검증 결과

다음 작업은 수행하지 않았습니다.

```text
docker build 실행 안 함
docker restart 실행 안 함
docker rm 실행 안 함
docker run 재실행 안 함
```

그런데도 웹 서버에서 새로 생성한 파일을 즉시 확인할 수 있었습니다.

이는 호스트의 `app` 디렉토리와 컨테이너의 `/usr/share/nginx/html` 디렉토리가 바인드 마운트로 직접 연결되어 있기 때문입니다.

```text
호스트 app/bind-test.txt 생성
        ↓
바인드 마운트로 즉시 반영
        ↓
컨테이너의 /usr/share/nginx/html/bind-test.txt
        ↓
Nginx 웹 응답
```

따라서 바인드 마운트를 사용하면 개발 중 소스 코드 변경 사항을 이미지 재빌드 없이 바로 확인할 수 있습니다.

<!-- 호스트 변경 후 curl 성공 응답 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-6. Docker 볼륨 생성</strong></summary>

컨테이너와 분리하여 데이터를 저장하기 위해 `codyssey-data`라는 이름의 Docker 볼륨을 생성했습니다.

```bash
docker volume create codyssey-data
```

### 명령어 설명

- `docker volume`: Docker 볼륨 관리
- `create`: 새로운 볼륨 생성
- `codyssey-data`: 생성할 볼륨 이름

생성된 볼륨을 확인했습니다.

```bash
docker volume ls --filter name=codyssey-data
```

### 확인 명령어 설명

- `docker volume ls`: 생성된 Docker 볼륨 목록 확인
- `--filter name=codyssey-data`: 이름에 `codyssey-data`가 포함된 볼륨만 출력

출력 결과에서 `codyssey-data` 볼륨이 정상적으로 생성된 것을 확인했습니다.

<!-- Docker 볼륨 생성 및 확인 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-7. 기존 컨테이너에 볼륨을 추가하려다 발생한 문제</strong></summary>

처음에는 기존에 생성한 `bind-web` 컨테이너에 새 Docker 볼륨을 추가하려고 했습니다.

그러나 이미 생성된 Docker 컨테이너에는 새로운 마운트나 포트 매핑 설정을 추가할 수 없습니다.

컨테이너의 다음 설정은 생성 시점에 결정됩니다.

- 포트 매핑
- 바인드 마운트
- Docker 볼륨
- 네트워크 설정
- 환경 변수 일부
- 컨테이너 이름

따라서 새로운 볼륨 설정이 필요하다면 기존 컨테이너를 그대로 수정하는 것이 아니라 새로운 설정으로 컨테이너를 다시 생성해야 합니다.

```text
기존 컨테이너에 볼륨 추가
    → 불가능

새 볼륨 설정으로 새 컨테이너 생성
    → 가능
```

---

### 호스트 포트 충돌 문제

기존 `bind-web` 컨테이너는 다음 포트를 사용하고 있었습니다.

```text
호스트 8081번 포트 → 컨테이너 80번 포트
```

다른 컨테이너에서도 동일한 호스트 포트인 8081번을 사용하려 하면 포트 충돌이 발생합니다.

```text
bind-web
호스트 8081 → 컨테이너 80

새 컨테이너
호스트 8081 → 컨테이너 80
              ↑
        호스트 포트 충돌
```

여러 컨테이너가 각각 내부 80번 포트를 사용하는 것은 가능합니다.

하지만 동일한 호스트 IP에서 두 컨테이너가 같은 호스트 포트를 동시에 사용할 수는 없습니다.

따라서 볼륨 테스트용 새 컨테이너는 호스트의 8082번 포트를 사용하도록 구성했습니다.

```text
bind-web
호스트 8081 → 컨테이너 80

volume-web-1
호스트 8082 → 컨테이너 80
```

<!-- 기존 컨테이너 볼륨 추가 및 포트 충돌 관련 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-8. Docker 볼륨을 연결한 새 컨테이너 실행</strong></summary>

기존 `bind-web` 컨테이너와 호스트 포트가 충돌하지 않도록 8082번 포트를 사용하는 새 컨테이너를 생성했습니다.

```bash
docker run -d \
  --name volume-web-1 \
  -p 8082:80 \
  --mount type=volume,source=codyssey-data,target=/usr/share/nginx/html/data \
  codyssey-web:1.0
```

### 명령어 설명

#### `--name volume-web-1`

```bash
--name volume-web-1
```

새 컨테이너의 이름을 `volume-web-1`로 지정합니다.

---

#### `-p 8082:80`

```bash
-p 8082:80
```

호스트의 8082번 포트로 들어온 요청을 컨테이너 내부의 80번 포트로 전달합니다.

---

#### `type=volume`

```bash
type=volume
```

Docker가 직접 관리하는 볼륨을 사용한다는 의미입니다.

---

#### `source=codyssey-data`

```bash
source=codyssey-data
```

컨테이너에 연결할 기존 Docker 볼륨의 이름입니다.

---

#### `target=/usr/share/nginx/html/data`

```bash
target=/usr/share/nginx/html/data
```

`codyssey-data` 볼륨을 연결할 컨테이너 내부 경로입니다.

컨테이너에서 해당 경로에 저장한 파일은 컨테이너의 writable layer가 아니라 `codyssey-data` 볼륨에 저장됩니다.

---

#### `codyssey-web:1.0`

```bash
codyssey-web:1.0
```

컨테이너 생성에 사용할 커스텀 Docker 이미지입니다.

### 컨테이너 실행 상태 확인

```bash
docker ps --filter name=volume-web-1
```

출력 결과에서 다음 사항을 확인했습니다.

- 컨테이너 이름이 `volume-web-1`인지
- 상태가 `Up`인지
- 호스트 8082번 포트가 컨테이너 80번 포트에 연결되었는지

<!-- volume-web-1 컨테이너 실행 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-9. Docker 볼륨에 데이터 생성 및 확인</strong></summary>

실행 중인 `volume-web-1` 컨테이너 내부에서 명령어를 실행하여 볼륨에 파일을 생성했습니다.

```bash
docker exec volume-web-1 sh -c \
  'echo "Persistent data created by volume-web-1" > /usr/share/nginx/html/data/result.txt'
```

### 명령어 설명

#### `docker exec`

```bash
docker exec volume-web-1
```

이미 실행 중인 `volume-web-1` 컨테이너 내부에서 추가 명령어를 실행합니다.

---

#### `sh -c`

```bash
sh -c
```

뒤에 전달된 문자열을 셸 명령어로 해석하여 실행합니다.

파일 리다이렉션 기호인 `>`를 사용하기 위해 셸을 통해 명령어를 실행했습니다.

---

#### `echo`

```bash
echo "Persistent data created by volume-web-1"
```

문자열을 표준 출력으로 전달합니다.

---

#### `> result.txt`

```bash
> /usr/share/nginx/html/data/result.txt
```

출력된 문자열을 `result.txt` 파일에 저장합니다.

해당 경로에는 `codyssey-data` 볼륨이 연결되어 있으므로 데이터는 Docker 볼륨에 저장됩니다.

### 생성된 데이터 확인

```bash
docker exec volume-web-1 \
  cat /usr/share/nginx/html/data/result.txt
```

출력 결과에서 다음 문자열을 확인했습니다.

```text
Persistent data created by volume-web-1
```

이를 통해 `result.txt` 파일이 볼륨 경로에 정상적으로 생성된 것을 확인했습니다.

<!-- Docker 볼륨 데이터 생성 및 확인 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-10. 첫 번째 볼륨 컨테이너 삭제</strong></summary>

데이터를 생성한 `volume-web-1` 컨테이너를 삭제했습니다.

```bash
docker rm -f volume-web-1
```

### 명령어 설명

- `docker rm`: Docker 컨테이너 삭제
- `-f`: 실행 중인 컨테이너를 강제로 종료한 후 삭제
- `volume-web-1`: 삭제할 컨테이너 이름

`-f` 옵션을 사용하지 않는 경우 실행 중인 컨테이너는 먼저 중지해야 합니다.

```bash
docker stop volume-web-1
docker rm volume-web-1
```

`-f` 옵션을 사용하면 위 과정을 한 번에 수행합니다.

<!-- volume-web-1 컨테이너 삭제 결과 이미지 삽입 위치 -->

### 컨테이너 삭제 여부 확인

```bash
docker ps -a --filter name=volume-web-1
```

`docker ps -a`는 실행 중인 컨테이너와 종료된 컨테이너를 모두 확인합니다.

출력 결과에 `volume-web-1`이 나타나지 않는 것을 통해 컨테이너가 실제로 삭제되었음을 확인했습니다.

<!-- volume-web-1 삭제 확인 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-11. 컨테이너 삭제 후 Docker 볼륨 확인</strong></summary>

`volume-web-1` 컨테이너를 삭제한 후에도 `codyssey-data` 볼륨이 남아 있는지 확인했습니다.

```bash
docker volume ls --filter name=codyssey-data
```

출력 결과에서 `codyssey-data` 볼륨이 계속 존재하는 것을 확인했습니다.

```text
volume-web-1 컨테이너
    → 삭제됨

codyssey-data 볼륨
    → 유지됨
```

이는 컨테이너와 Docker 볼륨의 생명주기가 서로 분리되어 있기 때문입니다.

컨테이너를 삭제하더라도 볼륨을 명시적으로 삭제하지 않는 한 데이터 저장 공간은 유지됩니다.

Docker 볼륨을 삭제하려면 별도의 명령어가 필요합니다.

```bash
docker volume rm codyssey-data
```

이번 실습에서는 데이터 영속성을 확인해야 하므로 볼륨을 삭제하지 않았습니다.

<!-- 컨테이너 삭제 후 codyssey-data 볼륨 확인 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-12. 동일한 볼륨을 새 컨테이너에 연결</strong></summary>

기존 컨테이너는 삭제했지만 동일한 `codyssey-data` 볼륨을 사용하여 새로운 컨테이너를 생성했습니다.

```bash
docker run -d \
  --name volume-web-2 \
  -p 8082:80 \
  --mount type=volume,source=codyssey-data,target=/usr/share/nginx/html/data \
  codyssey-web:1.0
```

### 이전 컨테이너와 새 컨테이너 비교

```text
기존 컨테이너: volume-web-1
새 컨테이너: volume-web-2

공통으로 사용하는 볼륨: codyssey-data
공통 볼륨 연결 경로: /usr/share/nginx/html/data
```

`volume-web-1`은 이미 삭제되었으므로 호스트 8082번 포트를 새 컨테이너에서 다시 사용할 수 있습니다.

```text
volume-web-1 삭제
    ↓
호스트 8082번 포트 반환
    ↓
volume-web-2가 8082번 포트 사용
```

<!-- volume-web-2 컨테이너 실행 결과 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-13. 새 컨테이너에서 기존 데이터 확인</strong></summary>

새로 생성한 `volume-web-2` 컨테이너에서 기존 `result.txt` 파일의 내용을 확인했습니다.

```bash
docker exec volume-web-2 \
  cat /usr/share/nginx/html/data/result.txt
```

### 명령어 설명

- `docker exec`: 실행 중인 컨테이너 내부에서 명령어 실행
- `volume-web-2`: 명령어를 실행할 컨테이너 이름
- `cat`: 파일 내용 출력
- `/usr/share/nginx/html/data/result.txt`: 확인할 파일 경로

출력 결과에서 첫 번째 컨테이너가 생성했던 데이터를 확인했습니다.

```text
Persistent data created by volume-web-1
```

현재 명령어를 실행한 컨테이너는 `volume-web-2`이지만, 파일 내용에는 첫 번째 컨테이너인 `volume-web-1`에서 생성한 문자열이 그대로 남아 있었습니다.

```text
volume-web-1에서 데이터 생성
        ↓
codyssey-data 볼륨에 저장
        ↓
volume-web-1 컨테이너 삭제
        ↓
volume-web-2에 동일한 볼륨 연결
        ↓
기존 데이터 확인 성공
```

이를 통해 데이터가 컨테이너 내부에만 저장된 것이 아니라 `codyssey-data` 볼륨에 저장되었음을 확인했습니다.

또한 컨테이너를 삭제하고 새로 생성하더라도 동일한 볼륨을 연결하면 기존 데이터를 다시 사용할 수 있다는 것을 검증했습니다.

<!-- volume-web-2에서 기존 데이터 확인 이미지 삽입 위치 -->

<!-- 삭제 전후 데이터 비교 이미지 삽입 위치 -->

</details>

---

<details>
<summary><strong>4-14. 바인드 마운트 및 Docker 볼륨 실습 결과 요약</strong></summary>

### 바인드 마운트 검증 결과

호스트의 `app` 디렉토리를 컨테이너의 Nginx 웹 콘텐츠 경로에 연결했습니다.

호스트에서 `bind-test.txt` 파일을 새로 생성한 후 이미지 재빌드나 컨테이너 재실행 없이 웹 서버에서 파일을 확인했습니다.

```text
호스트 파일 변경
    ↓
바인드 마운트를 통해 즉시 반영
    ↓
웹 서버 응답 확인
```

이를 통해 바인드 마운트를 사용하면 개발 중 소스 코드 변경 사항을 컨테이너에 실시간으로 반영할 수 있음을 확인했습니다.

---

### Docker 볼륨 검증 결과

`volume-web-1` 컨테이너에서 `codyssey-data` 볼륨에 데이터를 저장한 후 컨테이너를 삭제했습니다.

이후 `volume-web-2` 컨테이너에 동일한 볼륨을 연결하고 기존 데이터를 다시 확인했습니다.

```text
volume-web-1에서 데이터 생성
    ↓
codyssey-data 볼륨에 저장
    ↓
volume-web-1 삭제
    ↓
volume-web-2 생성
    ↓
codyssey-data 재연결
    ↓
기존 데이터 확인
```

이를 통해 컨테이너가 삭제되어도 Docker 볼륨의 데이터는 유지되는 것을 확인했습니다.

---

### 사용한 주요 명령어

| 수행 항목 | 명령어 |
| :--- | :--- |
| 바인드 마운트 컨테이너 실행 | `docker run --mount type=bind ...` |
| 컨테이너 실행 상태 확인 | `docker ps --filter name=bind-web` |
| HTTP 응답 확인 | `curl -i http://localhost:8081/bind-test.txt` |
| Docker 볼륨 생성 | `docker volume create codyssey-data` |
| Docker 볼륨 목록 확인 | `docker volume ls --filter name=codyssey-data` |
| 볼륨 연결 컨테이너 실행 | `docker run --mount type=volume ...` |
| 실행 중인 컨테이너 내부 명령 실행 | `docker exec` |
| 컨테이너 강제 삭제 | `docker rm -f volume-web-1` |
| 삭제된 컨테이너 확인 | `docker ps -a --filter name=volume-web-1` |
| 새 컨테이너에서 기존 데이터 확인 | `docker exec volume-web-2 cat ...` |

### 최종 결론

- 바인드 마운트는 개발 중 소스 코드 변경 사항을 실시간으로 반영하는 데 적합합니다.
- Docker 볼륨은 컨테이너 삭제 후에도 유지해야 하는 데이터를 저장하는 데 적합합니다.
- 컨테이너는 필요할 때 삭제하고 다시 생성할 수 있습니다.
- 소스 코드와 중요 데이터는 컨테이너 외부에 분리하여 보관할 수 있습니다.
- 여러 컨테이너와 마운트를 함께 구성할 때는 Docker Compose를 사용하면 설정을 파일로 관리할 수 있습니다.

</details>



