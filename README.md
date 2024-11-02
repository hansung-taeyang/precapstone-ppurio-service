# precapstone-2024

## 본 저장소 설명 및 클론 방법

```bash
$ git clone --recurse-submodules https://github.com/hansung-taeyang/precapstone-ppurio-service.git 원하는-폴더명
```

본 저장소는 `flutter-frontend`와 `node-backend` 저장소를 서브모듈로 가지고 있습니다. 위 명령어로 클론하면 서브모듈도 함께 클론됩니다.

- `flutter-frontend`: 플러터 프론트엔드 저장소. Android Studio로 열어서 작업.
- `node-backend`: 노드 백엔드 저장소. 원하는 IDE로 열어서 작업.
- 본 저장소: 프로젝트 전체를 관리하는 저장소.

개발 시 위에서 언급한 두 개의 저장소를 별도로 열어서 작업하면 됩니다. 어떤 저장소를 열었는지 헷갈리지 않게 주의해주세요.

`flutter-frontend`와 `node-backend` 폴더를 따로 열어서 작업할 때, 브랜치가 `dev`인지 **꼭!!** 확인하세요. Detached HEAD인 상태라면 현재 브랜치가 `dev`가 아닌 커밋 해시 값으로 되어 있습니다.

## 프론트 - 백엔드 연동 방법

**node-backend 저장소!!** 를 기준으로 설명합니다. 해당 폴더를 VS Code에서 열어서 내장 터미널을 열던, 별도의 콘솔 창을 열어서 하던 설명은 `node-backend`를 기준으로 합니다.

> 명령어 - 설명 순으로 적혀있습니다. 잘 읽어주세요.
> 명령어는 `$` 뒤에 써져 있는 것들을 말합니다! 예시) `$ git pull` 이라면 `git pull`이 입력할 명령어

```shell
$ docker -v 
Docker version 27.1.1, build 6312585
```

