# 전화번호 뒷 4자리 운세 — 배포 안내

## 파일 (5개 전부 같은 폴더에)
- `index.html` — 페이지 본체
- `og.png` — 링크 미리보기 이미지 (1200×630)
- `bujeok.webp` — 부적 종이 배경
- `pouch_closed.webp` — 복주머니 (닫힘)
- `pouch_opened.webp` — 복주머니 (열림)

**이미지 4개가 없으면 화면이 깨집니다.** 반드시 index.html과 같은 폴더에 두세요.

## 배포 전 필수 수정 1가지

`index.html` 상단의 `https://REPLACE-ME.example` 를 **실제 도메인**으로 전부 바꿔주세요. (3군데)

```
<link rel="canonical" href="https://내도메인/">
<meta property="og:image" content="https://내도메인/og.png">
<meta name="twitter:image" content="https://내도메인/og.png">
```

OG 이미지 경로는 **반드시 절대 URL**이어야 카톡·인스타 미리보기가 뜹니다.

## 배포 방법 (택 1)

### Cloudflare Pages — 권장
1. GitHub 저장소에 `index.html`, `og.png` 업로드
2. Cloudflare Pages → Create a project → 저장소 연결
3. Build command 비움 / Output directory `/`
4. 배포 후 도메인 확인 → 위 3군데 수정 → 재배포

### Vercel
1. `vercel` CLI 또는 대시보드에서 폴더 드래그
2. Framework Preset: Other
3. 배포 후 도메인 수정 → 재배포

### GitHub Pages
1. 저장소 Settings → Pages → Branch `main` / `/root`
2. 주소는 `https://아이디.github.io/저장소명/`
3. 서브경로라서 `og:image`도 서브경로 포함해서 적어야 함

## 개인정보 처리

번호 뒷자리가 URL·서버 로그에 남지 않도록 **결과 코드로 치환**했습니다.

- 1698 → `?k=BVJW` (육안으로 번호 판별 불가)
- `<meta name="referrer" content="no-referrer">` 적용 — 외부 이동 시 주소 미전달
- 입력값은 브라우저에서만 계산되고 전송되지 않음

**배포 시 액세스 로그 보존 기간을 최소로 설정**해두세요.

## 배포 후 확인 체크리스트

- [ ] `?k=BVJW` 붙여서 열면 1698 결과가 뜨는가
- [ ] 결과가 뜨면 주소창이 `?k=` 로 바뀌는가
- [ ] 복주머니가 흔들리다 열리고 부적이 나오는가
- [ ] 이미지 저장 → PNG 다운로드되는가 (부적 배경이 들어갔는지 확인)
- [ ] 카톡에 링크 붙여넣기 → 미리보기 이미지 뜨는가
- [ ] 모바일에서 숫자 입력 시 자동으로 다음 칸 이동하는가
- [ ] 상단·하단 @adot.wiki 링크가 계정으로 연결되는가

미리보기가 안 뜨면 카카오톡 캐시 문제일 수 있습니다.
`https://developers.kakao.com/tool/debugger/sharing` 에서 캐시 초기화하세요.

## 인스타 운영

공유 버튼은 뺐습니다. **릴스에서 링크로 유입 → 결과 이미지 저장 → 각자 스토리 업로드** 흐름입니다.

- 프로필 링크에 걸고, 릴스·캐러셀 캡션에 "프로필 링크" 안내
- 스토리는 링크 스티커로 바로 연결
- 결과 이미지에 @adot.wiki 가 없으므로, 스토리 리포스트 시 계정 태그 유도

## 다음 단계 (반응 확인 후)

지금은 OG 이미지가 **모든 결과에 동일**합니다.
결과별로 다른 미리보기를 만들려면 서버 렌더링이 필요합니다.

- Cloudflare Workers + `@vercel/og` 또는 Satori
- `/og?n=1698` 로 결과 문장이 그려진 이미지를 실시간 생성
- 링크 오픈율이 크게 올라가지만, **반응이 확인된 뒤에** 붙이는 게 순서

