# 🐝 Coubee · 쿠비

<img src="readme-images/seller-landing.png" alt="쿠비 판매자 웹 메인 화면" width="800px">

동네 상점과 고객을 연결하는 O2O 커머스 서비스입니다.
고객 앱의 상점 탐색·주문·결제와 판매자 웹의 매장·상품·주문·매출 관리를 연결합니다.

## 👨‍💻 역할

- **팀 프로젝트:** LG CNS 팀 4 · Honeycomb
- **담당:** 배포 환경 구성, 테스트 자동화, 성능 검증
- Jenkins·EKS·ArgoCD 설정과 팀원용 배포 절차를 문서화했습니다.
- Playwright로 로그인·상품 등록을 검증하고, JMeter로 부하 테스트와 병목 분석을 수행했습니다.

[담당 작업 상세](docs/contributions.md)

## 🛠️ 사용 기술

- **고객 앱:** React Native 0.79, Expo 53
- **판매자·운영자 웹:** React 19, Vue 3, Vite 7
- **백엔드:** Java 17, Spring Boot 3.5, Eureka, API Gateway
- **인프라·배포:** AWS, Terraform, Docker, Kubernetes(EKS), Jenkins, ArgoCD
- **추천·알림:** Python, AWS Personalize, Lambda, EventBridge
- **테스트:** Playwright, JMeter

## 🚀 섹션별 설명

### 서비스 구성

- **고객 앱:** 주변 상점과 상품을 탐색하고 추천·주문·결제 기능을 제공합니다.
- **판매자 웹:** 매장·상품·주문·매출을 관리합니다.
- **운영자 웹:** 서비스 운영에 필요한 관리 기능을 제공합니다.

<img src="readme-images/seller-login.png" alt="판매자 웹 로그인 화면" width="800px">

메인·로그인 화면은 기존 프론트엔드 빌드를 로컬에서 촬영했습니다. 현재 API 연결을 통한 사용자 흐름은 미검증 상태입니다.

### 고객 앱 · 상점 페이지

상점의 할인 정보와 상품 목록을 확인하고, 매장 내 상품 검색·관심 상점 등록·가게 정보 조회로 이어지는 화면입니다.

<img src="readme-images/app-store.png" alt="쿠비 고객 앱의 상점 페이지 — 할인 정보, 관심 상점, 상품 검색과 목록" width="300px">

2025년 팀 최종 발표 자료에 수록된 앱 화면입니다.

### 배포 환경 구성

Jenkins에서 **버전 설정 → 애플리케이션 빌드 → Docker 이미지 빌드 → 이미지 푸시**로 이어지는 파이프라인을 구성하고, 팀원이 사용할 수 있도록 설정 절차를 정리했습니다. Terraform·EKS·ArgoCD 기반 배포 환경의 구성과 운영 절차도 문서화했습니다.

<img src="readme-images/architecture.png" alt="팀에서 작성한 Coubee 인프라 아키텍처 설계도" width="800px">

팀 아키텍처 설계도입니다. 현재 운영 자원의 상태를 나타내는 그림은 아닙니다.

### 핵심 기능 자동화 테스트

Playwright로 판매자 로그인과 상품 등록 흐름을 검증했습니다.

- **로그인:** 계정 입력 → 로그인 → 판매자 화면 이동
- **상품 등록:** 상품 정보 입력 → 이미지 업로드·크롭 → 제출 → 목록 반영 확인

### 성능 검증과 병목 분석

JMeter로 부하를 높이며 **p95 응답 시간·JVM Heap·CPU**를 관찰했습니다. 네트워크, 레플리카, 노드 수를 바꾸어 지연 원인을 조사했습니다.

- **레플리카 증설:** 지연 문제가 해소되지 않았습니다.
- **노드 증설:** CPU 사용량은 감소했으나 지연 한계는 남았습니다.
- **처리 경로 분석:** 상품 검색·추천 API가 공유하는 Python 처리 경로를 후속 검증 대상으로 좁혔습니다.

| 시나리오 | 실측 처리량 | p95 응답 시간 | 오류율 |
| --- | ---: | ---: | ---: |
| RPS-150 | 11.6 req/s | 88 ms | 0.03% |
| RPS-160 | 73.1 req/s | 1,426 ms | 0.00% |

2025년 9월 11일 리포트 기준입니다. 시나리오 이름과 실측 처리량이 달라 최대 처리량이나 동일 조건의 개선율로 해석하지 않습니다.

[실험 과정·원본 리포트](docs/performance.md)

## 📌 저장소 및 실행 안내

이 저장소는 프로젝트 소개와 담당 작업을 모은 아카이브입니다. 실행 코드는 **프론트엔드 3개·백엔드 8개·인프라 및 연동 3개**의 원본 저장소에서 확인할 수 있습니다.

- [역할별 원본 저장소 14개](docs/repositories.md)
- [확인한 코드 버전](docs/repo-snapshot.json)
- [팀 프로젝트 소개](https://github.com/lg-cns-team-4-retail/.github/blob/main/profile/README.md)

판매자·운영자 웹의 `npm ci`와 `npm run build` 성공을 확인했습니다. 앱·백엔드 실행과 클라우드 재배포는 진행하지 않았습니다.

[이미지 출처](docs/credits.md)
