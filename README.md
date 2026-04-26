# 성가대 연습 영상 링크 공유

교회 성가대 대원들과 주차별 파트 연습 유튜브 링크를 공유하는 웹앱입니다.

**라이브 주소:** https://warabica.github.io/choir/

---

## 화면 구성

### 메인 화면
- 우측 상단에 **늘감사 성가대** 배지 표시
- 세 개의 버튼 제공:
  1. **연습 영상 보기** → 주차별 파트 연습 링크 조회
  2. **늘감사 성가대 영상 보기** → 최근 공연 영상 5개 조회
  3. **링크 입력 (관리자)** → 주차 데이터 입력

---

## 사용 방법

### 대원 (일반 사용자)
1. 지휘자/관리자에게 받은 링크를 클릭합니다.
2. 주차를 선택하면 파트별 유튜브 링크가 표시됩니다.
3. 원하는 파트 카드를 클릭하면 유튜브가 열립니다.
4. 등록된 경우 하단에 **지난 주 늘감사 영상** 카드도 표시됩니다.

### 늘감사 성가대 영상 보기 (일반 사용자)
1. 메인 화면 → **늘감사 성가대 영상 보기** 버튼 클릭
2. 관리자가 마지막으로 저장한 시점 기준 최근 **늘감사 성가대 공연 영상 5개**가 카드로 표시됩니다.
3. 카드를 클릭하거나 **▶ 열기** 버튼을 누르면 YouTube가 열립니다.
4. YouTube API Key 없이도 바로 확인할 수 있습니다.

---

### 관리자 (링크 입력)

#### 1단계: GitHub PAT 발급
1. GitHub → 우상단 프로필 → **Settings**
2. 좌측 하단 **Developer settings** → **Personal access tokens** → **Tokens (classic)**
3. **Generate new token (classic)** 클릭
4. Note: `choir-app`, Expiration: 원하는 기간 설정
5. Scope: **`public_repo`** 체크
6. **Generate token** 클릭 → 토큰 값 복사 (한 번만 표시됨!)

#### 2단계: YouTube API Key 발급 (영상 검색용)
1. [Google Cloud Console](https://console.cloud.google.com/) → 프로젝트 생성
2. **API 및 서비스** → **라이브러리** → `YouTube Data API v3` 활성화
3. **사용자 인증 정보** → **API 키 만들기** → 복사
4. 앱의 관리자 화면 `YouTube API Key` 입력란에 붙여넣고 저장

#### 3단계: 앱에서 PAT / API Key 입력
1. 웹앱 메인 화면 → **링크 입력 (관리자)** 버튼
2. `Personal Access Token` 및 `YouTube API Key` 입력 후 각각 **저장** 클릭
3. 브라우저에 저장되므로 다음부터는 자동 입력됨

#### 4단계: 주차 링크 입력
1. 주차 번호, 곡 이름 입력
2. **영상 찾기** 버튼으로 유튜브 자동 검색 후 파트별 영상 선택 (여러 번 실행 가능)
3. 또는 각 파트 링크를 직접 입력 (없는 파트는 비워두면 됩니다)
4. **저장하기** 클릭
   - `data/weeks.json` 저장 후, YouTube API Key가 설정된 경우 **자동으로** `"청운교회 늘감사 성가대"` 검색을 수행해 최근 영상 5개를 `data/choir-videos.json`에 함께 저장합니다.
   - YouTube API Key가 없어도 주차 데이터는 정상 저장되며, 늘감사 영상은 다음 저장 시 업데이트됩니다.

#### 5단계: 링크 공유
1. **연습 영상 보기** 화면에서 해당 주차 선택
2. 하단 **이 페이지 링크 복사** 버튼 클릭
3. 복사된 링크를 카카오톡 등으로 대원들에게 전송

---

## GitHub Pages 설정 (최초 1회)

레포지토리를 생성한 후:
1. 레포 상단 **Settings** 탭
2. 좌측 **Pages** 메뉴
3. **Source**: Deploy from a branch
4. **Branch**: `main` / `/ (root)`
5. **Save** 클릭
6. 약 1분 후 `https://warabica.github.io/choir/` 접속 가능

---

## 파일 구조

```
choir/
├── index.html            ← 전체 앱 (메인/입력/조회/늘감사 영상 4개 화면)
├── data/
│   ├── weeks.json        ← 주차별 데이터 (앱이 자동 관리)
│   ├── choir-videos.json ← 늘감사 성가대 최근 영상 5개 (저장하기 시 자동 갱신)
│   └── church.png        ← 청운교회 로고 이미지
└── README.md
```

---

## 데이터 구조

### `data/weeks.json`

```json
{
  "weeks": [
    {
      "id": 16,
      "song": "곡 이름",
      "links": {
        "choir":   "https://youtube.com/...",
        "soprano": "https://youtube.com/...",
        "alto":    "https://youtube.com/...",
        "tenor":   "https://youtube.com/...",
        "bass":    "https://youtube.com/..."
      }
    }
  ]
}
```

### `data/choir-videos.json`

관리자가 **저장하기** 클릭 시 YouTube API로 자동 생성/갱신됩니다.

```json
{
  "updatedAt": "2026-04-26T10:00:00.000Z",
  "videos": [
    {
      "videoId": "xxxxxxxxxxxx",
      "title": "영상 제목",
      "channelTitle": "채널명",
      "publishedAt": "2026-04-20T00:00:00.000Z"
    }
  ]
}
```

- `updatedAt`: 마지막 갱신 시각 (ISO 8601)
- `videos`: 최근 5개 영상 목록 (일반 대원은 이 파일을 읽어 영상 표시, API Key 불필요)
