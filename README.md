# Velvet Room — Persona Playlist

유튜브 재생목록을 3D 카드 캐러셀로 탐색하는 단일 파일 웹 앱입니다.

🌐 **데모**: https://ring-experimental.github.io/velvet-playlist/

## 특징

- **HTML-in-Canvas 렌더링** — 카드, 타이틀 패널, 트랜스포트 바를 모두 캔버스 안의 DOM 요소로 만들고 `drawElementImage`로 합성합니다.
- **3D 카드 캐러셀** — 원근 투영 + `rotateY`로 카드 스트립을 잘라 그리며, 드래그·관성·스냅을 지원합니다.
- **실시간 YouTube 플레이어** — 임베드 플레이어는 크로스오리진 제약 때문에 실제 DOM 레이어로 분리하고, 캔버스 카드와 동일한 3D 포즈로 동기화합니다.
- **썸네일 기반 컬러 추출** — 현재 곡의 커버에서 지배색을 추출해 액센트 슬래브·배경 그라디언트에 실시간 반영합니다.
- **슬래시 트랜지션** — 곡 전환 시 타이틀 패널이 대각선으로 잘려 나가고 새 제목이 뒤에서 쓸어 들어옵니다.
- **반응형 레이아웃** — 모바일 세로 / 데스크톱 배치를 자동 전환하고 안전 영역(safe-area)을 반영합니다.
- **접근성** — 키보드 탐색(←/→, Space, M), 라이브 리전 알림, 포커스 링, `prefers-reduced-motion` 대응을 포함합니다.

## 사용 방법

1. 저장소 루트의 `index.html`을 그대로 사용합니다 (빌드 불필요, 의존성 없음).
2. 로컬에서 열 때는 `file://` 대신 로컬 서버를 쓰세요 (YouTube 임베드 제약):
   ```bash
   npx serve .
   ```
   GitHub Pages 배포본은 `https://` 주소로 열어 주세요.
3. 조작: 카드 드래그 / 휠 / ← → 키로 곡 이동, Space로 재생·일시정지, M으로 음소거 토글, 카드 클릭으로 선택·재생.

## 요구 사항

| 항목 | 내용 |
| --- | --- |
| 브라우저 | **Chrome Canary** 및 `drawElementImage` 지원 빌드 |
| 플래그 | `chrome://flags/#canvas-draw-element` 활성화 |
| 주소 | `file://`에서는 YouTube 임베드 미지원 → `http(s)` 필요 |

`drawElementImage`를 지원하지 않는 브라우저에서는 안내 문구만 표시됩니다.

## 배포 (GitHub Pages)

```bash
gh repo create ring-experimental/velvet-playlist --public --source . --push
gh api -X POST repos/ring-experimental/velvet-playlist/pages -f source[branch]=main -f source[path]=/
```

Pages는 저장소 루트의 `index.html`을 정적 파일로 그대로 서빙합니다.

## 플레이리스트

재생목록 ID `PLVbc8DqsLqEYywbRnDeZSUV5gr2LmyzzN` 이 코드 상단의 `PLAYLIST_ID` 상수로 정의되어 있습니다. 다른 재생목록을 쓰려면 이 값을 바꾸면 됩니다. 영상 제목/채널 정보는 oEmbed → noembed 순으로 조회합니다.

## 라이선스

자유롭게 사용·수정해 주세요.
