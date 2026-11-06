# RELAB Homepage — 작업 맥락 (Claude Code용)

## 프로젝트 개요
- 전북대학교 양자시스템공학과 **RELAB (Reactor and Energy Systems Laboratory)** 연구실 홈페이지.
- 책임자: 김지용 조교수 (원자력 열수력·안전 전공). 영문 표기는 **Ji Yong Kim** (Jiyong 아님).
- 참고 모델: UNIST NETHS 연구실 홈페이지(https://neths.unist.ac.kr) — 메뉴 구조와 메인 페이지 구성을 그대로 따름.
- 콘텐츠 원본: 기존 노션 홈페이지(https://lyrical-chiller-e67.notion.site/relab)와 CV(`04. 기타/02. Curriculum Vitae/CV_Template_JY.tex`). 2026-11-06 기준 People·Projects·Publication·Join us·News를 옮겨 왔음.
- 현재 상태: 단일 정적 파일 `index.html` (HTML + CSS + JS 인라인). 빌드 도구 없음.
- 위치: Dropbox `05. RELAB/Homepage/`. 로컬 미리보기는 `.claude/launch.json`의 `relab-site`(python http.server, 포트 8765).

## 파일 구조
```
index.html   # 전체 사이트 (단일 페이지, 해시 앵커로 섹션 이동)
CLAUDE.md    # 이 파일
README.md    # 운영자/학생용 수정 가이드
images/      # relab_logo.png(헤더 로고), professor.jpg(교수 사진), members/*.jpg(구성원 증명사진, 600px)
             # research_overview.webp (Overview 하단 연구 개요 그림, 1800px, 흰 배경을 투명 처리, 사용자 제공)
             # gallery/*.jpg (노션 Gallery 전체 23개 행사 + 메인 페이지 수상 사진 1장 = 24장, 행사당 1장, 긴 변 1200px, 파일명 YYYY-MM-DD.jpg)
             # Gallery는 최신 8장만 보이고 "View all photos" 버튼(#gal-more)으로 .more-item을 펼침
             # 원본: Dropbox 05. RELAB/연구실 로고, 05. RELAB/서명 및 사진/{교수 증명사진, 학생 증명사진}
qr/          # 홈페이지 QR (relab_qr.png 기본, relab_qr_logo.png 로고 삽입, relab_qr.svg 벡터, relab_qr_card.png 포스터용). 생성: python qrcode+zxing-cpp, 오류정정 H, 남색 #004287
data/        # (예정) members.json, publications.json 등 데이터 분리 시 사용
```

## 디자인 규칙 (반드시 유지)
- 브랜드 색상: **navy `#004287`**, **teal `#66D7D5`** (RELAB PPT 템플릿과 동일). CSS 변수 `--navy`, `--teal`로 정의되어 있음.
- 폰트: Noto Sans KR(본문, 한글) + Montserrat(영문 제목/숫자). Google Fonts만 외부 로드.
- 외부 스크립트·이미지 URL 사용 금지 — 이미지는 `images/` 로컬 파일로.
- 반응형 브레이크포인트: 960px(태블릿), 600px(모바일). 새 섹션 추가 시 두 미디어쿼리에 그리드 규칙 추가.

## 페이지 구조 (섹션 id)
`#home`(히어로: 교수 프로필 카드 + Welcome) → Introduction 3단 카드 → `#news`(Recent News 3건) → `#research`(Overview + Research Topics 4개 + 통계 3개: SCIE·특허·학부연구생) → `#projects`(Ongoing/Past) → `#people`(히어로와 같은 교수 프로필 카드 `.profile.people-prof`(id=professor) + 학력·경력·수상 `.prof-grid` → `#members` = Graduate Researchers(대학원생, 현재는 모집 안내 `.recruit` 박스만) → Members·학부연구생 카드 → `#alumni`) → `#publication`(Journal / Conference / Patent 탭) → `#gallery` → `#joinus` → `#contact`(footer). (Links·Lab Facility 섹션은 사용자 요청으로 삭제)
- 섹션 배경은 흰색/`.alt`(회색)를 번갈아 사용. 새 섹션을 끼워 넣으면 이후 섹션의 `alt` 클래스를 다시 맞출 것.
- 헤더 브랜드(`.brand`)는 링크가 아님(사용자 요청). 로고 옆 두 줄 문구는 600px 이하에서 숨김. 데스크톱 메뉴는 1100px 이하에서 햄버거로 전환.

## 콘텐츠 규칙
- **URI-SMR(urismr.or.kr) 관련 내용은 넣지 않는다.** (사용자 요청으로 제거됨)
- Research Topics 4개: ① 시스템 안전해석(MARS-KS·RELAP5·SPACE) ② 비등 열전달·CHF ③ 차세대 원자로 열수력(MSR·PCSG) ④ 통합 에너지 시스템(Modelica)·원전 탄력운전. **인공지능(AI) 연구 내용은 넣지 않는다** (사용자 요청, 2026-11-06). 히어로 인용문·Join us·Facility 카드에서도 제거함.
- 구성원·논문·특허는 **실제 정보만** 기입. 임의 생성 금지.
- 구성원 6명은 전원 학부연구생(Undergraduate Researcher). 카드 순서: 박하영-김태우-오상훈-유재운-임형석-문민기 (사용자 지정). 박하영 사진은 원본의 검은 테두리를 잘라낸 것. Alumni는 이동호만 표시 (임혜윰·노혜민은 사용자 요청으로 제외).
- Publication은 CV 기준. SCIE 10·KCI 2는 DOI 링크(새 탭), Under review 3건 포함, 학회 41건(KNS 2026 추계 2건은 2026-11-06 사용자 제공으로 추가, 임형석 발표는 Best Poster Award 표기)·특허 4건은 링크 없음. "in preparation" 항목은 싣지 않음.
- 언어: 영문 메뉴/제목 + 한글 본문 혼용 (NETHS 방식).

## 채워야 할 자리표시자
- Footer SNS 링크 (현재 `#`). 교수 개인 링크(Google Scholar, LinkedIn)는 히어로 프로필 카드의 아이콘으로 들어가 있음.
- 상단 유틸바: 전북대학교(jbnu.ac.kr), 양자시스템공학과(atom.jbnu.ac.kr) 링크 반영 완료.

## 향후 계획
1. ~~GitHub Pages 호스팅~~ → 완료(2026-11-06): 저장소 `relab-nucl/relab-nucl.github.io` (GitHub 조직 relab-nucl, 소유자 jykimth95), 공개 주소 https://relab-nucl.github.io/ . `main`에 push하면 자동 배포.
2. 구성원·논문 데이터를 `data/*.json`으로 분리하고 JS로 렌더링 → 학생이 HTML을 건드리지 않고 JSON만 수정.
3. (선택) 노션 DB → GitHub Actions → JSON 자동 갱신.

## 작업 시 주의
- 수정 후 브라우저에서 데스크톱/모바일 폭 모두 확인.
- Publication 탭 전환 JS(`showPane`)와 네비게이션 `data-tab` 속성은 연동되어 있으므로 탭 id(`journal`, `conf`, `patent`) 변경 시 양쪽 모두 수정.
