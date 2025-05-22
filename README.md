김재민
=======
![Profile Photo](profile.jpg)

- 연락처: 010-6226-5546
- 이메일: kjm5546@gmail.com
- 링크드인: https://www.linkedin.com/in/재민-김-871716153/

## About
안녕하세요, 소프트웨어 엔지니어 김재민입니다.

Java Spring, AWS 기반의 7년 차 서버 백엔드 개발자로, 이커머스 ‘뉴발란스’, 일 평균 트래픽 4,000만의 ‘그루비 마케팅 솔루션’ 등의 서비스에서 백엔드 플랫폼 개발 및 AWS 인프라 구축 등을 수행해 왔습니다.

개인이 하고 싶은 일보다 회사와 팀의 목표 달성에 기여하는 개발을 우선시하며, 원활한 소통과 명확한 목표 설정을 바탕으로 업무를 진행하는 것을 선호합니다.

확장 가능한 시스템과 유연한 운영을 위해 리팩토링, 신규 기술 도입, 시스템 설계를 제안하고 주도해 왔으며, 안정적인 운영을 위한 테스트 코드 작성은 기본적인 개발 습관으로 여기고 있습니다.

## 경력

### 플래티어
**2022.08 ~ 재직 중 (2년 9개월) | AI CX SaaS 사업부 플랫폼개발팀 | 과장**
- 그루비 신규 기능 개발, 설계, 운영
- 대용량 처리, 성능 개선을 위한 신규 기술 도입
- 모놀리식 레거시 시스템 MSA 마이그레이션
- 테스트 코드 도입으로 안정적인 배포 환경 구성

<details>
<summary>
Details
</summary>

### 과거 세그먼트 대상 기간 연장에 대한 성능 최적화 | PL
- 배경
  - 고객사의 니즈로 기존 최대 3개월 이었던 과거 행동 기간 연장이 필요
- 액션
  - 최대 5배까지 연장되는 경우를 위해 기존 로직의 성능 개선
    - DB 비즈니스 로직 확인 후 1초 이상 slow query 최적화, index 작업
    - Elasticache를 도입하여 과거 행동 데이터 조회 세그먼트 결과를 캐싱
- 성과
  - **DB CPU 부하 40 ~ 50% 개선**
  - 1년 후 행동 데이터가 누적된 상황에서 서비스 장애 없이 운영

### 룰 세그먼트 리팩토링, 테스트 코드 도입 | PL
- 배경
  - 기존 로직은 DB에 저장되어 있는 Class명, function명을 Java Reflection의 method invoke로 구현되어 있었고 신규 개발에 대한 비효율성과 DB 의존성이 존재
- 액션
  - 유사한 기능을 하고 있는 Class들이여서 팩토리 패턴으로 리팩토링
  - 해당 프로젝트에서 JUnit5 최초 도입하여 기능에 대한 Unit Test를 진행
- 성과
  - 신규 세그먼트 개발에 대한 공수 20 ~ 30% 감소
  - DB 의존성 없이 코드 베이스로 개발 할 수 있어 신규 인원에게 불필요한 가이드 인계에 대한 일정 단축, 개발 과정 중 휴먼에러 발생 확률 축소
  - Unit Test로 기능 검증하여 QA과정 단축
    - QA팀에서 테스트 진행 시 **3090건의 테스트 케이스 중 오류건 수 4건 발생(0.1%)**

### 룰 세그먼트, 추천 기능 MSA 전환 | PL
- 배경
  - 메인 서버가 모놀리식으로 구현되어 있어 장애 발생 시 모든 기능에게 영향을 주고 있음
- 액션
  - 제일 많은 부하가 발생되는 룰 세그먼트 기능을 별도의 도메인으로 분리 작업
  - DB 분리 작업
  - 신규 ECS 구성, 내부 네트워크 LB 구성
- 성과
  - 룰 세그먼트, 추천 도메인이 부하가 발생되더라도 다른 서비스들이 영향을 받지 않고 정상적으로 기능을 수행


### 오프사이트 발송 Event-Driven으로 전환 | PL
- 배경
  - 오프사이트 발송에 대한 장애 발생이 잦고 Spring Batch와 Jenkins cron 기반으로 설계되어 있어서 모니터링에 어려움이 있음
  - EC2에서 같은 발송시간에 Spring Batch를 여러개 실행 시키는 경우에는 Scale-Out이 어렵고 다른 작업이 서로 영향을 주는 상황이 발생

- 액션
  - AWS 관리형 서비스를 이용한 Event-Driven 아키텍처 전환
  - Lambda에서 수행되는 PostgreSQL DB LOCK 원인을 파악하여 수정
  - MongoDB Atlas Database Triggers, EventBridge, EventBridge Scheduler, Step Functions, Lambda, ECS로 구현
  - CloudWatch + Webhook 기반 장애 실시간 전파

