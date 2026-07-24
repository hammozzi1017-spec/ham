# 햄모찌 (HAMMOZZI) 팬페이지 — DREAM ARCHIVE

## 폴더 구조
```
index.html          메인 (받은 디자인 그대로)
style.css           메인 CSS(원본 유지) + 서브 공통 디자인 시스템
supabase.js         ← 상단 2줄 교체 필요
fx.js               공통 연출 (루트에 있어야 함)
supabase_setup.sql  Supabase SQL Editor에 통째로 Run
assets/hammozzi-memory.webp

profile/   schedule/   song/   notice/   memory/   closet/
admin/     overlay/
```

| nav 이름 | 폴더 | DB 테이블 |
|---|---|---|
| PROFILE | `profile/` | `profile` (id=1, JSONB) |
| SCHEDULE | `schedule/` | `schedule` |
| SONG BOOK | `song/` | `songs` |
| NOTICE | `notice/` | `notice` |
| MEMORY | `memory/` | `diary` + `comments` |
| CLOSET | `closet/` | `dress_items` |

## 셋업 순서
1. **Supabase** — New project → `supabase_setup.sql`을 SQL Editor에 붙여넣고 Run
   (`viewers` / `upbo_*` 테이블은 이번 사이트에서 안 쓰지만 그냥 둬도 무해)
2. **`supabase.js` 상단 2줄** 교체
   ```js
   const SUPABASE_URL  = 'https://{{SUPABASE프로젝트ID}}.supabase.co';
   const SUPABASE_ANON = '{{SUPABASE_ANON_KEY}}';
   ```
   `{{버킷이름}}`도 같이 (이미지 업로드 안 쓰면 아무 값이나)
3. **`admin/index.html`** 안 `ADMIN_PASSWORD` = `{{관리자비밀번호}}` → 버리는 비번으로
4. **`overlay/index.html`** 안 `createClient(...)` 2개 값도 같이 교체
5. **각 페이지 footer** `{{이메일}}` → 실제 문의 메일 (없으면 `문의 버튼을 이용해 주세요`)
6. GitHub 업로드 → Cloudflare Pages (Framework: None) → Deploy

## admin 탭
🏠 메인 · 🎀 프로필 · 📢 공지 · 📅 일정 · 🎵 노래책 · 📔 메모리 · 👗 옷장 · ✉️ 문의 · 🎨 테마

- **🎨 테마** 탭에서 색 6종을 바꾸면 **서브 페이지 전체**에 즉시 반영 (메인은 사진 배경 디자인이라 영향 없음)
- **🏠 메인 > 방송 시간 · 메인 화면** 카드에서 메인의 `NEXT LIVE` / `LIVE` 값과 배경 일러스트를 교체
- **방송 요일** 체크: `0=월 … 6=일`

## 분류(옷장) 바꿀 때 — 세 곳 동시 수정
1. `closet/index.html` 의 `const CATS`
2. `admin/index.html` 의 `<select id="dr-cat">` 옵션
3. `admin/index.html` 의 `const DRESS_CATS`

## SOOP 게시글 삽입
```html
<iframe height="2400" scrolling="no" src="배포주소" style="width:100%;border:0;display:block;"></iframe>
```

## 연출 (fx.js)
맨 위 4줄만 바꾸면 모양이 바뀝니다.
```js
var FX_FLOAT = ['♡','✦','♡','✧','·','✦'];
var FX_CLICK = '♡';
var FX_COUNT = 13;
var FX_TILT  = true;
```
