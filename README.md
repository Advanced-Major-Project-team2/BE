# GangKU - 강쿠 (Backend)

모임을 만들고, 참여하고, 사람들과 연결되는 모임 플랫폼의 백엔드 서버입니다.

## 기술 스택

| 분류 | 기술 |
|------|------|
| 프레임워크 | Spring Boot 3.5.6 |
| 언어 | Java 21 |
| ORM | Spring Data JPA |
| 보안 | Spring Security + JWT |
| 데이터베이스 | MySQL (운영), H2 (로컬/테스트) |
| 캐시 | Redis |
| 스토리지 | AWS S3 |
| HTTP 클라이언트 | Spring WebFlux (WebClient) |
| 코드 포맷터 | Spotless (Google Java Format) |

## 주요 기능

- **모임** - 모임 생성 / 수정 / 삭제 / 종료 / 상세 조회 / 목록 조회 (날짜 필터)
- **참여** - 모임 참여 / 취소
- **리뷰** - 리뷰 작성 / 조회
- **유저** - 회원가입 / 프로필 조회·수정 / 선호 카테고리 설정
- **인증** - 이메일 인증 / 로그인 / JWT 기반 인증
- **AI** - 모임 소개글 자동 생성 / 개인화 추천 / 텍스트 필터링
- **홈** - 추천 / 최신 / 인기 모임 조회
- **오브젝트 스토리지** - S3 Presigned URL 발급

## 프로젝트 구조

```
src/
├── main/
│   ├── java/com/gangku/be/
│   │   ├── config/       # 설정 (Security, AWS, Redis, AI 등)
│   │   ├── constant/     # 상수 정의
│   │   ├── controller/   # REST API 컨트롤러
│   │   ├── domain/       # JPA 엔티티
│   │   ├── dto/          # 요청/응답 DTO
│   │   ├── exception/    # 예외 처리 및 에러 코드
│   │   ├── external/     # 외부 API 클라이언트 (AI 서버)
│   │   ├── model/        # 도메인 모델
│   │   ├── repository/   # JPA 리포지토리
│   │   ├── service/      # 비즈니스 로직
│   │   └── util/         # 유틸리티 (JWT, S3, AI 매퍼 등)
│   └── resources/
│       ├── application.yml
│       ├── application-local.yml
│       └── application-prod.yml
└── test/                 # 단위 테스트
```

## 시작하기

### 환경 변수 설정

`.env` 파일을 프로젝트 루트에 생성하여 아래 변수를 설정하세요.

| 변수 | 설명 |
|------|------|
| `JWT_SECRET` | JWT 서명 시크릿 키 |
| `JWT_EXP_MIN` | JWT 만료 시간 (분, 기본값: 60) |
| `MAIL_HOST` | SMTP 호스트 |
| `MAIL_PORT` | SMTP 포트 |
| `MAIL_USERNAME` | SMTP 계정 |
| `MAIL_PASSWORD` | SMTP 비밀번호 |
| `MAIL_FROM` | 발신자 이메일 주소 |
| `S3_IMAGE_BUCKET` | S3 버킷 이름 |
| `S3_REGION` | S3 리전 |
| `S3_IMAGE_BASE_PREFIX` | S3 이미지 경로 프리픽스 |
| `S3_TTL_SECONDS` | Presigned URL 유효 시간 (초) |
| `CDN_BASE_URL` | CDN 베이스 URL |

### 로컬 실행

```bash
# 로컬 프로파일로 실행 (H2 DB, 로컬 Redis)
./gradlew bootRun --args='--spring.profiles.active=local'
```

개발 서버: [http://localhost:8080](http://localhost:8080)

H2 콘솔: [http://localhost:8080/h2-console](http://localhost:8080/h2-console)

로컬 환경에서는 H2 인메모리 DB를 사용하므로 별도의 MySQL 설치가 필요 없습니다.

### 빌드

```bash
./gradlew build
java -jar build/libs/be-0.0.1-SNAPSHOT.jar --spring.profiles.active=prod
```

---
