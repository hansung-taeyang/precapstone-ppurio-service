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

백엔드 DB 구동 시 Docker와 본 저장소에 있는 `compose.db.yml` 스크립트를 사용합니다. 백엔드 저장소에 있는 [README](https://github.com/hansung-taeyang/node-backend/blob/main/README.md)를 참고하세요.

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
