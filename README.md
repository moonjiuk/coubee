<p align="center">
  <img src="readme-images/coubee.svg" width="88" alt="Coubee 로고" />
</p>

<h1 align="center">Coubee · 쿠비</h1>
<p align="center">동네 상점과 고객을 연결하는 O2O 커머스 서비스</p>
<p align="center">
  <a href="#담당-역할">담당 역할</a> ·
  <a href="docs/repositories.md">소스 코드</a> ·
  <a href="docs/performance.md">성능 검증</a>
</p>

![판매자 웹 메인 화면](readme-images/seller-landing.png)

> 고객 앱, 판매자 웹, 운영자 웹과 마이크로서비스로 구성한 팀 프로젝트입니다. 이 저장소는 분산된 원본 코드와 문지욱의 담당 작업을 모아 소개하는 프로젝트 아카이브입니다.

## 서비스 소개

고객은 주변 상점을 탐색하고 상품을 주문·결제하며, 판매자는 매장과 상품, 주문, 매출을 관리합니다. 운영자 웹에서는 서비스 운영에 필요한 관리 기능을 제공합니다.

| 사용자 | 주요 기능 | 구현 |
| --- | --- | --- |
| 고객 | 주변 상점 탐색, 상품 조회·추천, 주문·결제 | React Native · Expo 앱 |
| 판매자 | 매장·상품·주문·매출 관리 | React · Vite 웹 |
| 운영자 | 서비스 운영 관리 | Vue · Vite 웹 |

## 담당 역할

**문지욱 · 배포 환경 구성, 테스트 자동화, 성능 검증**

| 영역 | 수행 내용 |
| --- | --- |
| CI/CD | Jenkins 기반 빌드·컨테이너 이미지 배포 구성 및 팀원용 설정 절차 문서화 |
| 인프라 | Terraform·EKS·ArgoCD 배포 환경 구성과 운영 절차 정리 |
| 테스트 자동화 | Playwright로 판매자 로그인과 상품 등록 흐름 검증 |
| 성능 검증 | JMeter 부하 시나리오 설계, 모니터링, 네트워크·레플리카·노드 변경 실험 및 병목 분석 |

팀 전체 서비스 구현과 개인 담당 작업을 구분하여 정리했습니다. [담당 작업 상세 보기 →](docs/contributions.md)

## 주요 화면

### 판매자 웹

![판매자 로그인 화면](readme-images/seller-login.png)

매장 운영을 위한 판매자 웹의 메인·로그인 화면입니다. 위 두 화면은 기존 프론트엔드 빌드를 로컬에서 촬영했으며, API 연결을 통한 로그인·주문·결제는 이번 정리에서 검증하지 않았습니다.

## 시스템 구성

![Coubee 아키텍처 설계도](readme-images/architecture.png)

고객·판매자·운영자 클라이언트와 도메인별 백엔드를 분리하고, AWS 인프라와 추천·알림 처리로 연결한 구조입니다. 위 그림은 팀의 인프라 설계도이며, 현재 운영 자원의 상태를 나타내는 그림은 아닙니다.

| 구분 | 주요 기술 |
| --- | --- |
| 프론트엔드 | React 19 · Vite 7 / React Native 0.79 · Expo 53 / Vue 3 |
| 백엔드 | Java 17 · Spring Boot 3.5 · Eureka · API Gateway |
| 인프라·배포 | AWS · Terraform · Docker · Kubernetes(EKS) · Jenkins · ArgoCD |
| 추천·알림 | Python · AWS Personalize · Lambda · EventBridge |
| 검증 | Playwright · JMeter |

프론트엔드 3개, 백엔드 8개, 인프라·알림·추천 3개로 구성된 **14개 원본 저장소**를 역할별로 모았습니다. [저장소 목록과 코드 보기 →](docs/repositories.md)

## 성능 검증

부하를 높이면서 응답 지연을 관찰하고, 인프라 증설의 효과와 애플리케이션 처리 경로를 나누어 확인했습니다.

- 레플리카·노드 증설만으로 지연 문제가 해소되지 않는 것을 확인했습니다.
- 상품 검색·추천 API가 공유하는 Python 처리 경로를 후속 병목 검증 대상으로 좁혔습니다.
- 설정 부하와 실제 처리량을 구분해 결과를 정리했습니다. 아래 수치는 **2025년 9월 11일 당시 JMeter 리포트**이며, 현재 서비스의 측정값이 아닙니다.

| 시나리오 이름 | 리포트 Throughput | 전체 요청 p95 | 오류율 |
| --- | ---: | ---: | ---: |
| RPS-150 | 11.6 req/s | 88 ms | 0.03% |
| RPS-160 | 73.1 req/s | 1,426 ms | 0.00% |

시나리오 이름의 RPS와 리포트의 실측 처리량이 달라, 이를 최대 150 RPS 처리 성과나 동일 조건의 전후 개선율로 해석하지 않았습니다. [실험 과정과 원본 리포트 보기 →](docs/performance.md)

## 코드 확인 및 실행

이 저장소에는 소개 문서와 이미지가 있으며, 실행 코드는 각 [원본 저장소](docs/repositories.md)에 있습니다.

판매자 웹과 운영자 웹은 잠금 파일 기준 `npm ci` 및 `npm run build` 성공을 확인했습니다. 앱·백엔드 실행과 클라우드 재배포는 이번 아카이브 범위에 포함하지 않았습니다. 확인한 코드 버전은 [저장소 스냅샷](docs/repo-snapshot.json)에 기록했습니다.

---

프로젝트 구현: **LG CNS 팀 4 · Honeycomb** · 개인 작업 정리: **문지욱**  
[원본 팀 프로젝트 소개](https://github.com/lg-cns-team-4-retail/.github/blob/main/profile/README.md) · [이미지 출처](docs/credits.md)
