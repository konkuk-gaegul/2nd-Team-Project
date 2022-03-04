# 2nd-Team-Project
Welcome to konkuk-gaegul's Repository Of Second Team Project

# DACON 신용카드 연체 예측 AI 경진대회
- 대회는 2021년 5월에 종료, 이 모델은 2022년 3월에 생성하였다.
- 약 1,000여 개 팀이 참여하여 다양한 인사이트와 코드의 공유가 활발히 이루어졌다.

# 목적
- 개인 정보(성별, 집, 가족, 직업, 연봉, 근무시기, 수입원 등)를 통해 신용카드 연체 여부를 학습한다.
- predict_probaility로 각 신용 점수의 확률을 구한다.

# 변수 설명
- 변수 설명은 다음 데이콘 링크를 참고한다.
  https://www.dacon.io/competitions/official/235713/talkboard/402821/
- 유의해야할 변수 
    - DAYS_BIRTH, DAYS_EMPLOYED, begin_month
    - DAYS or weeks 값이 자료 수집일 기준, 과거이기 때문에 음수를 갖는다.

# Feature Engineering
