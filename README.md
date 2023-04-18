# 2023project
## MobileBert를 활용한 게임리뷰 분석

## 1. 개요
 ### - 1.1 문제정의
 게임을 선택할때 이 게임이 재미가 있는지 또는 없는지 알 수 없고 게임을 플레이했을때 만족도를 알 수 없기때문에 게임 선택에 약간이나마 의사결정에 도움이 될만한 정보가 필요할 수 있다.
 때문에 리뷰를 통해서 많은 소비자들이 남긴 긍정적 혹은 부정적인 리뷰의 그 결과를 통해 게임 구매자에게 의사결정의 약간의 도움을 주기 위해 게임리뷰에 대한 분석을 한다.<br>
 이 프로젝트에서는 Kaggle에서 제공하는 게임리뷰 데이터를 바탕으로 긍정 혹은 부정을 예측하는 인공지능 모델을 개발하고자 한다.
 
 ### - 1.2 게임리뷰의 영향력
 
리뷰의 영향은 소비자가 제품을 구매하는 데 있어, 다양한 사전 정보 탐색을 통해 위험을 줄이려는 심리에서 그 원인을 찾을 수 있다. 특히 직접 사용해보지 않으면 해당 상품 및 서비스의 품질 및 만족도를 알 수 없는 경험재의 경우, 다른 구매자의 리뷰가 더 큰 영향력을 갖게 된다. 

한국인터넷진흥원이 실시한 ‘구매 결정 시 다른 사용자의 구매 후기에 영향을 받느냐’는 설문조사에서 74%의 응답자들이 영향을 받는다고 응답한 바 있다. 이처럼 온라인 리뷰는 소비자들의 구매 의사결정에 매우 중요한 역할을 담당하고 있다는 것을 알 수 있다.

 연구 결과 리뷰의 수는 판매량에 긍정적인 영향을 미치는 것으로 나타났다. 이는 게임의 리뷰가 많아질수록 소비자들의 게임 선택에 정의 영향을 미친다는 것을 뜻한다. 또한 리뷰가 긍정적일수록 비디오 게임의 성과에도 정의 영향을 미치는 것을 확인하였다. 더불어 본 연구는 정보이론에서 사용되는 엔트로피 개념을 활용하여 온라인 리뷰 감성의 분포에 따라 온라인 리뷰의 효과가 조절됨을 확인하였고, 사용자가 추천하는 경우에 리뷰 유용성에 영향을 미치는 것으로 분석되다. 
 또한, 리뷰어의 친구가 많을수록 유용하다고 판단하는 경향이 있었고, 게임 시간이 많은 게이머의 리뷰를 신뢰하는 경향이 보였다. 
 
## 2. 데이터
 ### - 2.1 데이터 출처
  Kaggle : https://www.kaggle.com/datasets/georgescutelnicu/hogwarts-legacy-reviews
  
 ### - 2.2 입력-모델-출력
 
 ### - 2.3 데이터 구성
  Index - 번호
  Playtime - 리뷰 기준 플레이 시간, 1시간 미만은 0으로 표시
  Feedback - Positive(긍정), Negative(부정)으로 나눔
  Review - 리뷰
  
 ### - 2.5 라벨, 분포, 부가정보
  - 총 46404개의 리뷰<br/>
  - 0~125시간 플레이시간<br/> ![hlplaytime](https://user-images.githubusercontent.com/79897716/231339975-de24721a-d26d-4bed-848d-761f1abf02c8.png)
<br/><br/>
  - 92% 긍정(Positive) 8% 부정(Negative) <br/>![0412](https://user-images.githubusercontent.com/79897716/231343783-23bdc89d-f9f7-4aa2-9566-d004c62a2a9e.png)
<br/><br/>
  - 41433개의 고유의 값<br/>
  
 ### - 2.6 가공


------ 출처 -------
https://www.itlab.co.kr/v7/?m=rssM&bid=column&cat=LG+CNS&sort=d_regis&orderby=desc&uid=27004 <br/>
https://s-space.snu.ac.kr/handle/10371/166332
