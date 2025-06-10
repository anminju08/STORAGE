# 물류 창고 위치 추천 및 배송 수요 예측 시스템

FastAPI와 MySQL을 기반으로 물류 창고 위치를 추천하고 지역별 배송 수요를 예측하는 시스템입니다. 시계열 예측 모델과 클러스터링 기반의 추천 기능을 포함하여, 실시간 데이터 관리 및 시각화를 지원합니다.

---

## 🛠 기술 스택

- **Backend:** FastAPI
- **Database:** MySQL 8.0
- **ORM:** SQLAlchemy
- **Template Engine:** Jinja2
- **Visualization:** Chart.js
- **Machine Learning:** Prophet, ARIMA, scikit-learn(KMeans)
- **Containerization:** Docker & Docker Compose

---

## 🔑 주요 기능

1. **CRUD**
   - 물류 창고, 지역, 배송 수요 데이터 등록 / 조회 / 수정 / 삭제

2. **시각화**
   - 지역별 배송 수요 및 물류량 차트 제공 (Chart.js)

3. **예측**
   - 시계열 데이터 기반 향후 배송 수요 예측 (Prophet, ARIMA 등)

4. **추천**
   - 수요가 많은 지역을 중심으로 최적 물류 창고 위치 추천 (KMeans 클러스터링)

---

## 📁 프로젝트 구조

```
.
├── FastAPI
│   ├── Dockerfile
│   ├── README.md
│   ├── app
│   │   ├── __init__.py
│   │   ├── crud
│   │   ├── main.py
│   │   ├── models
│   │   ├── routers
│   │   ├── schemas
│   │   ├── static
│   │   └── templates
│   ├── docker-compose.yml
│   └── requirements.txt
└── structure.txt
```

## 설치 및 실행 방법

1. 프로젝트 클론
```bash
git clone [프로젝트_URL]
cd [프로젝트_디렉토리]
```

2. Docker 컨테이너 실행
```bash
docker-compose up --build
```

3. 웹 브라우저에서 접속
- 메인 페이지: http://localhost:8000
- API 문서: http://localhost:8000/docs

## 데이터베이스 스키마

### storage 테이블
   -  id (PK): Integer
   -  name: String(100)
   -  location: String(255)
   -  capacity: Integer
   -  created_at: DateTime
   -  updated_at: DateTime

### regions 테이블
	-	id (PK): Integer
	-	name: String(100)
	-	latitude: Float
	-	longitude: Float
   -	population: Integer
	-	created_at: DateTime
	-	updated_at: DateTime

### demands 테이블
	-	id (PK): Integer
	-	region_id (FK): Integer
	-	date: Date
	-	delivery_count: Integer
	-	created_at: DateTime
   -	updated_at: DateTime



## API 엔드포인트

### 창고 관리
	- GET /storage/ – 창고 목록 조회
	- POST /storage/ – 창고 생성
	- GET /storage/{id} – 창고 상세 조회
	- PUT /storage/{id} – 창고 수정
	- DELETE /storage/{id} – 창고 삭제


### 지역 관리
	-	GET /regions/ – 지역 목록 조회
	-	POST /regions/ – 지역 생성

### 수요 데이터
	-	GET /demands/ – 배송 수요 목록 조회
	-	POST /demands/ – 배송 수요 등록

### 에측/추천
   -  GET/predict/{region_id} - 특정 지역의 향후 수요 예측
   -	GET /recommend/ – 물류 창고 위치 추천

## 주의사항

1. MySQL 포트 충돌
   - 기본 MySQL 포트(3306)가 이미 사용 중인 경우, docker-compose.yml 파일에서 포트를 변경할 수 있습니다.
   - 예: "3307:3306"으로 변경

2. 데이터베이스 접속 정보
   - 기본 설정:
     - 데이터베이스: facility_db
     - 사용자: user
     - 비밀번호: password
   - 필요시 docker-compose.yml 파일에서 환경 변수를 수정할 수 있습니다.

## 개발 환경 설정

1. Python 가상환경 생성 및 활성화
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

2. 의존성 패키지 설치
```bash
pip install -r requirements.txt
```

## 라이선스

이 프로젝트는 MIT 라이선스를 따릅니다. 
