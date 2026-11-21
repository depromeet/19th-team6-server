<div align="center">

# 🚀 19th Team6 Server

**친구들과 함께 "살까 말까" 고민하고, 소비를 가볍게 기록하는 소셜 가계부**

결제 직전, 친구 그룹에 고민을 올리고 투표와 대안을 받아 더 나은 선택을 해요.<br>
그리고 그 선택과 지출을 부담 없이 기록해요.

<br>

<img src="https://img.shields.io/badge/DEPROMEET-19th-000000?style=flat-square" />
<img src="https://img.shields.io/badge/Team-6-4F46E5?style=flat-square" />
<img src="https://img.shields.io/badge/Platform-iOS-000000?style=flat-square&logo=apple&logoColor=white" />

</div>

<br>

## 🤔 왜 만들까요?

| 리서치 결과 (20대 설문 88명) | |
| :--- | :---: |
| 돈이 새고 있다고 느낀다 | **91%** |
| 가계부를 꾸준히 쓴다 | **8%** |
| 구매 전 주변에 의견을 묻는다 | **44%** |
| 물어본 사람 중 의견을 듣고 결정이 바뀌었다 | **82%** |

> 기록은 번거로워서 안 하지만, **친구 의견은 실제로 소비를 바꾼다.**<br>
> 그래서 "기록"이 아니라 **"같이 고민하기"** 에서 출발합니다.

<br>

## ✨ 주요 기능

### 🛒 살까 말까 (메인)
- 결제 전, 친구 그룹에 고민 글 올리기
- 친구들의 **투표**와 **대안 제시**
- 마감 후 **최종 선택 기록**: 안 삼 / 대안 구매 / 원래 것 구매
- 안 사서 아낀 금액 확인 ("안 산 것"과 "실제 저축"은 구분)

### 📅 가벼운 지출 기록 (보조)
- 금액 · 카테고리 · 항목명만으로 최소 입력
- 캘린더 형태의 가계부
- 기록별 **공개 여부**를 사용자가 선택

### 👥 그룹
- 팔로우가 아닌 **그룹 단위** 소셜 구조
- 초대로 친구 그룹 만들기

### 🔔 알림
- 투표 요청, 마감 등 푸시 알림 (APNs)

> 🧪 검토 중: 투표 링크를 카카오톡으로 공유해 앱이 없는 친구도 웹에서 투표<br>
> ⏸ 보류: 익명 커뮤니티 (UT 결과 보고 결정)

<br>

## 🛠 기술 스택

**Backend**

<img src="https://img.shields.io/badge/Java%2021-007396?style=flat-square&logo=openjdk&logoColor=white" /> <img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white" /> <img src="https://img.shields.io/badge/Spring%20Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white" /> <img src="https://img.shields.io/badge/Spring%20Data%20JPA-6DB33F?style=flat-square&logo=spring&logoColor=white" /> <img src="https://img.shields.io/badge/JWT-000000?style=flat-square&logo=jsonwebtokens&logoColor=white" /> <img src="https://img.shields.io/badge/Gradle-02303A?style=flat-square&logo=gradle&logoColor=white" />

**Database · Cache**

<img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white" /> <img src="https://img.shields.io/badge/Redis%20(예정)-DC382D?style=flat-square&logo=redis&logoColor=white" />

**Infra (초안)**

<img src="https://img.shields.io/badge/AWS%20EC2-FF9900?style=flat-square&logo=amazonec2&logoColor=white" /> <img src="https://img.shields.io/badge/AWS%20RDS-527FFF?style=flat-square&logo=amazonrds&logoColor=white" /> <img src="https://img.shields.io/badge/AWS%20S3-569A31?style=flat-square&logo=amazons3&logoColor=white" /> <img src="https://img.shields.io/badge/SQS%20·%20Lambda-FF4F8B?style=flat-square&logo=awslambda&logoColor=white" /> <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white" />

**Auth · Docs**

<img src="https://img.shields.io/badge/Kakao%20Login-FFCD00?style=flat-square&logo=kakao&logoColor=black" /> <img src="https://img.shields.io/badge/Google%20Login-4285F4?style=flat-square&logo=google&logoColor=white" /> <img src="https://img.shields.io/badge/Sign%20in%20with%20Apple-000000?style=flat-square&logo=apple&logoColor=white" /> <img src="https://img.shields.io/badge/Swagger-85EA2D?style=flat-square&logo=swagger&logoColor=black" />

<br>

## 🏗 아키텍처 (초안)

```
 iOS App
    │
    ▼
  ALB ──▶ EC2 (Spring Boot, Auto Scaling) ──▶ RDS (MySQL)
              │          │                └─▶ Redis (예정)
              │          └─▶ S3 (Presigned URL)
              │
              ├─▶ SQS ──▶ Lambda (AI 분석 · 배치)
              └─▶ APNs (푸시)

 EventBridge ──▶ 투표 마감 · 주간 배치
 CloudWatch  ──▶ 모니터링
```

> 💰 초기에는 **EC2 1대 + RDS 프리티어**로 시작하고, 트래픽에 맞춰 확장합니다.

<br>

## 🔐 인증 구조

카카오 · 구글 · 애플 소셜 로그인을 **하나의 공통 구조**로 처리합니다.

