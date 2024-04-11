# 개인 프로젝트
스피드 데이팅 성공요인 재분석


# 📌 들어가며

안녕하세요. 저는 개인프로젝트로 2023년 11월 9일부터 **스피드 데이트의 성공요인**을 분석하였습니다.

2021년에 진행했던 [같은 프로젝트](https://github.com/Da-Hye-JUNG/Speed-Dating)에서 분석 결과에 개인적인 아쉬움이 있었고, 그동안의 성장을 프로젝트에 녹여내고 싶었습니다.

또한, 많은 사람들이 시대가 변화함에 따라 **기존의 연애 방식에서 벗어나 다양한 방법을 통해 상대를 찾고** 있습니다. 그 중 온라인, 오프라인에서의 소개팅은 짝을 찾는 하나의 방법이라고 할 수 있으며 이들이 **소개팅에서 성공하는 요인을 이해하는 것은 그들의 연애 성공에 그치지 않고 더 나아가 연애 관련 프로그램 및 매칭 시스템 개발에 기여**할 수 있을 것이라 생각하여 분석을 결정하였습니다.

이번 프로젝트에서는 [**Kaggle**](https://www.kaggle.com/)의 스피드 데이팅 데이터를 활용하여 **데이터를 파악**하고 **정제과정**을 거친 후 남여가 이상형으로 생각하는 상대와 실제 선택한 상대의 특성을 비교하는 등 **의미있는 인사이트를 도출**하고 **모델링**을 통하여 요소들간의 조금 더 복잡한 관계를 파악하는 방식으로 분석하였습니다.

# 📌 프로젝트 개요

## 문제 정의

> 📰 결혼정보회사 듀오가 미혼남녀를 대상으로 연애 현황을 관련하여 설문조사한 결과  
>  
> 연애를 하고 있거나 썸(연애를 전제로 알아가는 단계)을 타고 있다고 답한 이들(남 39.2%, 여 48.8%)의 3명 중 1명(남 33.7%, 여 35.2%)은 ‘학교, 학원, 회사 등’에서, 남 19.4%, 여 15.6%는 ‘소개팅’으로 상대를 만난 것으로 나타났다.
> 
> 또한, 솔로남녀의 절반가량(남 51.3%, 여 38.3%)은 연애를 할 의향이 있다고 밝혔으며 연애 상대와의 선호하는 만남방식으로는 ‘학교, 학원, 회사 등에서의 만남’(남 34.8%, 여 30.8%)이었으며 남 15.2%, 여 10.8%이 ‘소개팅’을 꼽았다.
> 
> 해당 설문조사는 2022년 10월 12일부터 10월 14일까지 미혼남녀 500명 (남: 250명, 여: 250명)을 대상으로 진행되었으며 신뢰수준 95%에서 표본오차 ±4.38%p이다.
> 
> 박남수기자, “**듀오, 연애 현황 관련 설문조사 결과 발표”, 정보통신신문,** 2022-11-11

위 기사에서와 같이 소개팅은 연애에 있어서 큰 부분을 차지한다. 또한, 미혼남녀의 약 절반이 연애중이며 솔로남녀의 절반가량이 연애를 할 의향이 있다고 답한것으로 보아 **연애가 사회에서 큰 비중을 차지함을 알 수 있으며 이 중 소개팅이 연인을 찾는 효과적인 방법 중 한 가지**임을 알 수 있다.


> 📰 결혼정보업체 가연에 따르면 미혼남녀 187명(남 96명, 여 91명)을 대상으로 '소개팅 애프터를 결정하는 가장 큰 요인'에 대해 설문조사를 한 결과
> 
> '잘 맞는 대화코드'가 48.7%로 1위를 차지했다. 그 다음으로는 '통하는 느낌'(23.5%), '취향에 맞는 외모'(21.4%), '비슷한 취미 및 식성'(6.4%) 순으로 이어졌다.
> 
> “**봄 날씨 오니 소개팅 물결…`외모`보다 중요한 이것은?”, 매일경제,** 2020-04-30

이러한 설문조사 또한 유용한 정보이지만, 데이터 분석을 통해 **여러 변수들 간의 복잡한 관계를 분석하고 이해**함으로써 소개팅 애프터를 결정하는 요인에 대한 보다 포괄적인 이해를 얻을수 있다는 점에서 **매칭 성공에 영향을 주는 요인을 데이터 분석을 통해 파악해보고자 하였다.**

## 프로젝트 목표

✅ 지난 프로젝트에서의 부족한 점을 발견하고 그동안의 성장을 통해 얻은 방법들을 적용하여 재분석하기

✅ 소개팅의 성공요인을 분석하고 이를 토대로 소개팅에서의 효과적인 전략을 제안하기

## 데이터 소개

소개팅 성공에 영향을 주는 요인는 심리학적 요인과 환경적 요인 등 데이터화하기 어려운 요인들이 많을 것이라 생각한다. 따라서 최대한 상세한 데이터로 분석을 해야 더 신빙성 있는 결과가 나올 것이라 생각했다. 그에 적합한 데이터로 콜럼비아 경영대 교수의 논문 “Gender Differences in Mate Selection: Evidence From a Speed Dating Experiment”의 연구를 위해 형성된 데이터가 설문(개인 정보 데이터)과 경험(상대에 대한 평가 데이터)에 기반하여 만들어졌다는 점에서 적합하다고 생각했다.

### **주요 변수 소개**

| 변수명 | 변수 설명 | type | 예시 |
| --- | --- | --- | --- |
| iid | 참가자의 고유 번호 | int | 1,2,3, … |
| round  | 스피드 데이팅에서 만난 상대 수 | int | 6,18,22, … |
| match_es  | 예상 매칭 성공 수 | int | 0,8,12, … |
| prob | 상대방이 나를 선택할 가능성 | int | 0,3,10, … |
| impreling | 같은 종교인 것이 얼만큼 중요한지 | int | 1,5,4, … |
| exhappy  | 소개팅에 기대하는 정도 | int | 1,2,10, … |
| int_corr  | 사전조사가 상대와 비슷한 정도 (-1~1) | float | -0.25,0,0.4, … |
| goal | 참가 목적 | object | 1,2,5, … |
| match(Target) | 매칭 성공 여부 | category | 0(매칭X),1(매칭O) |



# 📌 프로젝트 수행 과정

## 지난 프로젝트와 다른 점

지난 프로젝트와 비교하여 다른 부분은 다음과 같다.

1. **데이터에 대한 정확한 이해 후 분석을 진행**

예시로, 설문조사 중 특성 요소에 대한 응답에서 wave6-9는 **절대적인 점수**로 응답(0부터 10사이 수)하였고, 나머지 wave는 **상대적인 점수**로 응답(합이 100이 되도록)하였기 때문에 **기준과 범위가 다르다는 문제**가 생겨 wave6-9를 제외하기로 결정하였다.

2. **데이터 수집 방식에 대한 이해를 데이터를 통해 알아낸 후에 분석을 진행**

이전에는 데이팅의 진행 및 데이터 수집 방식에 대한 이해 없이 분석을 진행하였으나 이번에는 데이터를 통해 알아낸 후에 분석하였으며 아래와 같다.

> 🗣️ 스피드 데이팅은 한 wave의 그룹 안에서 있는 모든 이성과 한번씩 동시에 진행되고 성비가 맞지 않더라도 남는 인원이 대기하는 방식으로 진행되어 모든 이성과 매치된다. 
> 여성은 같은 position을 가지고 남성은 모든 position을 가지고 있는 것으로 보아 남성이 자리를 옮기는 방식으로 진행된다.

이를 통해 스피드 데이팅 데이터를 기록하기 위한 요소 즉, 분석과 관계없는 요소가 있음(ex. positin1 - 맨 처음에 데이트한 상대와 만난 position)을 발견하였고 제거하였다.

3. **결측치와 이상치 처리과정에서 단순 제거가 아닌 명확한 근거와 함께 처리**

이전에는 결측값이 있는 행에 대하여 3개 이상의 결측값이 존재하면 해당 행을 삭제하는 방식을 사용했지만, 이번에는 하나하나 살펴보며 채울 수 있는 값을 확인하여 채워주었다. 

예를 들어, 설문조사에서 특성 요소의 합이 100이 되어야 하지만 설문 조사 참가자가 특정 항목에 대해 응답을 하지 않아 빈칸이 남아있을 경우, 해당 항목에 0을 주는 것이 적절하다고 판단하여 이를 0으로 채워주었다. 

<img width="743" alt="스크린샷 2024-04-08 오후 4 14 10" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/6f7ab06e-230f-4492-811a-ad2a97ca9fad">

이상치 처리과정에서의 예시로는, 설문조사시 입력값이 0부터 10까지의 범위를 가지는데, 0 미만이나 10 초과의 값을 가지는 경우에 대하여 **응답과** **입력 모두 사람이 하기에 발생한 이상치로 판단**하여 해당 값을 0 또는 10으로 대체하였다.

4. **변수 생성과정에서 상관관계를 시각화하여** **타당성을 부여**

지난 프로젝트에서는 변수를 임의로 선택하여 병합하는 방식으로 생성했지만, 이번에는 **히트맵으로 시각화한 상관관계를 참고하며 변수를 병합**하여 더욱 **유의미한 변수를 생성**하였다.

<img width="300" alt="스크린샷 2024-04-07 오후 10 32 05" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/3b08f6cb-009a-4885-bf2b-f4a8e0f03fe5">

> 🗣️ 서로 연관성이 높은 (0.4기준) 변수끼리 하나의 변수로 생성한다.
> museums + art + theater + concerts + movies + music -> `culture`
> exercise + sports + tvsports -> `active`
> 
> 나머지는 서로 연관성이 거의 없는 취미이므로 정적인 취미와 동적인 취미로 나누어 묶어주었다.
> hiking + yoga + clubbing -> `dynamic`
> dining + gaming + reading + tv + shopping -> `static`

5. **변수 제거 과정에서 가설을 세우고 상관계수를 확인**

> 🗣️ **가설 : `go_out`(외출횟수)와 `date`(데이트를얼마나자주하는지)가 비슷한 의미를 갖는다. (상관관계가 있을 것이다.)**

**상관계수**가 `0.33`, **p-value**가 `0에 매우 가까운 수`(7.705532e-167)이므로 두 변수가 약한 선형관계를 가지나 유의미한 상관계임을 확인하여 가설을 입증했다. 

**상관관계가 높은 변수는 모델의 성능을 저하**시킬 수 있으므로 이 중 연애과 관련이 상대적으로 적은 go_out변수를 제거하기로 결정하였다.

<img width="406" alt="스크린샷 2024-04-08 오후 4 21 21" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/aaad1932-3ce0-490a-b3f2-2ba53da0d7c4">


6. **모델의 성능을 저하할 수 있는 요소들을 제거**

`dec변수`는 상대와 애프터를 할지 말지 결정한 변수로, 이는 모델 학습에 있어 **치팅의 위험이 있기 때문에 제거**하였고
`like변수`는 상대에 대한 호감도를 나타내는 변수로, **결과에 직접적인 영향을 주기 때문에 제거**하여 **모델의 일반화 능력을 향상**시켰다.

## EDA

### **✅ 인사이트1 : 35세 이상의 참가자는 같은 종교 여부를 중요하게 생각한다.**

**`나이별로 소개팅에서 중요하게 생각하는 요소와 성공 요소가 다를것이라는 가설`을 세워** 35세 이상의 참가자들은 **같은 종교인 것이 얼마나 중요한지** 나타내는 변수 ‘imprelig’에서 **높은 점수에 많이 응답**하였음을 확인하였다.

<img width="294" alt="스크린샷 2024-04-01 오후 9 15 45" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/32d41eec-6fcf-4ac6-af7b-03065966eef9">

추가로, 매칭 여부에 따른 imprelig의 분포를 확인해 보았을 때 30대 초반 그룹에서는 매칭이 된 경우에서 더 높은 점수에 분포하고 35세 이상 그룹에서는 **매칭이 안된 경우에서 더 높은 점수**에 분포한다.

<img width="482" alt="스크린샷 2024-04-02 오후 6 26 59" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/85fc88e6-bee4-4df6-b3c9-5f4ffd7c20c7">

이를 통해 **35세 이상은 같은 종교임을 중요하게 생각한다**는 것을 다시한번 알 수 있다.

### **✅ 인사이트2 : 이상형과 실제로 선택한 상대의 특성은 다르다.**

<img width="903" alt="스크린샷 2024-04-01 오후 9 41 02" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/57f14fca-ceb4-4fd6-a091-0f35f97ef04a">

**`성별 별로 소개팅에서 중요하게 생각하는 요소와 성공 요소가 다를 것이라는 가설`을 세워 이상형**으로 **남성은 매력**을, **여성은 지성**에 가장 높은 점수를 주었으며

**실제로 선택**한 상대에게 **여성은 지성**에서 높은 점수를 주었고, **남성은 거의 모든 특성에서 비슷**한 점수를 주었음을 확인하였다.

이를 통해 이상형과 실제로 선택한 상대의 **특성에 매긴 점수가 다르다**는 것을 알 수 있다.

### **✅ 인사이트3 : 집순이, 집돌이들의 소개팅 성공률은 낮다.**

`집순이, 집돌이일수록 소개팅 성공률이 낮을 것이라는 **가설**`을 세워 **외출빈도에 따른 매칭률**을 확인한 결과 **밖을 많이 나가지 않을 수록 소개팅 성공률이 낮음**을 확인하였다.

여기서 **숫자가 낮을수록 더 자주 외출**하는 것을 나타내며, 특히 7은 거의 외출하지 않음을 나타낸다. 따라서 **가설이 입증**되었음을 확인할 수 있다.

<img width="506" alt="스크린샷 2024-04-02 오후 7 53 08" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/15aa9027-f3b5-48ec-913e-760bf7672d6f">

### **✅ 인사이트4 : 같은 직업, 분야를 가진 상대와의 소개팅 성공률은 높다.**

<img width="888" alt="스크린샷 2024-04-02 오후 7 54 37" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/457e9106-c647-44dc-ab8f-c27efb1c4905">

**`같은 직업, 분야일수록 소개팅 성공률은 높을 것이라는 가설`을 세워 같은 직업이나 분야를 가진 상대**와 소개팅한 경우에서 소개팅 **성공률이 상대적으로 높음**을 확인하였다.

특히, 같은 분야일 때의 소개팅 성공률의 평균이 약 0.1 더 높음을 확인하였다.

여기서 **1이 매칭된 경우**이다.

## 모델링

> **랜덤 포레스트**
> 
> 랜덤 포레스트는 다양한 트리들을 생성하고 그들의 예측을 결합함으로써 높은 성능을 제공하여 과적합을 줄이고, 안정적인 예측을 할 수 있다.


앞서 남녀가 응답에 있어 차이를 보임을 확인하여 **나누어 모델링을 진행**하기로 결정하였다.

### **남성에 대하여 모델링한 결과**

<img width="714" alt="스크린샷 2024-04-08 오후 10 41 00" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/388f6dd3-c87d-4fb8-9840-c9c70c58f025">

<img width="703" alt="스크린샷 2024-04-08 오후 7 25 48" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/b564ac02-ce5d-41e2-bee9-1afa54bfa3e2">

남성의 모델링 결과 변수 중요도가 비슷함, 매력, 재미, 상대와 나와 일치하는 정도 순으로 나타났으며 모델 평가 결과는 오른쪽과 같다.

### **여성에 대하여 모델링한 결과**

<img width="707" alt="스크린샷 2024-04-08 오후 10 43 28" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/7ccf9d0b-0128-4a14-8e7d-b83cc5ae7558">

<img width="704" alt="스크린샷 2024-04-08 오후 10 42 32" src="https://github.com/Da-Hye-JUNG/RE-Speed-Dating/assets/96599427/c72bf94f-75c9-4ee0-9c3d-a00e309ee004">

여성의 모델링 결과 변수 중요도가 비슷함, 매력, 진실성, 재미, 상대와 나와 일치하는 정도 순으로 나타났으며 모델 평가 결과는 오른쪽과 같다.

# 📌 프로젝트 결과

---

여성과 남성 모두 비슷함, 매력, 재미, 상대와 내가 일치하는 정도 순으로 중요하게 생각함을 알 수 있다.

또한, 위의 EDA결과를 통해 같은 분야의 사람들을 매칭하고, 35세 이상의 참가자는 같은 종교의 참가자와 매칭하는 등 실질적인 도움이 될 수 있는 **인사이트를 발견**하였다.

이러한 인사이트를 기반으로 **소개팅에서의 전략을 수립**하고, **매칭 가능성이 높은 참가자를 연결하는 모델**을 개발함으로써 연애 성공 요인을 이해하는 것을 넘어서서 **실제 연애 관련 프로그램 및 매칭 시스템 개발에 기여**할 수 있다고 생각한다.

# 📌 감사합니다.

---

이것으로 개인프로젝트 `스피드 데이팅 성공요인 분석` 소개를 마칩니다. 감사합니다.
