# 성가대 연습 영상 링크 공유

교회 성가대 대원들과 주차별 파트 연습 유튜브 링크를 공유하는 웹앱입니다.

**라이브 주소:** https://warabica.github.io/choir/

---

## 사용 방법

### 대원 (일반 사용자)
1. 지휘자/관리자에게 받은 링크를 클릭합니다.
2. 주차를 선택하면 파트별 유튜브 링크가 표시됩니다.
3. 원하는 파트 카드를 클릭하면 유튜브가 열립니다.

### 관리자 (링크 입력)

#### 1단계: GitHub PAT 발급
1. GitHub → 우상단 프로필 → **Settings**
2. 좌측 하단 **Developer settings** → **Personal access tokens** → **Tokens (classic)**
3. **Generate new token (classic)** 클릭
4. Note: `choir-app`, Expiration: 원하는 기간 설정
5. Scope: **`public_repo`** 체크
6. **Generate token** 클릭 → 토큰 값 복사 (한 번만 표시됨!)

#### 2단계: 앱에서 PAT 입력
1. 웹앱 메인 화면 → **링크 입력 (관리자)** 버튼
2. `Personal Access Token` 입력란에 발급받은 PAT 붙여넣기
3. **저장** 클릭 (브라우저에 저장됨, 다음부터는 자동 입력)

#### 3단계: 주차 링크 입력
1. 주차 번호, 곡 이름 입력
2. 각 파트 유튜브 링크 입력 (없는 파트는 비워두면 됩니다)
3. **저장하기** 클릭

#### 4단계: 링크 공유
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
├── index.html       ← 전체 앱
├── data/
│   └── weeks.json   ← 주차별 데이터 (앱이 자동 관리)
└── README.md
```