```
iOS (SDK 로그인) ──토큰──▶ 서버
                             │
                   OAuthClient (제공자별 구현)
                   ├─ Kakao : 액세스 토큰으로 사용자 정보 API 호출해 검증
                   ├─ Google: 토큰 검증
                   └─ Apple : id_token(JWT)을 애플 공개키(JWKS)로 검증
                             │
                   공통 사용자 정보 (provider, providerId, email)
                             │
                   (provider, providerId)로 회원 조회 / 가입
                             │
                   서버 JWT 발급 (Access / Refresh)
```

- 소셜 로그인을 제공하므로 **애플 로그인 필수** (App Store 심사 가이드라인 4.8)
- 애플은 이메일 · 이름을 **첫 로그인 때만** 주기 때문에 반드시 저장

<br>

## 🧩 도메인 (초안)

> 기능 명세 확정 시 변경될 수 있습니다.

| 도메인 | 설명 |
| --- | --- |
| `member` | 회원, 소셜 로그인 계정 |
| `group` | 그룹, 그룹 멤버, 초대 |
| `ask` | 살까 말까: 고민 글 → 투표 → 대안 제시 → 마감 → 최종 선택 |
| `record` | 지출 기록(금액, 카테고리, 항목명), 공개 여부 |
| `notification` | 푸시 알림 (APNs) |

<br>

## 🧱 개발 원칙

| 구분 | 원칙 |
| --- | --- |
| 🔁 트랜잭션 | 조회는 `readOnly = true`, 범위는 짧게. AI 호출 · 푸시 등 외부 호출은 트랜잭션 밖에서, 커밋 이후 처리는 `AFTER_COMMIT` 이벤트로 |
| 🗳 동시성 | 동시 투표 집계 누락 방지 (조건부 UPDATE, 유니크 제약, 필요 시 락). 중복 요청은 멱등하게 |
| 🚨 예외 처리 | 공통 에러 포맷 `{ code, message }` + `@RestControllerAdvice` + 도메인별 커스텀 예외 |
| 📜 로그 | 요청별 traceId(MDC), INFO / WARN / ERROR 기준 분리, 토큰 · 금액 등 민감 정보 마스킹 |
| 🛡 권한 | 그룹 멤버만 그룹 데이터 접근, IDOR 방지, "금액 숨김"은 서버 응답에서부터 제외 |
| ✅ 테스트 | 서비스 단위 테스트, 주요 API 통합 테스트, 투표 동시성 테스트 |
| 🔑 보안 | 키 · 시크릿은 절대 커밋하지 않고 환경변수로만 참조 (로컬 `.env` / 배포 GitHub Secrets · Parameter Store) |
| 📝 ADR | 기술 선택 근거를 `docs/adr/`에 기록 (상황 / 선택지 / 기준 / 결정 / 이유 / 트레이드오프 / 다시 볼 조건) |

<br>

## 📐 개발 컨벤션

### 📦 패키지 구조

도메인별로 패키지를 먼저 나누고, 그 안에서 역할별로 나눕니다.

```
src/main/java/.../
├── member/
│   ├── controller/
│   ├── service/
│   ├── repository/
│   ├── entity/
│   └── dto/
├── group/
├── ask/
├── record/
└── notification/
```

- DTO와 Entity는 **별도 패키지**에서 관리합니다.
- DTO는 **Inner Class** 방식을 사용합니다.

```java
public class LoginDTO {
    public record Request(String provider, String token) {}
    public record Response(String accessToken, String refreshToken) {}
}
```

### 🏷 네이밍

| 대상 | 규칙 | 예시 |
| --- | --- | --- |
| 클래스명 | `PascalCase` | `MemberService` |
| 필드명 | `camelCase` | `providerId` |
| YML 파일 | `kebab-case` | `application-jwt.yml` |

### ⚙️ 설정 파일

- DB 등 공통 설정은 `application.yml`
- `jwt`, `aws`, `mail` 등은 **별도 yml**로 분리 (`.gitignore` 처리)

### 🌐 API URL

- URL에 **동사를 쓰지 않습니다.**
- `/api/{버전}/{entity}` 형식 → 예) `/api/v1/member`

<br>

## 🤝 협업 규칙

### 🌿 브랜치 전략

| 브랜치 | 설명 |
| --- | --- |
| `main` | 운영 브랜치 |
| `develop` | 개발 통합 브랜치 |
| `feat/*` | 기능 개발. `develop`에서 분기 → `develop`으로 merge |
| `hotfix/*` | 운영 긴급 수정. `main`에 merge 후 `develop`에 반영 |

**네이밍** : `브랜치종류/이슈번호-간단한설명` → 예) `feat/67-login`

### 📝 커밋 메시지

```
type : 제목 #이슈번호

본문
```

| Type | 설명 |
| --- | --- |
| ✨ `feat` | 새로운 기능 |
| 🐛 `fix` | 버그 수정 |
| 🚀 `ci/cd` | 배포 |
| 📝 `docs` | 문서 수정 |
| 🎨 `style` | 코드 스타일, 포맷 |
| ♻️ `refactor` | 리팩토링 |
| ✅ `test` | 테스트 코드 |
| 🔧 `chore` | 패키지 · 빌드 설정 |

<br>

## 👥 Server Team

| <img src="https://github.com/JJhwan7099.png" width="100" /> | <img src="https://github.com/D5-wq.png" width="100" /> |
| :---: | :---: |
| **정지환** | **황윤재** |
| [@JJhwan7099](https://github.com/JJhwan7099) | [@D5-wq](https://github.com/D5-wq) |
| 👑 Server Lead | 🛠 Server |

<br>

<div align="center">

🚀 Made with care by **DEPROMEET 19th Team 6**

</div>
