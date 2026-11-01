# 원본 저장소

[← 프로젝트 소개](../README.md)

Coubee는 여러 저장소로 구성된 하나의 팀 프로젝트입니다. 아래 링크에서 각 구성 요소의 코드를 확인할 수 있습니다.

## 프론트엔드

| 저장소 | 역할 |
| --- | --- |
| [coubee-fe-web](https://github.com/lg-cns-team-4-retail/coubee-fe-web) | 판매자 웹 · React / Vite |
| [coubee-fe-app](https://github.com/lg-cns-team-4-retail/coubee-fe-app) | 고객 앱 · React Native / Expo |
| [coubee-fe-superadmin](https://github.com/lg-cns-team-4-retail/coubee-fe-superadmin) | 운영자 웹 · Vue / Vite |

## 백엔드

| 저장소 | 역할 |
| --- | --- |
| [coubee-be-eureka](https://github.com/lg-cns-team-4-retail/coubee-be-eureka) | 서비스 탐색 |
| [coubee-be-gateway](https://github.com/lg-cns-team-4-retail/coubee-be-gateway) | API 라우팅·인증 |
| [coubee-be-user](https://github.com/lg-cns-team-4-retail/coubee-be-user) | 회원·인증 |
| [coubee-be-store](https://github.com/lg-cns-team-4-retail/coubee-be-store) | 매장·위치 기반 조회 |
| [coubee-be-product](https://github.com/lg-cns-team-4-retail/coubee-be-product) | 상품·검색·추천 API |
| [coubee-be-order](https://github.com/lg-cns-team-4-retail/coubee-be-order) | 주문·결제 |
| [coubee-be-notification](https://github.com/lg-cns-team-4-retail/coubee-be-notification) | 이벤트 기반 알림 |
| [coubee-be-report](https://github.com/lg-cns-team-4-retail/coubee-be-report) | 매출 통계 |

## 인프라·연동

| 저장소 | 역할 |
| --- | --- |
| [coubee-infra-terraform](https://github.com/lg-cns-team-4-retail/coubee-infra-terraform) | AWS 인프라 선언 |
| [coubee-infra-notification-lambda](https://github.com/lg-cns-team-4-retail/coubee-infra-notification-lambda) | 알림 분배·푸시 발송 |
| [coubee-personalize](https://github.com/lg-cns-team-4-retail/coubee-personalize) | 추천 데이터 처리·AWS Personalize 연동 |

## 확인한 코드 버전

기본 `main` 브랜치의 체크아웃 커밋을 [repo-snapshot.json](repo-snapshot.json)에 기록했습니다. 판매자·운영자 웹은 `npm ci`와 `npm run build` 성공을 확인했으며, 두 빌드 모두 500 kB 초과 청크 경고가 남아 있습니다. 고객 앱·백엔드 실행과 클라우드 자원 상태는 확인하지 않았습니다.

[팀 프로젝트 소개](https://github.com/lg-cns-team-4-retail/.github/blob/main/profile/README.md)
