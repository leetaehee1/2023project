# 2023project 
## MobileBert를 활용한 게임리뷰 분석

## 1. 개요

 <img src = "https://user-images.githubusercontent.com/79897716/234445318-cec73f4a-e3ca-4426-b738-9ff31227f6b1.png" width="300" height="100">

 **스팀**(Steam)은 밸브 코퍼레이션에서 개발하고 운영 중인 세계 최대 규모의 전자 소프트웨어 유통망이다.  
 스팀 클라이언트를 통해 게임을 구입, 관리할 수 있으며, 채팅, 방송 및 다양한 커뮤니티 기능을 통해 다른 유저들과 소통할 수 있으며 약 5만 개가 넘는 게임들이 있으며, 2019년 발표된 자료에 의하면 가입 계정이 10억 개를 돌파했고, 2021년에는 월 평균 사용자 1억 3,200만 명을 기록하며 엄청난 인기를 끌고 있다 [1]. <br/>
이 스팀게임 중에서 호그와트 레거시라는 해리포터의 호그와트를 배경으로한 게임의 리뷰에 대해 분석하고자 이 게임을 선택하였다.<br/><br/>
 <img src = "https://user-images.githubusercontent.com/79897716/234443638-811bd143-3d53-46b3-9516-65be5d95b620.jpg" width="550" height="330"><br/>

**호그와트 레거시**는 해리포터 세계관에서 진행되는 몰입형 오픈월드 액션 RPG 게임이다.  
  한국 시간으로 2023년 2월 6일 출시하였고, 원작자 관련 논란에도 불구하고 2월 7일에는 이러한 논란이 무색하게 트위치 트래커에 따르면 트위치에서 호그와트 레거시의 순간 시청자수가 130만명을 돌파했다.<br/>
  또한 정식 출시가 아닌 디럭스 에디션 구매자 한정 사전 접속만으로 스팀 동시 접속자 수 49만명을 기록했으며, 2월 12일 기준 호그와트 레거시의 스팀 최다 동시 접속자 수는 80만명으로, 주간 2위이자 역대 스팀 최대 동시 접속자 수 8위(RPG 장르 3위)에 올랐다. 전문가들은 호그와트 레거시가 출시 첫주에 1,000만장 이상 판매될 것이라 예측했고 발매 2주만에 1200만 장을 판매하고 8억 5천만 달러의 수익을 올렸을 정도로 흥행한 게임이다.

### - 문제정의
 
 게임을 선택할때 이 게임이 재미가 있는지 또는 없는지 알 수 없고 게임을 플레이했을때 만족도를 알 수 없기때문에 게임 선택에 약간이나마 의사결정에 도움이 될만한 정보가 필요할 수 있다.
 때문에 리뷰를 통해서 많은 소비자들이 남긴 긍정적 혹은 부정적인 리뷰를 예측해보고 그 결과를 통해 게임 구매자에게 의사결정의 약간의 도움을 주기 위해 게임리뷰에 대한 분석을 한다.<br>
 이 프로젝트에서는 Kaggle에서 제공하는 **호그와트 레거시**라는 게임의 리뷰 데이터를 바탕으로 긍정 혹은 부정을 예측하는 인공지능 모델을 개발하고자 한다.
 
 ### - 게임리뷰의 영향력
 
 리뷰의 영향은 소비자가 제품을 구매하는 데 있어, 다양한 사전 정보 탐색을 통해 위험을 줄이려는 심리에서 그 원인을 찾을 수 있다. 특히 직접 사용해 보지 않으면 해당 상품 및 서비스의 품질 및 만족도를 알 수 없는 경험재의 경우, 다른 구매자의 리뷰가 더 큰 영향력을 갖게 된다 [2].  
 한국인터넷진흥원이 실시한 ‘구매 결정 시 다른 사용자의 구매 후기에 영향을 받느냐’는 설문조사에서 74%의 응답자들이 영향을 받는다고 응답한 바 있다. 이처럼 온라인 리뷰는 소비자들의 구매 의사결정에 매우 중요한 역할을 담당하고 있다는 것을 알 수 있다 [2].  

 연구 결과 리뷰의 수는 판매량에 긍정적인 영향을 미치는 것으로 나타났다. 이는 게임의 리뷰가 많아질수록 소비자들의 게임 선택에 정의 영향을 미친다는 것을 뜻한다. 또한 리뷰가 긍정적일수록 비디오 게임의 성과에도 정의 영향을 미치는 것을 확인하였다. 더불어 본 연구는 정보이론에서 사용되는 엔트로피 개념을 활용하여 온라인 리뷰 감성의 분포에 따라 온라인 리뷰의 효과가 조절됨을 확인하였고, 사용자가 추천하는 경우에 리뷰 유용성에 영향을 미치는 것으로 분석이다. 
 또한, 리뷰어의 친구가 많을수록 유용하다고 판단하는 경향이 있었고, 게임 시간이 많은 게이머의 리뷰를 신뢰하는 경향이 보였다 [3].
 