- 성과
  - **기존 구조 대비 비용 91% 절감**
  - ECS Fargate 실행 구조로 고객사 별 독립된 작동 보장, 안정성 증가
  - 장애 발생 빈도 감소
  - 고객사, 발송 이벤트 별 모니터링 편의성 증가

### Admin 신규 프로젝트 전환, 리팩토링 | PL
- 배경
  - 고객사가 사용하는 Admin은 Spring MVC 구조로 Front 영역이 JS, Thymeleaf로 개발이 되어 있었는데 모듈화가 되어 있지 않아 기능 확장이 어렵고 신규 개발 속도가 부진
- 액션
  - 프론트엔드 팀과 협업을 위해 Spring Boot로 백엔드로 전환하면서 SpringDoc Swagger-ui를 도입하여 문서화 진행
- 성과
  - API 명세서를 통해 프론트엔드팀과 원활한 소통으로 개발 기간 단축

### 데이터 수집 확장성을 위한 kafka 도입 및 개발
- 배경
  - 행동 데이터를 기반으로 하는 데이터마트 수요 및 상품 추천을 위한 학습 전용 데이터의 필요성
- 액션
  - AWS MSK Kafka, Spring Cloud Stream Kafka 메세지 브로커 신규 도입
  - Produce, Consume에 대한 성능테스트 진행 및 스펙 산정
- 성과
  - Kafka를 이용해 다른 도메인에서 데이터를 실시간으로 수집 할 수 있어서 새벽에 발생하는 Batch 작업을 제거

### 성능/부하테스트 환경 구성
- 배경
  - 성능/부하테스트를 할 수 있는 환경이 구성되어 있지 않아 신규 기능 배포 후 성능이슈로 롤백하는 경우가 발생
- 액션
  - AWS 환경 내에 JMeter를 설치하여 성능/부하테스트 환경을 구축
  - 성능/부하테스트를 진행하기 위한 프로세스 정립
- 성과
  - 성능 문제로 인한 운영배포 후 롤백하는 경우가 발생하지 않음

### 그 외 운영 업무, 추천 신규 기능 개발, 고객사 요구 기능 개발 대응
- 상품 추천 신규 기능 개발
- 고객사 문의 사항 대응, 비정상 데이터 확인 후 버그 수정
- 운영 시 발생되는 반복 작업, 테스트 편의성 증대를 위한 백오피스 구성
- 내부 프로젝트 네이밍 규칙, 커밋 메세지 convention 정의
- 신규 사용될 기술 및 SaaS에 대한 비용, 적정 스펙 파악
- Java, Spring boot 버전 업

</details>

### 아이엔소프트
**2022.05 ~ 2022.08 (4개월) | 어플리케이션 현대화 사업부 | 대리**
- 사내 프로젝트 매니징 그룹웨어 개발
- MSA 설계, Kubernetes, CI/CD 환경 구성

<details>
<summary>
Details
</summary>

### PMS 프로젝트 매니저 시스템 설계 및 개발
- Vue.js, Spring Boot를 이용한 CSR 신규 프로젝트 개발
- 프로젝트 세팅, 백엔드 기능 개발, 인프라 구성
- Kubernetes, Jenkins로 CI/CD 구성

</details>

### 라드씨엔에스
**2021.04 ~ 2022.05 (1년 1개월) | 뉴발란스(SF)팀 | 주임**
- 뉴발란스 백엔드 신규 기능 개발 및 유지보수
- 뉴발란스 MyNB 백엔드 신규 기능 개발 및 유지보수
- API 개발, Linux 배포 및 자동화, 대규모 트래픽 환경 대응 및 최적화
- 레거시 프로젝트 Spring으로 마이그레이션
- ISMS 인증 대응

<details>
<summary>
Details
</summary>

### 뉴발란스
#### 신규 대규모 이벤트 개발 (멤버스 위크, 블랙프라이데이)
- 이벤트 페이지 웹 개발, 기능 개발
- 네이버페이 결제 API 추가
- SSR에서 CSR로 일부 전환 및 slow query 개선으로 기존대비 3배 트래픽까지 수용 가능하게 개선

#### .NET Legacy API 재고관리 서버 Spring Boot로 전환
- 기존 API 구조 파악 및 마이그레이션
  
#### 로그 개선 작업
- S3에 log 파일을 업로드하여 Glue, Athena를 이용해서 로그 탐색 편의성 증가

#### 운영 업무
- 주문, 결제 관련 비정상 데이터 확인
- 데이터 추출
- ISMS 인증 대응
  
---

