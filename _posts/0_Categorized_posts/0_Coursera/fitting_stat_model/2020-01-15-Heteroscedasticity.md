---
title: wikipedia - Heteroscedasticity
category: others
tags: GLM GEE statistics Heteroscedasticity
---

## intro: back to the basic. 

- 최근에 기본적인 통계들과 선형방정식을 활용한 다양한 기법들을 정리하고 있습니다. 사실, 뉴럴 넷이 나온 다음부터는 거의 사람들이 언급하지 않는 것이기는 하죠. 뉴럴넷은 어쩌면, 좀 그냥 '돌려보니까 좋았더라, 그냥 막 돌려보고 가장 좋은 것을 고르자'에 가까운 이야기들이니까요. 
- 그런데, 통계에서는 '데이터 자체에 내재되어 있는 문제 혹은 한계'를 좀 더 과학적으로 풀려고 합니다. 가령, 이 데이터는 이 분포를 따른다고 할 수 있는가? 이 데이터는 모두 같은 분포에 속한다고 할 수 있을까? 그렇다면, 이 오차를 줄이기 위해서는 어떤 모델을 쓰는 것이 타당할까? 와 같은, 비교적 탄탄한 백그라운드가 필요하죠. 
- 다시, 머신러닝으로 돌아와서 보면, 머신러닝(특히 뉴럴넷)은, 이 부분에 대한 고찰이 비교적 떨어집니다. "그냥 쓰고 제일 좋은 놈을 골라"와 같이, 약간은 무모하게 선택하죠. 뭐, 맞는 말이기도 하지만, 음. 뭔가, 예술적이지는 않아요. 그렇죠? 
- 결국, 통계를 다시 제대로 공부할 필요성이 있다고 느낍니다. 그래서, 통계를 공부하다가 나온 낯선 개념들을 다시 이렇게 정리해보기로 했습니다.

## What is Heteroscedasticity? 

- 한국말로 Heteroscedasticity를 어떻게 해석해야 할지 모르겠습니다. 심지어 발음도 어려워요. 
    - hetero: "different", "서로 다름"
    - scedasticity: "the distribution of error term", 오차항의 분포 
- 즉, "서로 다른 오차항 분포"를 의미합니다. 뱀발로, 영어단어를 한국단어로 변환했을 때 그 "직관적으로 이해되는 정도"는 정말 최악이라고 생각해요. 젊은 세대는 심지어, 이제 "한자어"에 익숙하지도 않지만, 대부분의 학술어들은 한자어로 표현되어 있습니다. 한국어로 누가 잘 설명을 해두어도, 각 개념들이 영어로 되어 있지 않으면, 매번 서로 다른 두뇌를 섞어서 써야 하는 느낌이에요. 그러니까, 여러분 유학가세요.
- 아무튼 다시 돌아와서, "서로 다른 오차항 분포"라는 말에서 알 수 있는 것은, 데이터 세트에 수집된 데이터들이 "동일한 평균/분산을 가지지 않고 각기 다른 분포 위에서 돌아간다"라는 것이겠죠. 혹은 무엇인가에 따라서 변화하고 있다는 말입니다. 

## heteroscedasticiy in wikipeida

- 통계에서 "수집된 랜덤 변수들이 heteroscedastic하다"라는 말은 그 집합의 sub-population(부분 집합)들이 서로 다른 변동성(variability)를 가지고 있다는 것을 말합니다. 여기서, "variability"는 통계적으로 '분산된 정도'를 의미하는 어떤 지표든 포함되겠으나, 보통 variance가 되겠죠.
    - 즉, heteroscedasticity는 [homoscedasticity](https://en.wikipedia.org/wiki/Homoscedasticity)의 부재라고 볼 수 있습니다. homoscedasticity는 homogeneity of variance, 즉 분산의 일관성이라는 말이죠.
- 즉, `e`라고 한다면, 이 아이가 그냥 `norm(0, 1)`인 것이 아니라, 어떤 특정 변수 `a`등에 따라서 변한다는 것이죠. 커질 수도 있고, 작아질 수도 있고. 즉, **현재 충분히 통제되어 있지 않다** 라고 말할 수 있습니다.
- 이처럼, heteroscedasticiy의 존재는 
regression analysis, anova 분석 등에서 기본적으로 error 간에 서로 상관성이 없고(uncorrelated), uniform하다고 가정하기 때문에, 분산 자체가 바뀌지 않는다고 가정하고, 모델링한하기 때문에, 매우 중요하게 고려되어야 하는 사항이 되죠.
- 예를 들어, OLS(ordinary least square)로 만든 estimator가 heteroscedasticity의 존재가 있을 때도 여전히 unbiased일 수는 있지만,  진짜, variance는 물론, covariance가 과소평가되었으므로, 비효율적이 되고, 비슷하게, 서로 다른 두 집단 간의 차이를 알기 위해 test를 진행한다고 할 때에도, 이 테스트는 보통 variance가 같다고 가정하고 진행된다. 여기서, heteroscedasticity는 평균(first moment)과는 관련이 없고, 분산(second moment)과 관련있기 때문인데, 잘못된 variance에 대해서 두 평균이 같다고 결론을 내릴 경우 틀린 결론을 내리게 되는 것이죠. 

### Examples

- Heteroscedasticity의 고전적인 예로, "수입"과 "식비"를 말할 수 있습니다. "음식 소비 금액"이 올라가면서, "음식 소비 금액"의 변동성이 커지게 됩니다. 가난한 사람은 비싸지 않은 음식들만 항상 먹는 반면, 부유한 사람들은 종종 싼 음식과 비싼 음식을 모두 먹게 되죠. 따라서, 고소득의 고객 층들은 "음식 소비 금액"에서 큰 변동성을 가지게 됩니다. 즉, 데이터세트에 '가난한 사람'과 '부유한 사람'이 혼재되어 있고, 수입이 커짐에 따라서, 이 때 발생하는 식비의 분산 정도가 커지게 됨에도 불구하고, 그냥 "수입 ~ 식비" 등으로 모델링을 할 경우에는 Heteroscedasticity가 컨트롤되지 못한 상황이라는 것이죠.

### Multivariate case

- heteroscedasticity에 대한 연구는 다변수, 다변량(multivariate)의 케이스로 확장될 수 있으며, variance를 고정값으로 두는 것이 아니라, covariance matrix를 사용하여, 분산도를 다변량 적으로 측정하는 것이 하나의 방법이 됩니다.

## wrap-up 

- 복잡하게 써있지만, 오히려 '시간'이라는 축을 가지고 보는 것이 훨씬 이해가 쉽습니다. 우리가 1년 365일 동안 매일 "온도(T)"라는 데이터를 수집했다고 합시다. 그런데, 1년동안 점차 하루의 온도차가 심해지는 것이죠. 1년의 마지막 날에는 영하 10도에서 영상 20도를 오갔다고 할게요. 만약 이 때 first moment는 똑같다고 해도, second moment인 분산은 극심하게 차이가 납니다. 하지만, 기본적인 regression에서는 이를 가정하고 있지 않습니다. 따라서, error라는 것 자체도 고정된 분포를 가진다고 두는 것이 아니라, 하나의 벡터로서 관리해서 처리해줘야 한다는 것이죠. 