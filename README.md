# Goyang_fifteen
COMPAS에서 주최한 고양시의 자전거 대여소(피프틴)의 새로운 장소를 데이터로 도출하는 입지 분석 프로젝트를 수행하였습니다.  
2020년 7월~8월 동안 진행되었으며, 이 공모전에서 __장려상__ 을 수상하였습니다.  
위 코드는 [COMPAS의 다음 링크](https://compas.lh.or.kr/subj/past/code?subjNo=SBJ_2007_001&teamNo=590)에서도 다운받으실 수 있습니다.

A location analysis project was conducted to derive data from a new location at a bicycle rental station (Fifteen) in Goyang City hosted by COMPAS.
It was held from July to August of 2020, and was awarded the __Encouragement Prize__ in this competition.
The above code can also be downloaded from [the following link of COMPAS.](https://compas.lh.or.kr/subj/past/code?subjNo=SBJ_2007_001&teamNo=590)

---
### 1. Background
- 고양시 공공자전거의 운영이력 데이터 및 공간정보 데이터를 활용하여, 신규 자전거 스테이션의 위치를 선정하는 프로젝트 
- 분석에 사용한 데이터는 모두 COMPAS에서 제공
### 2. 분석 개요
- EDA: 피프틴의 이용 현황을 다양하게 시각화(이용시간, 대여시간대별/요일별 이용건수, 주요 이용 스테이션, 경로분석 등)
- 선행 연구 검토: 공공자전거에 대해 연구한 논문을 바탕으로 자전거 이용에 영향을 미치는 요인에 대해 검토
  - 서울시 공공자전거 이용에 영향을 미치는 물리적 환경요인 분석(사경은 외, 2018)
  - 계절 및 회원 특성이 공공자전거 통행에 미치는 영향분석: 서울시 따릉이를 대상으로(장재민 외, 2018)
- 고양시 관련 기사 검토: 최근 고양시의 개발 이슈를 뉴스기사를 토대로 알아보고, 이를 새로운 입지를 도출하는 데 활용
### 3. 피처 생성 및 다중회귀 모델 구축
- H3 라이브러리를 활용하여 고양시의 도시화 지역을 그리드로 나눈 뒤, 각종 공간 정보를 매핑한 뒤 기존 스테이션을 포함하는 그리드의 데이터를 학습하는 지도학습 모델링 진행
- 새롭게 개발한 피처는 크게 _인구특성 변수, 토지이용특성 변수, 대여소 접근성 변수_ 로, 세부적으로는 16개의 피처 생성 
- 기본모델은 피프틴 이용에 영향을 미치는 요인이 무엇인지를 알기 위한 다중회귀 모델
- 데이터 스케일링, 잔차분석, Stepwise Selection 등을 활용하여 유의한 피처만 선별, 최종 12개의 피처 선택. 
### 4. 모델링
- 만들어진 최종 피처를 대상으로, 예상 수요를 타겟으로 하는 예측 모델링 
- 크게 _선형회귀 모델과 Tree 기반 모델_ 을 만들었으며, 가장 좋은 예측 성능을 보인 `XGBRegressor` 채택 
### 5. 분석 결과 및 문제 해결 
- 학습된 모델에 기반한 일 평균 수요 예측 결과와, 향후 지역 개발 정보들을 반영하여 신규 스테이션 위치 선정 및 거치대수 결정 
### 6. 의의 및 한계
- 의의: 도시화 지역을 그리드화+모델링을 결합한 분석은 새로운 접근이었다고 생각, 피프틴 사용자의 이용특성을 반영한 입지분석으로 사용자들이 만족할 최적 위치에 입지할 수 있을 것을 기대
- 한계: 기존 피프틴 스테이션의 수가 적어 학습 데이터의 수가 적었다는 점, 좀 더 세부적인 위치에 해당하는 데이터의 부족으로 모델링에 아쉬움이 있었음

<img src=https://user-images.githubusercontent.com/48719168/111165057-f6390580-85e1-11eb-9000-25b8f7ace710.jpg  width="400" height="450"> <img src=https://user-images.githubusercontent.com/48719168/111272769-61341c00-8676-11eb-8394-5edf477f6487.jpg  width="400" height="450">