### MyNB
#### 신규 대규모 이벤트 개발 (뉴발란스 마라톤)
#### 운영 업무
- MyNB 활동 포인트 관련 문의 대응
- STRAVA 운동 추적 API 기능 오류 개선
- Jenkins CI/CD 결과 Slack Webhook 알림 작업

</details>

### 유탑소프트
**2017.12 ~ 2020.06 (2년 7개월) | Convergence Lab | 사원**
- 교원 도요새 잉글리시 인텐시브 과정 콘텐츠 및 UI 개발
- 교원 구몬 스마트이야기 4A 과정 앱, 콘텐츠, UI 개발
- 한컴로보틱스 Toki Readers 하이브리드 앱 개발
- 교원 도요새 중국어 콘텐츠 및 UI 개발

<details>
<summary>
Details
</summary>

### 교원 도요새 잉글리시 인텐시브, 중국어 
- Unity3d로 교육 앱 개발

### 교원 구몬 스마트이야기 4A 게임 개발
- Unity3d로 교육 앱 개발

### 한컴로보틱스 Toki Readers 앱 개발(Android, iOS 출시)
- Toki 로봇에서 진행하는 교육 진척도를 관리하는 앱
- QR코드 인식을 통한 Toki 로봇 연동
- 로그인 및 기기관리
- MVVM 패턴을 이용한 Xamarin 앱 구현

</details>

## 역량
### 리팩토링, 리엔지니어링
- Event-Driven 아키텍처 도입으로 개선된 성능, 모니터링, 비용 절감
- 그루비 전체 Admin 시스템 백엔드 분리(Spring MVC => Spring Boot) 마이그레이션
- 그루비 룰 세그먼트 시스템 리플렉션 호출 구조에서 전략패턴 및 테스트 코드 도입(비정상 작동 30% 개선)
- Spring Boot 버전 업, 마이그레이션
- 뉴발란스 재고 관리 API (.NET => Spring Boot) 마이그레이션

### 성능 개선, 안정성 개선
- JUnit5 테스트 코드 도입 (3,156개)
- Elasticache 도입을 통해 MongoDB 부하 개선(CPU 40~50% 개선)
- ISMS 인증 및 CSAP 인증 대응 개선

### 신규 기술 도입, 구조 설계
- 모놀리식 구조에서 MSA로 전환하고, 주요 기능을 모듈화
- 그루비 오프사이트 발송(Push, Kakao, SMS) 시스템 Event-Driven 아키텍처 설계(AWS 비용 91% 절감)
- Spring Cloud Stream Kafka, MSK 도입으로 대용량 메시지 처리(데이터 마트 구성 및 데이터 정합성 개선)
- 성능/부하 테스트 도입 및 환경 구성(배포 후 성능 관련 장애률 50% 개선)

### 자동화 및 인프라 운영 관리
- 운영 업무 자동화를 위한 백오피스 환경 설계 및 구축
- Graviton ARM 아키텍처 전환
- Kubernetes, GitHub Actions 환경 구성
- 뉴발란스 S3 로그 분석을 위한 Glue, Athena를 도입

## Tech Stack
> 현재 업무에 사용 중 혹은 사용했던 기술입니다.

### Backend
- Java, Groovy, C#, Python
- Spring Boot, Spring Batch, Spring MVC, Spring Security, Spring Data Redis, Spring Cloud AWS/GCP, Spring Cloud Stream Kafka, .NET Framework, JUnit5
- Gradle, Maven
- Intellij, Visual Studio Code, Visual Studio, WebStorm

### DevOps
- PostgreSQL, MySQL, MariaDB, MS-SQL
- MongoDB, Redis
- Kafka, RabbitMQ
- Docker, Kubernetes
- Jenkins, GitHub Actions, AWS Code Deploy
- AWS ECS, CloudWatch, Glue, Athena, EventBridge, Step Functions, Lambda, RDS, Elasticache, MSK
- GCP BigQuery, Cloud Run
- MongoDB Atlas
- Sentry, Prometheus, Grafana
- Linux CentOS, Ubuntu, AmazonLinux

### Frontend
- Vue.js
- Npm
- Xamarin

## 교육
### AWS EDA Jumpstart 워크숍
##### 2025.04 ~ 2025.05
AWS EventBridge, Step Functions를 이용한 Event-Driven Development 교육 및 PoC 구현

### 자바 기반 웹 개발자 과정
##### 2020.09 ~ 2021.03
Java, Spring, RDB, JavaScript, MVC 교육 수료

## 학력 및 병역
### 경남과학기술대학교
##### 컴퓨터공학 학사 (2012.03 ~ 2018.02)
- 평균 평점 3.92 / 4.5
- 전공 평균 평점 4.05 / 4.5
### 육군 병장
##### 만기 전역 (2013.05 ~ 2015.02)