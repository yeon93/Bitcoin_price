## 프로젝트 목표
+



## Data
+ pyupbit 라이브러리 이용, 5분봉 데이터 선택
+ open, high, low, volume, value 5개 feature를 통해 close(종가)를 예측
+ Normalizer를 사용해 정규화
+ window_size=100, 데이터를 window dataset 변환



## Model
+ Sequential + LSTM
+ loss='hube', optimizer='adam', metrics=['mse']
+ 테스트 성능 : loss 0.0207, mse 0.0415