## 2. 데이터
 ### - 데이터 출처
  Kaggle : https://www.kaggle.com/datasets/georgescutelnicu/hogwarts-legacy-reviews
  
 ### - 입력-모델-출력
 ```python
 import pandas as pd
 df = pd.read_csv('/content/hogwarts_legacy_reviews.csv')
 df
 ```
 
 |Index|Playtime|Feedback|Review|
 |---|---|---|---|
 |0|16|Positive|Greattt Game!|
 |1|26|Positive|9/10Fantastic experience. A true Wizarding World experience. ...|
 |2|29|Positive|worth it|
 |3|24|Positive|I've been waiting 84 YEARSSSSSSSS.The game is everything I could have hoped for and more.|
 |...|...|...|...|
 |46401|11|Positive|WORTH EVERY PENNY! LOTS TO DO ...|
 |46402|8|Positive|Awesome game! Awesome graphics, story line, and even combat. ...|
 |46403|1|Positive|Well yes, I'm transphobic how did you know?|
 |46404|6|Positive|I would take a Avada Kedavra and endure a Crucio for Professor ...|
 ### - 데이터 구성
 |데이터|구분|
 |---|---|
 |Index|번호|
 |Playtime|리뷰 기준 플레이 시간, 1시간 미만은 0으로 표시|
 |Feedback|Positive(긍정), Negative(부정)으로 나눔|
 |Review|리뷰|
 
 ### - 라벨, 분포, 부가정보
  - Index : 총 46404개의 리뷰<br/>
  - Playtime : 0~125시간 플레이시간<br/> <img src = "https://user-images.githubusercontent.com/79897716/231339975-de24721a-d26d-4bed-848d-761f1abf02c8.png" width="270" height="240">
<br/><br/>
  - Feedback : 92% 긍정(Positive) 8% 부정(Negative) <br/> <img src = "https://user-images.githubusercontent.com/79897716/232953272-a5538f34-0fcd-4e57-91ce-def8cbeb5546.png" width="370" height="370">
<br/><br/>
  - Review : 41433개의 고유의 값 <br/>![chart (1)](https://user-images.githubusercontent.com/79897716/235825321-c1bf5900-e574-42b5-bf20-b0cb5f28c451.png)<br/>


 ## 결론  
  플레이타임이 길어질수록 긍정적인 평가가 많아지기 때문에 플레이타임과 긍정 혹은 부정적인 리뷰의 관계는 큰 편이고 단순히 리뷰의 문장의 길이로만 보기에는 어떤 내용인지 봐야 하므로 리뷰의 길이와 긍정 혹은 부정적인 리뷰의 관계는 약한 편이다.  
  호그와트 레거시 게임의 긍정적인 리뷰가 92%가 된다는 것과 플레이타임이 긴 사람들의 리뷰가 긍정적이라는 것은 리뷰에 대해 신뢰감을 높이고 이를 유용하다고 판단해 후기에 영향을 받은 새롭게 게임을 구매할 구매자들이 늘어날 것이라고 본다.
  
 ## 출처
[1] https://namu.wiki/w/Steam <br/>
[2] https://www.itlab.co.kr/v7/?m=rssM&bid=column&cat=LG+CNS&sort=d_regis&orderby=desc&uid=27004 <br/>
[3] https://s-space.snu.ac.kr/handle/10371/166332
