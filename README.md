# 비트코인 가격 예측
![image](https://user-images.githubusercontent.com/88722429/175088485-2f3079f4-c22f-40e5-a787-312aa2577b58.png)

## 프로젝트 기획 배경
+ 최근 몇년간 비트코인에 대한 관심이 급증하면서 2030부터 노년층까지 많은 사람들이 투자에 뛰어듦
+ 코인의 변동성 덕분에 벼락부자도 생긴 반면, 변동성 때문에 한순간에 전재산을 잃은 사람도 생겨남  
=> 지금까지의 비트코인 가격 추세 데이터를 이용해 앞으로의 가격을 예측해 투자에 도움을 줄 수 있다면?



## Data
+ pyupbit 라이브러리 이용, 5분봉 데이터 선택
+ open, high, low, volume, value 5개 feature를 통해 close(종가)를 예측
+ Normalizer를 사용해 정규화
+ window_size=100, 데이터를 window dataset 변환



## Model
시간 흐름에 따른 sequential 데이터이기 때문에, 긴 시간에 분포한 패턴(eg.경제 사이클)을 학습하기 위해 LSTM 모델 선택
+ loss='hube', optimizer='adam', metrics=['mse']
+ 테스트 성능 : loss 0.0207, mse 0.0415  
![output](https://user-images.githubusercontent.com/88722429/175094954-d19eebab-7c03-4d50-ba3d-853717eab61d.png)



## 한계
+ 비트코인 가격에 영향을 주는 요소가 매우 많음(수요/공급, 실물경제, 심리적 요인, 전쟁 등)
+ 예측가격 그래프 역시 그릴 수는 있으나, 실질적으로 예측이라기 보다는 후행분석에 가까움
+ 예상 수익률을 계산해보았을 때 실제로 사용할 수 없는 모델임
