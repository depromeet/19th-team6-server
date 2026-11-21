<div align="center">

# 🚀 19th Team6 Server

**{서비스 한 줄 소개}**

{서비스가 해결하려는 문제와 핵심 가치를 2~3줄로 소개합니다.}

<br>

<img src="https://img.shields.io/badge/DEPROMEET-19th-000000?style=flat-square" />
<img src="https://img.shields.io/badge/Team-6-4F46E5?style=flat-square" />

</div>

<br>

## ✨ 주요 기능

> 기능이 정해지면 채워 주세요.

| 기능 | 설명 |
| --- | --- |
| {기능 1} | {설명} |
| {기능 2} | {설명} |
| {기능 3} | {설명} |

<br>

## 🛠 기술 스택

**Backend**

<img src="https://img.shields.io/badge/Java%2021-007396?style=flat-square&logo=openjdk&logoColor=white" /> <img src="https://img.shields.io/badge/Spring%20Boot%204-6DB33F?style=flat-square&logo=springboot&logoColor=white" /> <img src="https://img.shields.io/badge/Spring%20Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white" /> <img src="https://img.shields.io/badge/Spring%20Data%20JPA-6DB33F?style=flat-square&logo=spring&logoColor=white" /> <img src="https://img.shields.io/badge/Lombok-BC4521?style=flat-square" /> <img src="https://img.shields.io/badge/Gradle-02303A?style=flat-square&logo=gradle&logoColor=white" />

**Database · Infra · CI/CD**

> 확정되면 추가해 주세요.

<br>

## 🧱 개발 컨벤션

### 📦 패키지 구조

도메인(`member`, `chat` 등 큰 단위)별로 패키지를 먼저 나누고, 그 안에서 역할별로 나눕니다.

```
src/main/java/.../
├── member/                  ← 도메인
│   ├── controller/
│   ├── service/
│   ├── repository/
│   ├── entity/              Entity
│   └── dto/
│       ├── request/         요청 DTO
│       └── response/        응답 DTO
└── chat/
    └── ...
```

- DTO와 Entity는 **별도의 패키지**에서 관리합니다.
- DTO 내부는 용도에 따라 `request`, `response` 패키지로 분리합니다.
- DTO는 **Inner Class** 방식을 사용합니다. (예: `LoginDTO` 안에 `Request`, `Response`)

```java
public class LoginDTO {
    public record Request(String email, String password) {}
    public record Response(String accessToken) {}
}
```

### 🏷 네이밍

| 대상 | 규칙 | 예시 |
| --- | --- | --- |
| 클래스명 | `PascalCase` | `MemberService` |
| 필드명 | `camelCase` | `nickName` |
| YML 파일 | `kebab-case` | `application-jwt.yml` |

### ⚙️ 설정 파일

- DB 설정 등 프로젝트 공통 설정은 `application.yml`에 둡니다.
- `jwt`, `aws`, `mail` 등은 **별도 yml 파일**로 분리해 관리합니다.

### 🌐 API URL

- URL에 **동사를 쓰지 않습니다.**
- `/api/{버전}/{Entity 이름}` 형식을 사용합니다.

```
GET  /api/v1/member
POST /api/v1/chat
```

<br>

## 🤝 협업 규칙

### 🌿 브랜치 전략

| 브랜치 | 설명 |
| --- | --- |
| `main` | 실제 운영 중인 서비스 브랜치 |
| `develop` | 개발 브랜치. 여러 `feat`이 merge되는 곳으로, 아직 release되지 않은 기능이 모입니다. |
| `feat/*` | 기능 하나를 개발하는 브랜치. `develop`에서 분기해 완료 후 `develop`으로 merge합니다. |
| `hotfix/*` | 운영 장애 대응 브랜치. `main`에 바로 merge하고, 이후 `develop`에도 반영합니다. |

**네이밍** : `브랜치종류/이슈번호-간단한설명`

```
feat/67-login
```

### 📝 커밋 메시지

```
Type : 제목 #이슈번호

본문
```

```
feat : 로그인 기능 구현 #67
```

| Type | 설명 |
| --- | --- |
| `feat` | 새로운 기능 |
| `fix` | 버그 수정 |
| `ci/cd` | 배포 |
| `docs` | 문서 수정 |
| `style` | 코드 스타일, 포맷 |
| `refactor` | 코드 리팩토링 |
| `test` | 테스트 코드 수정 |
| `chore` | 패키지 관련 및 빌드 코드 수정 |

<br>

## 👥 팀원

| <img src="https://github.com/{github-id}.png" width="100" /> | <img src="https://github.com/{github-id}.png" width="100" /> | <img src="https://github.com/{github-id}.png" width="100" /> |
| :---: | :---: | :---: |
| [@{github-id}](https://github.com/{github-id}) | [@{github-id}](https://github.com/{github-id}) | [@{github-id}](https://github.com/{github-id}) |
| {역할} | {역할} | {역할} |

<br>

<div align="center">

🚀 Made with care by **DEPROMEET 19th Team 6**

</div>