[Docker](https://www.docker.com/) 설치 후 실행합니다. 터미널(콘솔 창)을 열어서 `docker -v`로 버젼 확인합니다.

> Docker는 리소스를 많이 잡아 먹을 수도 있으니, 개발 시 Docker Desktop을 실행하여 백그라운드에서 돌아가게 해주고, 더 이상 사용하지 않을 때에는 작업 표시줄의 Docker 아이콘을 우클릭, `Quit Docker Desktop`으로 잘 종료하면 됩니다.

```shell
$ node -v
v20.14.0
```

그리고 [Node.js](https://nodejs.org/en/download/prebuilt-installer)에서 **v20.xx.x(LTS)** 버젼을 설치합니다. 이미 깔려있다면 스킵해도 됩니다. 다만 **v20(LTS)** 이상의 버젼이어야 합니다. 마찬가지로 위의 명령어로 설치 확인합니다.

```shell
$ git pull
Already up to date.

$ npm install

up to date, audited 417 packages in 1s

74 packages are looking for funding
  run `npm fund` for details

2 low severity vulnerabilities

To address all issues, run:
  npm audit fix

Run `npm audit` for details.
```

우선 백엔드의 최신 커밋을 `pull` 해옵니다.

그 후 백엔드 가동에 필요한 npm 패키지들을 설치해줍니다.

```shell
$ docker ps
CONTAINER ID   IMAGE       COMMAND                   CREATED      STATUS              PORTS                               NAMES
f136fc2b1512   mysql:lts   "docker-entrypoint.s…"   3 days ago   Up About a minute   33060/tcp, 0.0.0.0:3307->3306/tcp   db

$ docker volume ls
DRIVER    VOLUME NAME
local     db_data
```

그 후 위의 명령어를 실행하여 Docker 컨테이너와 볼륨(데이터 저장용 파일)이 이미 돌아가고/존재하는지 확인합니다.

만약에 `db` 이름의 컨테이너 (`docker ps`의 실행 결과에서 오른쪽 끝 열의 NAMES에 해당하는 이름)과 `db_data` (`docker volume ls`의 실행 결과에서 VOLUME NAME`)가 없다면 다음 단계로 건너 뛰어도 좋습니다.

```shell
$ docker container stop db
db

$ docker container rm db
db

$ docker volume rm db_data
db_data
```

만약에 이전 단계에서 해당사항이 있다면, 위의 명령어로 컨테이너와 볼륨을 지워줍니다.

---

### 매우 중요
백엔드 팀원으로부터 `.env` 파일을 제공받아 `node-backend` 폴더 안에 바로 둡니다. 다른 폴더 안이 아니라, 바로 안에 두어야합니다!

---

```shell
$ docker-compose -f ../compose.db.yml up -d
[+] Running 2/2
 ✔ Volume "db_data" Created
 ✔ Container db     Started

$ npx drizzle-kit migrate
No config path provided, using default 'drizzle.config.js'
Reading config file 'D:\Dev\Computer-Sceience\Year3\PRECAP_TEST\node-backend\drizzle.config.js'
[dotenvx@1.14.0] injecting env (0) from .env

$ npm run dev

> back-node@1.0.0 dev
> dotenvx run -- tsx watch src/index.ts

[dotenvx@1.14.0] injecting env (11) from .env
[dotenvx@1.14.0] injecting env (0) from .env
[21:59:38.876] INFO (18244): Server running on http://localhost:3000
```

마지막으로 위의 명령어를 실행하여 MySQL DB를 Docker에서 실행시켜두고, 백엔드 서버를 가동합니다.

> `npx drizzle-kit migrate`에서 출력되는 경로명은 당연히 이 문서의 것과 다릅니다! 걱정하지 마세요.

## 주요 백엔드 API 주소

- `localhost:3000/v1/signIn`: 로그인 주소
- `localhost:3000/v1/signUp`: 회원가입 주소
- `localhost:3000/v1/image` : 이미지 생성 API
- `localhost:3000/docs`: 백엔드 API 명세를 웹 브라우저에서 볼 수 있는 주소
- 문자 기록 조회 주소는 추가 예정입니다.

요청 방식은 `/docs` 참조 및 백엔드 팀원에게 문의하세요.

## Visual Studio Code profile 참고
프로젝트 루트에 있는 `Pre-capstone.code-profile`은 VS Code의 Profile 기능에서 Import(불러오기) 가능한 파일입니다. 본 프로젝트에 필요한 익스텐션이나 일부 세팅같은게 준비되어있으니 직접 불러오셔서 마음에 맞게 수정해서 쓰면 됩니다.

본 프로필에는 [Comment Anchors](https://marketplace.visualstudio.com/items?itemName=ExodiusStudios.comment-anchors) 익스텐션이 설치되어 있습니다.

```md
// NOTE Some note...
// TODO Something to do...
```

<img src="/assets/comment-anchor.png" alt="comment anchor" width="500" />

위와 같은 형식으로 작성하면 에디터 왼편에 닻 아이콘이 떠서 중요한 주석들을 쉽게 확인 가능합니다. 사이드 바의 닻 아이콘을 누르면 리스트로도 주요한 주석들을 모아 볼 수 있습니다. 자세한 내용은 위 링크를 참조하세요.

<img src="/assets/thunder-client.png" alt="thunder client" width="700" />

또한 [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) 도 설치되어 있습니다. API 테스트 시 간편하게 UI로 테스트해 볼 수 있습니다. 사이드 바에 번개 아이콘을 클릭하면 사용할 수 있습니다.

---

<img src="/assets/profile.png" alt="profile" width="500" />

프로필을 불러오려면 사이드 바 최하단 아이콘 - Profiles를 클릭하여 프로필 리스트를 열어볼 수 있습니다.

<img src="/assets/profile2.png" alt="profile2" width="500" />
프로필은 위 스크린샷처럼 불러올 수 있고, 프로필을 선택해서 사용하려면 불러온 프로필 리스트에서 체크 ✓ 표시를 눌러 사용하면 됩니다.