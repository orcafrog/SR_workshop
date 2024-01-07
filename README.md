# LSTM을 통한 주가 방향 예측 및 성능 분석

---
## 🔥 목차
+ 개요
+ 개발기간
+ 실행환경
+ 모델 결과
+ 백테스트 코드
+ 결과
---
## 📚 개요
+ 주가 데이터를 활용하여 주가의 변동 패턴을 학습하고 주가 가격과 방향성을 예측하기<br>
적합한 ***LSTM(Long)*** 모형을 이용하여  18년치 데이터를 test set과 train set으로 분리하고<br>
1000회 학습시킨 후 이익 주가의 향방을 예측함 <br>
---
## ⏲️ 개발기간
+ 총 개발 기간2023.09.07 ~ 2023.11.01
  + 모델 선택 회의 2023.10.11
  + 금리와 거시경제 변수 상관관계 분석 2023.10.11
  + 분석한 데이터를 활용하여 모델 완성 2023.11.01
---
## 🎓 실행환경
* 운영체제: Colab pro
* Python: 3.10.12
* Yfinance: 0.2.31
* Pandas: 1.5.3
* Numpy: 1.23.5
* Sklearn: 1.2.2
* Matplotlib: 3.7.1
* Torch: 2.1.0+cu118
* Torchinfo: 1.8.0
* Torchviz: 0.0.2
---
## 모델 결과
||
|모델 결과 이미지|
---
## 백테스트 코드
```
from backtesting import Backtest,Strategy
from backtesting.lib import crossover

class backtesting(Strategy):
  def init(self):
    super().init()
    Open_price=self.data.Open
    Close_price=self.data.Close
  def next(self):
    for i in range(len(self.data)):
      try:
        if self.data["0_d"][i]>=0.0 and self.data["Rate"][i]==2.0:
            self.buy()
        elif self.data["Rate"][i]==0.0 or self.data["0_d"][i]<0:
            self.sell()
      except:
        pass
```
```
bt=Backtest(final_df_real["2020-01-01":],backtesting,commission=.0002,cash=100000,exclusive_orders=True)
stats=bt.run()
print(stats)
```
---
## 🔍 결과
|![KakaoTalk_20240107_162720940](https://github.com/orcafrog/SR_workshop/assets/76116588/c007a4e3-3f7f-41c6-b5e2-9a3a9eb9dfc9)|![애플 8년](https://github.com/orcafrog/SR_workshop/assets/76116588/22d75585-632c-4c42-866f-7ea1aba7d0da)|![그래픽 8년](https://github.com/orcafrog/SR_workshop/assets/76116588/6abf17a7-b2e9-40ee-9b63-3a270d5f9d42)|
|------|---|---|
|GOOG 8년 백테스트 결과|AAPL 8년 백테스트 결과|NVIDA 8년 백테스트 결과|
|![구글 3년](https://github.com/orcafrog/SR_workshop/assets/76116588/b3180617-26f9-4466-845c-4ee708f0a369)|![애플 3년](https://github.com/orcafrog/SR_workshop/assets/76116588/7900718c-b2f3-4df6-8ac5-8b0c75e768b7)|![그래픽 3년](https://github.com/orcafrog/SR_workshop/assets/76116588/1dbec5ea-b686-44ea-afd2-baff41044a6e)|
|GOOG 3년 백테스트 결과|AAPL 3년 백테스트 결과|NVIDA 3년 백테스트 결과|


