# 햄모찌 팬페이지 — 설치 안내

## 0. 폴더 구조
```
index.html          메인 (오르골 대시보드)
style.css           카테고리 공용 스타일
supabase.js         DB 연동 (⚠ 상단 2줄 수정 필요)
fx.js               공통 연출 (입자 · 클릭 · 페이지 전환 로딩)
supabase_all.sql    Supabase SQL Editor에 한 번에 Run

profile/            프로필
notice/             공지
schedule/           일정 (달력)
song/               노래책
work/               업보
dress/              옷장
diary/              추억창고 (사진 갤러리 + 라이트박스 + 댓글)
admin/              관리자
overlay/            OBS 오버레이 ("지금 트는 노래")
```

## 1. Supabase
1. New project 생성 → Settings → API 에서 **Project ID** 와 **anon public key** 복사
2. SQL Editor → `supabase_all.sql` 전체 붙여넣기 → **Run**
   - 맨 아래 INSERT가 햄모찌 기본 프로필 값까지 한 번에 넣어줌

## 2. 키 — ✅ 이미 채워져 있음
`supabase.js` 와 `overlay/index.html` 두 군데 모두 프로젝트 ID(`ykalffbeexzxmdyfvybk`)와 anon 키가 들어가 있어요.
프로젝트를 새로 만들면 이 두 파일만 다시 고치면 됩니다.

## 3. GitHub → Cloudflare Pages
- 폴더 구조 그대로 업로드 (`fx.js`는 반드시 **루트**)
- Cloudflare Pages → Connect to Git → repo 선택
- 빌드 설정 **비움** (Framework preset = None) → Deploy

## 4. SOOP 게시글 삽입
```html
<iframe height="2400" scrolling="no" src="배포주소" style="width:100%;border:0;display:block;"></iframe>
```

## 5. 관리자
- 주소: `배포주소/admin/`
- 비밀번호: **`1234`** (임시) — `admin/index.html`의 `const ADMIN_PASSWORD` 에서 변경
- ⚠ 비번은 소스에 그대로 보이니 **버리는 비번**으로 쓸 것

### 관리자 탭
| 탭 | 하는 일 |
|---|---|
| 🏠 메인 | 프사 · 프로필 정보 · 추가 정보 · 좋아/싫어 · 방송 요일 · 링크 |
| 🎀 프로필 | 한마디 · 하고픈 말 · 능력치 · 목표 · TMI · 사용설명서 · VOD |
| 📢 공지 / 📅 일정 / ⚡ 업보 / 👗 옷장 / 🎵 노래책 / 🖼 추억창고 | 각 페이지 내용 |
| ✉️ 문의 | 페이지 문의 모달로 들어온 글 |
| 🎨 테마 | 색 6종 팔레트 — 저장하면 전 페이지 색이 한 번에 바뀜 |

## 6. 자주 쓰는 규격
- **프사** — 관리자 메인 탭에 SOOP 아이디만 넣으면 자동. 직접 이미지 URL을 넣으면 그게 우선.
- **생일** — `MM.DD` (예: `10.17`). 메인 D-Day가 자동 계산됨.
- **방송 요일** — 체크한 요일만 "방송", 나머지는 자동 "휴방". (0=월 … 6=일)
- **이미지** — SOOP 비공개 게시판에 올린 뒤 사진 **우클릭 → "이미지 주소 복사"**
  (글 주소 ✗ / `https://stimg.sooplive.com/…` 직접 주소 ○)
- **옷장 사진** — 세로 3:4 (900×1200 권장)
- **VOD** — SOOP 다시보기 주소의 **숫자 ID만** 입력
- **추억창고** — 사진 격자로 보이고 누르면 크게 열려요(댓글 가능). 여기 올린 **최신 4장**이 메인 "모찌의 추억창고" 칸에도 자동으로 뜸
- **BGM** — 관리자 메인 탭에 mp3 직링크를 넣으면 메인 히어로의 ▶ 버튼이 실제로 재생.
  비워두면 애니메이션만 돎.

## 7. 아직 안 들어간 것 (다음 단계)
- **스탬프 · 룰렛 쿠폰 보상 시스템** — 테이블 설계 + 관리자 발급 화면이 따로 필요해서 별도 작업
- **자기소개 · 채팅규칙 본문** — 관리자 🎀프로필 탭 "모찌 사용설명서" 칸에 직접 적으면 바로 반영됨
- 유튜브 링크 — 아직 없다고 하셔서 뺐음. 생기면 말씀 주시면 추가

## 8. 재배포
바뀐 파일 덮어쓰기 → Commit → 1~2분 → 브라우저에서 **Ctrl+Shift+R**

## 9. 테마 색 (기본값)
| 변수 | 값 | 쓰임 |
|---|---|---|
| main | `#FFEE9C` | 버튼·배지·강조 배경 |
| main-dark | `#A8801F` | 제목·아이콘 |
| main-deep | `#8A6A18` | 카드 제목·라벨 |
| main-light | `#FFFBE0` | 테두리·연한 배경 |
| bg | `#FFF9E8` | 페이지 배경 |
| logo | `#8B6FC4` | 상단 로고 (라벤더) |

⚠️ 관리자 🎨테마 탭에서 색을 바꿀 때, **메인 색을 아주 밝게 하면 그 위 글자가 안 보일 수 있어요.**
밝은 색을 쓰면 `main-dark`·`main-deep`을 충분히 진하게 같이 맞춰주세요.
