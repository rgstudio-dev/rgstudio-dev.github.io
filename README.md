# RETRO GAMES STUDIO 프로젝트 가이드 & 배포 매뉴얼

본 문서는 **RETRO GAMES STUDIO** 랜딩 페이지 및 웹사이트의 성격, 프로젝트 구조, 배포 환경 설정 및 배포 절차를 정리한 매뉴얼입니다.

---

## 1. 프로젝트 성격 및 목적

### 1.1 개요
- **사이트명**: RETRO GAMES STUDIO
- **라이브 도메인**: [https://rgstudio-dev.github.io/](https://rgstudio-dev.github.io/)
- **목적**:
  - 80~90년대 아케이드/레트로 감성을 현대 기술로 재해석한 인디 게임 스튜디오의 공식 쇼케이스 랜딩 페이지입니다.
  - 스튜디오의 출시작 및 예정작(Solitaire, Flash Dodge 등)을 홍보합니다.
  - 글로벌 사용자 대응을 위한 다국어(한국어/영어) 지원을 제공합니다.
  - 광고 플랫폼 및 스토어 심사(Google Play, Toss 등)에 필요한 필수 정책 문서(`privacy.html`, `app-ads.txt` 등)를 호스팅하는 공식 루트 도메인 역할을 겸합니다.

### 1.2 주요 기술 스택
- **프론트엔드**: HTML5, CSS3, Vanilla JavaScript
- **디자인/스타일**:
  - CRT 모니터 오버레이 효과 (`crt-overlay`)
  - 사이버펑크/네온 스타일 및 3D Grid Floor 애니메이션
  - Web Fonts: `Orbitron`, `Press Start 2P`, `Outfit`
- **호스팅/인프라**: **GitHub Pages** (정적 웹 호스팅)
- **원격 저장소**: `https://github.com/rgstudio-dev/rgstudio-dev.github.io.git`

---

## 2. 프로젝트 디렉터리 구조

```text
c:\project\retrogamesstudio/
├── .git/                        # Git 버전 관리 디렉터리 (origin -> rgstudio-dev.github.io)
├── assets/                      # 게임 썸네일 및 미디어 리소스
│   ├── flash-dodge-thumb.png    # Flash Dodge 프로젝트 썸네일
│   └── solitaire-thumb.png      # Solitaire 프로젝트 썸네일
├── sajumeetslotto/              # '사주가 로또를 만났을 때' 앱 전용 문서
│   └── privacy-policy.html      # 개인정보처리방침 (URL: /sajumeetslotto/privacy-policy.html)
├── app-ads.txt                  # 구글 애드몹/애드센스 등 광고 매체 인증용 파일 (앱 수익화 필수)
├── googlebc1347cce702ff3d.html  # Google Search Console 소유권 인증 파일
├── privacy.html                 # 개인정보처리방침 기본 문서
├── privacy_google.html          # Google Play 스토어 제출용 개인정보처리방침
├── privacy_toss.html            # Toss 앱 연동/인앱 서비스용 개인정보처리방침
├── index.html                   # 메인 랜딩 페이지 마크업
├── style.css                    # 레트로/CRT 테마 및 반응형 레이아웃 스타일시트
├── main.js                      # 스크롤 인터랙션, 글리치 애니메이션, i18n(KO/EN) 로직
└── README.md                    # 본 안내 문서
```

> **주의 사항**:
> `app-ads.txt`, `privacy*.html`, `google*.html` 파일들은 앱 스토어 심사 및 광고 수익화, 검색 엔진 인증과 직접 연결되어 있으므로 절대 실수로 삭제되지 않도록 주의해야 합니다.

---

## 3. 원격 저장소 및 배포 환경 설정

현재 로컬 작업 폴더(`retrogamesstudio`)는 GitHub Pages의 루트 저장소와 연동되어 있습니다.

- **저장소 URL**: `https://github.com/rgstudio-dev/rgstudio-dev.github.io.git`
- **배포 브랜치**: `main`
- **배포 방식**: GitHub Pages 설정에서 `main` 브랜치의 루트(`/`) 경로를 웹 호스팅하도록 구성됨.
  - 즉, `main` 브랜치에 코드를 `git push`하면 수 분 이내에 [https://rgstudio-dev.github.io/](https://rgstudio-dev.github.io/)에 자동 배포됩니다.

---

## 4. 작업 및 배포 워크플로우

### 4.1 로컬 작업 전 최신 상태 동기화
새로운 작업을 시작하기 전에 원격 저장소의 최신 커밋을 가져옵니다:
```powershell
git pull origin main
```

### 4.2 로컬 개발 및 테스트
별도의 빌드 과정(Webpack, Vite 등)이 필요 없는 순수 HTML/JS 정적 페이지이므로, 브라우저에서 `index.html`을 바로 열거나 Live Server(VS Code 확장 등)를 통해 실시간으로 확인하며 작업합니다:
```powershell
# 기본 브라우저로 index.html 열기 (PowerShell)
Start-Process index.html
```

### 4.3 변경사항 확인 및 커밋
작업 완료 후 변경사항을 확인하고 스테이징합니다:
```powershell
# 변경 상태 확인
git status

# 변경된 차이점 확인
git diff

# 원하는 파일 스테이징
git add index.html main.js style.css

# 커밋 생성 (커밋 메시지는 영문 작성 권장)
git commit -m "Update landing page content and styles"
```

### 4.4 GitHub Pages 배포 (Push)
커밋한 내용을 원격 `main` 브랜치로 푸시하면 즉시 배포가 트리거됩니다:
```powershell
git push origin main
```
*푸시 완료 후 1~3분 뒤에 `https://rgstudio-dev.github.io/`에 접속하여 반영 결과를 확인합니다.*

---

## 5. 유지보수 및 참고사항

1. **다국어(i18n) 텍스트 추가/수정**
   - 신규 텍스트 추가 시 `index.html` 태그에 `data-i18n="키이름"` 속성을 부여합니다.
   - `main.js` 내부의 `translations.ko` 및 `translations.en` 객체에 대응되는 번역 쌍을 함께 등록해야 합니다.
2. **연결 링크 주의**
   - `index.html` 내에서 다른 프로젝트(예: `flash-dodge`)나 외부 링크를 연결할 때는 상대 경로(`../`) 대신 배포된 전체 URL(예: `https://rgstudio-dev.github.io/flash-dodge/`)을 사용하거나 저장소 배포 구조에 맞게 설정해야 링크 깨짐을 방지할 수 있습니다.
