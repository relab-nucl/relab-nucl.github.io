# RELAB Homepage

전북대학교 양자시스템공학과 **Reactor and Energy Systems Laboratory (RELAB)** 홈페이지 소스입니다.
단일 `index.html` 파일로 구성된 정적 사이트이며, 별도 설치나 빌드 과정 없이 동작합니다.

## 1. 로컬에서 열어 보기
`index.html`을 더블클릭하면 브라우저에서 바로 열립니다. (인터넷 연결 시 Google Fonts가 적용되고, 오프라인이면 시스템 기본 폰트로 표시됩니다.)
터미널에서 `python3 -m http.server 8765`를 이 폴더에서 실행한 뒤 `http://localhost:8765`로 접속해도 됩니다.

## 2. 배포 (GitHub Pages)
- 공개 주소: **https://jykimth95.github.io/relab-homepage/**
- 저장소: https://github.com/jykimth95/relab-homepage (`main` 브랜치 `/ (root)`에서 Pages 자동 빌드)
- 파일을 수정한 뒤 아래 세 줄을 실행하면 1~2분 안에 사이트에 반영됩니다.

```bash
git add -A
git commit -m "내용 수정"
git push
```
- 처음 쓰는 컴퓨터에서는 `gh auth login`(GitHub CLI) 또는 GitHub Desktop으로 로그인한 뒤 push 하세요.

## 3. 자주 하는 수정

### 3.1 논문 추가 (Publication)
`index.html`에서 `id="pane-journal"`(저널), `id="pane-conf"`(학회), `id="pane-patent"`(특허)를 찾아 `<ul class="pubs">` 안에 아래 형식의 `<li>`를 **맨 위**에 추가합니다(최신순).

```html
<li><span class="yr">2026</span><div><b>논문 제목</b><span>저자1, 저자2, <i>Journal Name</i>, Vol. 00, pp. 000–000 — DOI</span></div></li>
```

### 3.2 구성원 추가 (Members)
`id="members"` 아래 `<div class="people">` 안에 추가합니다.

```html
<div class="person"><div class="av">Photo</div><b>홍길동</b><span>M.S. Course</span><i>연구 주제</i></div>
```
사진은 `images/members/` 폴더에 영문 파일명(예: `hong_gildong.jpg`, 긴 변 600px)으로 넣고
`<img class="av" src="images/members/hong_gildong.jpg" alt="홍길동" loading="lazy">`로 씁니다. (CSS가 원형으로 잘라 보여 줍니다.)

### 3.3 교수 정보 / 연락처
- 히어로 영역 `class="profile"` 내부의 `<dl>`에서 이메일·전화·호실을 수정합니다.
- footer(`id="contact"`)의 Contact 블록도 같은 내용으로 맞춰 주세요.
- 교수 사진: `<div class="photo">…</div>`를 `<img class="photo" src="images/professor.jpg" alt="Prof. Ji Yong Kim">`로 교체.

### 3.4 갤러리 사진
`id="gallery"`의 `<div class="gallery">` 안에 아래 형식의 `<figure>`를 **맨 앞**에 추가합니다(최신순). 사진은 `images/gallery/`에 긴 변 1200px 정도로 줄여 넣습니다.

```html
<figure><img src="images/gallery/2026-12_event.jpg" alt="설명" loading="lazy"><figcaption><b>2026.12</b>행사 이름</figcaption></figure>
```
(CSS가 `aspect-ratio: 4/3`로 잘라 보여 주므로 비율이 달라도 괜찮습니다. 8장 넘게 넣어도 됩니다.)

### 3.5 Research Topics 수정
`id="research"` 섹션의 `<ul class="topics">` 항목을 수정합니다. 번호(`<span class="n">01</span>`)는 순서대로 유지합니다.

## 4. 디자인 변경
- 색상은 `<style>` 최상단 `:root` 변수(`--navy`, `--teal` 등)만 바꾸면 전체에 적용됩니다.
- 메뉴 항목은 `<nav class="main">`(데스크톱)과 `<div class="mobile">`(모바일) **두 곳**을 함께 수정해야 합니다.

## 5. 파일 구성
```
index.html   사이트 전체
CLAUDE.md    Claude Code 작업 맥락
README.md    이 문서
images/      사진 (생성 필요)
```

## 6. 문의
RELAB 관리자: 김지용 교수 (양자시스템공학과)
