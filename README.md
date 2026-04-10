# IMBK_Bank_Customer_Churn_ML

## 프로젝트명: 고객 이탈 분류 ML 및 인사이트 분석
- 기간: 2026년 04년 10일
- requirement: `pandas`, `numpy`, `scikit-learn`, `pycaret`, `shap`, `matplotlib`, `optuna`, `catboost`, `xgboost`
- 데이터 출처: 캐글 Bank Customer Churn Dataset (row: 10000, col:12)

1. 데이터 전처리
   - 분석의 효율성을 위해 고유 식별값인 `customer_id` 컬럼을 제거
   - 범주형 변수인 `country` `gender` 컬럼은 머신러닝 모델이 학습할 수 있도록 `LabelEncoder`를 사용하여 수치형 데이터로 변환
   - 전체 데이터를 학습용(Train)과 검증용(Valid)으로 분리한 뒤, 특성(Feature) 간의 단위 차이를 조정하기 위해 StandardScaler를 적용

2. EDA 및 해석
   - 

깃 레포 이름: IMBK_Bank_Customer_Churn_ML
1. 프로젝트명: 고객 이탈 분류 ML 및 인사이트 분석
2. 기간 : 2026년 4월 10일
3. 기술스택: 라이브러리 명시
4. 데이터 출처: 캐글 Bank Customer Churn Dataset (row: 10000, col:12)
5. 데이터 전처리
6. EDA 및 해석
7. AutoML – Hyperparameter Tuning – Stacking Pipe – Shap value
8. 인사이트 제안
9. Reference
