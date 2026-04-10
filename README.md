# IMBK_Bank_Customer_Churn_ML

## 프로젝트명: 고객 이탈 분류 ML 및 인사이트 분석
- 기간: 2026년 04년 10일
- requirement: `pandas`, `numpy`, `scikit-learn`, `pycaret`, `shap`, `matplotlib`, `optuna`, `catboost`, `xgboost`
- 데이터 출처: 캐글 Bank Customer Churn Dataset (row: 10000, col:12)

### 1. 데이터 전처리
   - 분석의 효율성을 위해 고유 식별값인 `customer_id` 컬럼을 제거
   - 범주형 변수인 `country` `gender` 컬럼은 머신러닝 모델이 학습할 수 있도록 `LabelEncoder`를 사용하여 수치형 데이터로 변환
   - 전체 데이터를 학습용(Train)과 검증용(Valid)으로 분리한 뒤, 특성(Feature) 간의 단위 차이를 조정하기 위해 StandardScaler를 적용

### 2. EDA 및 해석
   - 성별 및 국가 분포
   
   <img width="300" height="300" alt="graph" src="https://github.com/user-attachments/assets/59bfc988-b878-4eda-805e-dfff54cd2061" /> <img width="400" height="250" alt="graph2" src="https://github.com/user-attachments/assets/4c643b50-3b31-4672-b522-737f9bead8d0" />
      
   -- 여성고객이 남성보다 약 10% 분포가 높은 것으로 확인.
   -- 국가는 프랑스 고객이 압도적인 비중을 차지


### 3. AutoML
<img width="817" height="479" alt="image" src="https://github.com/user-attachments/assets/e0594472-619f-478d-9fb4-2c38784ef6e2" />

이중에 CatBoost, Gradient Boosting Classifier, Extreme Gradient Boosting, Ada Boost Classifier 모델 사용

### 4. Hyperarameter Tuning
- CatBoost: n_estimators => 100~300
            depth => 4~10
- Gradient Boosting Classifier: n_estimators => 100~300
                              max_depth: 4~10
- Extreme Gradient Boosting: n_estimators => 100~300
                              max_depth => 3~10
- Ada Boost Classifier: n_estimators => 50~300
                        learning_rate => 0.01, 1.0



최적 파라미터를 적용한 각 모델의 F1 Score 출력
<img width="518" height="80" alt="image" src="https://github.com/user-attachments/assets/d5c240ed-6837-45d6-b7b9-4178ef03ea7c" />

5. Stacking Pipe
전방모델: CatBoost, Gradient Boosting Classifier, Ada Boost Classifier
후방모델: Extreme Gradient Boosting
위의 모델들을 stacking하여 F1 Score를 출력했으나 0.57로 성능이 높게 출력되지 않음.

7. Shap value
<img width="757" height="550" alt="image" src="https://github.com/user-attachments/assets/1374d2ed-f0d2-48d1-b2b2-be98290f06cf" />

churn 이탈여부 : 0 = 유지, 1 = 이탈
- products_number: 3집군으로 나뉘어서 뚜렷하게 분류가 된 것으로 보임. 은행에서 이용 중인 상품 수가 낮을수록 이탈률 높다고 보임.
상품 수가 높으면 이탈하지하고 유지하는 쪽으로 몰려있는 것으로 확인되지만, 일부는 이탈률이 높다고 측정됨. 상품수가 높으나 이탈률이 높은 데이터를 살펴보아 특징을 알아볼 필요가 있음.
- age: 나이대가 낮을 수록 이탈률이 낮은 것으로 확인됨. 특정 연령대가 선호하는 상품을 보유중인지, 전연령대가 쓰기 적합하지 않은 상품인지 확인할 필요가 있음.
- active_member: 비활성이면 이탈, 활성이면 유지로 확인.
- balance: 분포가 계좌잔액이 낮을 수록 유지하는 것을 확인됨. 고잔액보유 고객이 이탈하는 이유가 무엇인지 찾아야한다.
- gender: 뚜렷하게 남여로 나뉘어 분포되어있음을 확인. 은행유지고객이 한 성별로 쏠린것으로 확인 됨.
- country ['France': 0 'Germany': 1 'Spain': 2]: France 고객이 주로 유지하는 것으로 확인 되며, Germany의 고객이 이탈률이 높은 것으로 확인됨.
                                               France에 최적화된 은행으로 볼 수 있을것이다. 다른나라의 이탈을 줄이기 위해 고안을 해보아야할 것임.
- estimated_salary: 골고루 분포되어있음.
- credit_score: 골고루 분포되어있음
- tenure: 이탈률에 크게 영향을 주지 않는 것으로 보임.
- credit_card: 이탈률에 영향이 거의 없는것으로 보임.

8. Reference
- 데이터 전처리 및 EDA : Pandas & Numpy
- 머신러닝 프레임워크 및 알고리즘: PyCaret(AutoML), Scikit-learn, Ensemble Learing(Boosting)
- 하이퍼파라미터 최적화 및 모델 해석: Optuna, SHAP
