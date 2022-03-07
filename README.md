# 2nd-Team-Project
- DACON PUBLIC 12위, Log Loss : 0.66659
- 멀티캠퍼스 데이터사이언스 빅데이터활용 프로젝트 최우수상

# DACON 신용카드 연체 예측 AI 경진대회
- 대회는 2021년 5월에 종료, 이 모델은 2022년 3월에 생성하였다.
- 약 1,000여 개 팀이 참여하여 다양한 인사이트와 코드의 공유가 활발히 이루어졌다.

## 목적
- 개인 정보(성별, 집, 가족, 직업, 연봉, 근무시기, 수입원 등)를 통해 신용카드 연체 여부를 학습한다.
- predict_probaility로 각 신용 점수의 확률을 구한다.

## 변수 설명
- 변수 설명은 다음 데이콘 링크를 참고한다.
  https://www.dacon.io/competitions/official/235713/talkboard/402821/
- 유의해야할 변수 
    - DAYS_BIRTH, DAYS_EMPLOYED, begin_month
    - DAYS or weeks 값이 자료 수집일 기준, 과거이기 때문에 음수를 갖는다.

## Feature Engineering

### 결측치 처리
- occyp_type의 결측치 약 8000개 존재
- 이 중 절반 이상의 수입원(income_type)은 연금 
  - 해당 데이터에 한하여 결측치를 retiree(퇴직자)로 대체
- 나머지는 수입원이 존재하여 No reponse(무응답)으로 

### deleted features
- index
- FLAG_MOBIL : 모든 값이 1, 분별력 상실
- child_num : familiy_size에 포함

### categorical features
- gender : 기본 변수
- car : 기본 변수
- reality : 기본 변수
- income_type : 기본 변수
- edu_type : 기본 변수
- family_type : 기본 변수
- house_type : 기본 변수
- occyp_type : 기본 변수
- ID : 중복된 데이터에 한해, 기존 변수를 합하여 주민등록번호와 같은 효과를 냄
- feature_set_4의 파생변수
  - G_C_R : gender + car + reality
  - I_O_E : income_type + occpy_type + edu_type
  - F_H : family_type + house_type

### numerical features
- income_total : 기본 변수
- DAYS_BIRTH : 기본 변수
- DAYS_EMPLOYED : 기본 변수
- work_phone : 기본 변수
- phone : 기본 변수
- email : 기본 변수
- family_size : 기본 변수
- begin_month : 기본 변수

### 정규화
- 분포가 일정하지 않은 변수에 대해서 정규화 진행
  - 로그, 제곱 그리고 StandardScale

## Machine Learing Model
- 팀원 별로 각자 다른 ML 알고리즘 사용
- Logistic Regression
- Catboost

## Cross Validation
- 분류 모형에서만 사용할 수 있는 StratifiedKFold 사용
- Parmeters
  - n_splits : 5 ~ 15까지 반복 수행했을 때 15에서 제일 좋은 성능을 냄
  - shuffle  : True
 
## HyperParameter
- 첫 모델은 기준을 위해 Default Parameter로 모델링 진행
- CatBoost는 Parameter로 cat_features가 존재
  - categorical_feature의 중요성을 인지함
  - G_C_R , I_O_E , F_H 변수 생성 및 Parameter 지정
- Optuna Library 이용하여 Best Parmeter 추출
  - 최고의 하드웨어 성능을 가진 AWS로 HyperParmeter tuning은 3시간, ML 학습은 1시간 소요
  - 구글 코랩으로 HyperParmeter tuning은 6시간, ML 학습은 3시간 소요
  - 최고점수(14등 -> 12등) 달성

## BenchMark
- Train 자료의 Log-Loss만을 나타냄
- features set 4에서 가장 좋은 점수를 보여줌
  - set 2와 3을 거쳐 4가 될 때 까지 categorical feature의 중요성을 느끼고, 파생변수 

|feature_set|model|K_folds|Los-Loss|
|------|------|---|---|
|set 2|CatBoost|15|0.664357|
|set 3|CatBoost|15|0.664093|
|set 4|CatBoost|15|0.662465|

# 출처
- CatBoost Classifier
  - https://catboost.ai/en/docs/concepts/python-reference_catboostclassifier

