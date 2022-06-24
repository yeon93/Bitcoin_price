# 비트코인 가격 예측
![image](https://user-images.githubusercontent.com/88722429/175088485-2f3079f4-c22f-40e5-a787-312aa2577b58.png)

## 프로젝트 기획 배경
+ 최근 몇년간 비트코인에 대한 관심이 급증하면서 2030부터 노년층까지 많은 사람들이 투자에 뛰어듦
+ 코인의 변동성 덕분에 벼락부자도 생긴 반면, 변동성 때문에 한순간에 전재산을 잃은 사람도 생겨남  
=> 지금까지의 비트코인 가격 추세 데이터를 이용해 앞으로의 가격을 예측해 투자에 도움을 줄 수 있다면?


## 솔루션
pyupbit 라이브러리 이용, 30분봉 데이터 선택  

### 1. 딥러닝을 이용해 가격 변동의 패턴을 학습해 다음 가격을 예상
+시간 흐름에 따른 sequential 데이터이기 때문에, 긴 시간에 분포한 패턴(eg.경제 사이클)을 학습하기 위해 LSTM 모델 선택
  + loss='hube', optimizer='adam', metrics=['mse']
  + 테스트 성능 : loss 0.0207, mse 0.0415  

+ open, high, low, volume, value 5개 feature를 통해 close(종가)를 예측
+ 0 이하의 값이 나오지 않도록 Normalizer를 사용해 정규화
+ window_size=100, 데이터를 window dataset으로 변환
![output](https://user-images.githubusercontent.com/88722429/175494033-9e712827-7f5c-44bf-b6ce-cad4d6171338.png)

### 2. 코사인 유사도를 이용해 가장 비슷한 과거의 패턴을 통해 다음 가격을 예상
+ close, volume 2개 feature의 패턴 이용
![output](https://user-images.githubusercontent.com/88722429/175493207-b38607d9-b485-469b-bd7f-eced6bc01568.png)
+ StandardScaler를 사용해 정규화
+ window_size=100, 데이터를 처음부터 끝까지 슬라이딩하며 학습해 미래 10개의 캔들을 예측하도록 함
+ 두 특성의 코사인 유사도를 계산해 평균값을 예측에 사용
![output](https://user-images.githubusercontent.com/88722429/175493946-94db3822-d52a-4434-a317-f982793511f5.png)





## 한계
+ 비트코인 가격에 영향을 주는 요소가 매우 많음(수요/공급, 실물경제, 심리적 요인, 전쟁 등)
+ 예측가격 그래프 역시 그릴 수는 있으나, 실질적으로 예측이라기 보다는 후행분석에 가까움
+ 예상 수익률을 계산해보았을 때 실제로 활용하기에는 적합하지 
