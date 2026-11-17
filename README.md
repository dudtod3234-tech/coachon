# 코치온 V35 — GitHub Pages 최종 배포 묶음 (링크별 OG 이미지)

⚠️ 공개 GitHub 저장소의 HTML/JavaScript와 정적 파일은 누구나 볼 수 있습니다. **service_role, 비밀번호, 알림톡 키, 실제 회원 정보를 업로드하지 마세요.** 회원 데이터 보안은 Supabase RLS/RPC가 책임집니다.

## 각 입구의 제목 및 미리보기

| 구분 | 공유 URL | OG 제목 | 파일 |
|---|---|---|---|
| 관리소 | `https://dudtod3234-tech.github.io/{저장소}/` | 코치온 관리소 | `og.png` |
| 기존 회원 | `https://dudtod3234-tech.github.io/{저장소}/m/?c=cheongsa` | 코치온 | `og-member.png` |
| 신규 신청 | `https://dudtod3234-tech.github.io/{저장소}/new/` | 슬기코치 레슨 신청 | `og-new.png` |
| 피드백 카드 | `https://dudtod3234-tech.github.io/{저장소}/card/?t=토큰` | 코치온 피드백 카드 | `og-card.png` |

이미지는 모두 제공된 원본을 비율 유지한 상태로 1200×630 PNG로 변환했습니다. 회원 이름·토큰은 OG 메타에 포함되지 않습니다. 앱 본체는 이전 V34를 유지합니다.

## GitHub Pages 배포 (저장소 이름 몰라도 OG URL 자동 완성)

1. ZIP 압축을 풀어 **폴더 안 내용물 전체를 저장소 루트**에 업로드합니다. `.github/workflows/deploy-pages.yml`, `new/index.html`, `m/index.html`, `card/index.html` 등 하위 폴더도 업로드해야 합니다. 숨김 파일 `.nojekyll`도 포함하세요.
2. GitHub 저장소 **Settings → Pages → Build and deployment → Source**를 **GitHub Actions**로 선택합니다. 이전의 **Deploy from a branch** 설정으로는 OG 주소의 `REPOSITORY_NAME`이 자동으로 변경되지 않습니다.
3. `main`에 업로드/커밋하면 **Actions → Deploy COACH ON to GitHub Pages** 워크플로가 실행됩니다. 성공 시 Pages 주소를 엽니다.
4. 이 워크플로가 계정명과 저장소명을 읽어서 OG `og:image`, `og:url`의 절대 HTTPS 주소를 자동으로 채웁니다. 저장소명이 `{계정}.github.io`이면 루트 주소(`/`)로 처리합니다.
5. Supabase Authentication → URL Configuration에 새 GitHub Pages 주소(필요한 Redirect URLs)를 등록하고 `window.COACHON_PUBLIC`의 공개 anon 키/URL만 올바르게 설정하세요. 다른 서버 설정과 접근 권한은 별도 확인이 필요합니다.

### GitHub Actions를 사용하지 않고 브랜치 직접 배포할 경우

`index.html`, `new/index.html`, `m/index.html`, `card/index.html`의 `https://dudtod3234-tech.github.io/REPOSITORY_NAME/` 를 실제 배포 기본 주소로 **직접 바꿔야** 합니다. 그렇지 않으면 카카오톡 OG 이미지가 나타나지 않습니다.

### 카카오톡 공유 테스트

- 카카오톡에 **새 폴더형 URL** (`/new/`, `/m/?c=...`, `/card/?t=...`)을 공유하세요. `?new` 등 루트 쿼리 링크는 모두 같은 관리소 OG를 보여줄 수 있습니다.
- 이미 공유한 URL은 카카오톡의 캐시 때문에 이전 이미지가 남을 수 있습니다. [카카오 개발자 도구 공유 디버거](https://developers.kakao.com/tool/debugger/sharing)에서 해당 URL 캐시 초기화 후 재공유하세요.
- `/new` 같은 예전 404 경유 주소는 OG 공유용으로 쓰지 마세요.
- 카카오톡 미리보기는 실제 배포된 페이지에서만 검증할 수 있습니다. GitHub Actions의 배포 결과와 카카오 캐시는 로컬 검사만으로 검증할 수 없습니다.

## 검사 범위와 보안

OG 정적 메타, 이미지 1200×630, HTML 및 인라인 JS 구문을 정적으로 검사했습니다. 모바일/카카오톡 실제 공유 및 Supabase 접속/권한은 실서비스 검증 전입니다.
