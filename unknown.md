
---
title: "Untitled"
output: 
  html_document:
    number_sections: true
---

```{r, setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE)
```










최종적으로 획득한 시각화 결과값을 통해 최신 논문 트렌드를 서술하는 것으로 



본 논문에서는 불특정 다수의 latent space model 알고리즘을 구현하였고 

word2vec을 통해 전처리하여

해당 과정의 도중 데이터가 부족할 상황을 상정하여 Biterm model 의 방법론을 활용하여 총 corpus 개수를 늘리는 작업을 병행하였다.

위의 알고리즘을 python 기반으로 구현하였으며 속도 퍼포먼스의 향상을 위해 c++을 접합하여 대량의 계산을 필요로 하는 부분을 c++로 처리하였다. 본 논문에서는 해당 구현의 결과값이 유효하다는 것을 증명하고자 

동일 주제를 갖는 Web of Science에서 논문 abstract 들을 크롤링하여 이를 대상으로

한 후

이의 iteration을 반복하여 해당 통계량들의 변화 추이를 서술하는 것으로 

작동성을 증명하고자 하였다.



# 서 론
## 연구 배경 


현대에 들어서는 분야별로 전문성이 심화되고 있으며 해당 분야에 대한 전문적인 지식 없이는 해당 분야를 얕게나마 이해하는 것도 벅차지고 있습니다. 그럼에도 통섭이라는 단어로 대표되는 분야 간의 협업 및 심화된 전문영역간의 상호교류의 수요는 계속해서 높아지고 있는 상황입니다. 이런 상황에서 각 분야에 대한 지식 없이는 협업의 생산성이 담보되지 않으면서도, 생산성을 갖추기 위해 해당 분야의 공부에 시간을 투자하기에는 자신의 분야에 집중하는 것만 해도 시간이 부족하다는 진퇴양난의 상황이 발생합니다.

Graph-based Trajectory Visualization for Text Mining of COVID-19 Biomedical Literature 논문은 이러한 상황을 타파하기 위해 해당 분야와 관련된 documents 들을 이용하는 것을 제안합니다. 해당 분야와 관련된 대량의 documents 들을 획득한 후 이에 해당 알고리즘을 적용하여 시각화 하는 것으로 해당 분야에 대한 documents 들의 주제들을 개략적으로 하나의 단어로 표시한 후, 이를 2차원 그래프에 배치하는 것으로 해당 주제들 간의 관계성을 드러내는 것이 가능합니다. 이를 통해 분야에 대한 지식 없이도 분야에 관한 documents 들의 흐름을 통해 피상적으로나마 해당 분야를 개괄적으로 파악하여 해당 분야에 엮인 외부인에게 요구되는 노력을 줄일 수 있다고 기대합니다. 이러한 목적을 달성하기 위해 해당 알고리즘을 독립적인 패키지로 배포하고자 하는 것이 해당 프로젝트의 목표였습니다. 












## 연구 목적 



이렇듯 해당 논문은 분야를 이해하는데 있어 유효한 도구가 될 수 있는 알고리즘을 제공하고 있습니다. 그러나 구현과정에서 각종 통계학 이론 및 분포, 그리고 딥러닝 처리방법을 사용하기 있기 때문에 통계학 지식이 부족한 연구자들이 해당 알고리즘을 사용해내는 것은 그다지 쉬운 일이 아닙니다. 이는 곧 연구자로 하여금 해당 알고리즘을 구현하여 실사용하기 위해서는 추가적인 통계적 지식 및 기초적인 프로그래밍 지식을 요한다는 것과 같은 의미이며, 이는 곧 통계적 역량이 부족한 연구자들에게 목적으로 하는 분야 이외에 통계학적인 지식 또한 요구하는 상황이 되고 맙니다. 해당 알고리즘 수요자에게 이렇듯 추가적인 부담을 지우는 것은 트렌드 분석을 용이하게 하고자 했던 당초의 목적과는 상반된다고 말할 수 있습니다. 따라서 이러한 불편함을 덜어주기 위해 해당 알고리즘을 분석한 후 일련의 과정을 코드로 작성한 후 하나의 패키지화 하여 배포하는 것은 충분한 실익이 있다고 말할 수 있습니다.

이러한 목적 아래서 본 논문의 내용은 다음과 같습니다. 우선 해당 알고리즘의 바탕으로 하고 있는 이론들과 기초적인 흐름을 서술합니다. 그 후 다양한 프로그래밍 언어들 중 해당 언어를 채택한 이유와, 해당 언어를 통해 구현하는 과정에서 고려되었던 사항들과 실구현 과정을 서술하겠습니다. 이때 실구현 과정에서 마주친 문제점들과 해당 문제점들에 대한 해결책을 제시합니다. 마지막으로 해결책을 적용한 구현 방법론을 통해 해당 알고리즘을 구현한 패키지의 사용법을 서술하고, 실제 데이터를 사용하여 해당 패키지의 퍼포먼스를 보일 것입니다.












# Method




해당 알고리즘이 목표로 하는 바는 명확합니다. 

다수의 




이때 문단의 길이가 길면 길수록 하나의 글줄에서 주제를 파악하기 위해 사용되는 corpus 의 숫자는 늘어나며, 그 숫자가 늘어남에 따라 글줄의 주제를 한두단어로 갈무리하고자 하는 시도는 더욱 어려워질수밖에 없습니다. 따라서 이러한 목적에 맞는 성질이 도드라지는 결과값을 얻기 위해서는 문단의 길이가 짧으면서도 문단 자체가 강력한 힘을 가지는 부류의 글줄을 사용하는 것이 최선입니다. 이런 성질을 가지는 글줄의 종류로는 기사의 서문, 정부발표 요약문, 그리고 논문의 abstract 등을 생각해볼 수 있을 것입니다.







## Biterm






### 2.1.1 



자연어 처리가 필요. 개별 글줄에서 corpus를 추출한 후 

풍부하게 하기 위하여 단어 벡터들 간의 유사도를 계산해낼 필요가 있다.

이를 위해 ‘비슷한 의미를 가지는 단어들은 비슷한 문맥에서 등장한다’ 는 가정 하에서 각 단어가 보유하는 스테이터스를 부여하고 

Word-To-Vector, 속칭 word2vec 알고리즘을 활용하여 


**Why word2vec?**

다른 알고리즘 많잖아. 

자연어 전처리는 큰 틀에서 둘. Frequency based Embedding(주파수 기반 임베딩) 과 Prediction based Vector(예측 기반 임베딩). 
후자를 word2vec 이라고 부르며, 이는 단일 알고리즘이 아닌 Continuous Bag Of Words (CBOW) 와 Skip-Gram Model 둘의 조합. 전자의 경우에는 BOW, CountVectorizor, TF-IDF 등 여러가지 방법론이 있지만 전부 공통적으로 Frequency, 즉 단어의 횟수로 확률을 판정하여 부여함. 반면 Prediction 은 






### 3줄 요약

3줄 요약에 주되게 사용되는 서비스는

tokenize 기법

추출적 방식

추상적 방식











### 2.1.2 




이때 1차적으로 그러나 input 하는 글줄의 양도 적을 뿐더러 같은 분야의 글줄들을 다루기 때문에 개별 글줄마다의 특성을 통계적으로 파악하기에 충분하지 않을 정도로 개별 글줄들이 고유하게 가지는 단어의 갯수가 적을 수 있음

이를 보완하기 위해서 Biterm Model을 도입.^[Xiaohui Yan, A Biterm Topic Model for Short Texts]




Biterm Model 은 본질적으로 통계적 확률을 가리기 위한 재료의 가짓수가 적을 경우 이를 판단하기 위한 재료를 늘리기 위한 과정

Biterm Model 은 다음과 같은 가정에 존재.

- 두 단어는 겉보기로 인식할 수 없는 단어의 클러스터에 함께 속한다
- 각 글줄에는 인식할 수 없는 주제가 존재하며, 각각의 주제 내부에는 유사한 의미를 보유하는 단어들이 모여있다
- 인식할 수 없는 단어의 클러스터가 함께 속해있는 그것을, 인식할 수 없는 주제라고 인식할 수 있다







이러한 Biterm Model 은 본질적으로 사용 가능한 corpus 의 양을 늘리고자 하는 것입니다. 원본 문서에서 corpus의 갯수가 $n$ 개였다면 Biterm 과정을 거치는 것으로 $n^2$으로 확률 추정에 사용되는 샘플들의 갯수를 늘리는 것이 가능하다는 것입니다. 이렇게 샘플을 늘린 것으로 개별 단어의 확률을 

이렇게 늘려서 획득한 각 corpus pair 들의 확률에서 개별 단어들의 확률 획득 가능.

**원본 corpus 만으로 진행하는 거랑 무슨 차이가 있는지를 서술해야 함**

1. $\theta \sim Dirichlet(\alpha)$ 로부터 모든 주제들의 분포를 샘플링.
2. Biterm set B 의 각 biterm b 에 대해, 해당 biterm을 구성하는 2개의 단어의 합이 전체 주제들 중 어느 주제 z에 속하는지를 샘플링. 이때 $z \sim Mult(\theta)$.
3. 주제가 주어졌을 경우의 단어의 분포, 즉 주제 z의 topic-word 분포를 샘플링. 이때 $\phi_z \sim Dirichlet(\beta)$.
4. topic-word 분포로부터 골라진 topic z 에 대응하는 각 두 단어들의 출현 확률을 샘플링. 이때 $w_i, w_j \sim Mult(\phi_z)$.

이의 단계를 모두 거치는 것으로, 모든 biterm set $B$ 의 joint likelihood 는 이하와 같이 표현될 수 있다.

$$
p(B) = \prod_{i,j} \sum_z \theta_z \phi_{i|z} \phi_{j|z}
$$



이에 의해 latent topic z 의 조건부 posterior 는 이하와 같은 비례식을 따른다.

$$
p(z | z_{-b} , B, \alpha, \beta) \propto (n_z + \alpha) \frac{(n_{w_i}+\beta)(n_{w_{j|z}}+\beta)}{(\sum_w n_{w|z}+M \beta)^2}
$$



- $n_z$: biterm  가 주제 z에 할당된 횟수
- $n_{-b}$: biterm b 가 포함되지 않았던 주제들
- $n_{w|z}$: 주제 z에 할당된 단어 w 의 횟수






이때 $p(z | z_{-b} , B, \alpha, \beta)$ 에의 깁스 샘플링의 직접적인 적용은 변수들 간의 dependency 때문에 convergence 로 이르지 못할 우려를 배제할 수 없음. 따라서 우리는 collapsed 깁스 샘플링을 사용하여 불필요한 패러미터들을 integrate out  하여 이의 영향을 억제한다. 이때 prior 을 $dirichlet$ 으로 사용한 것의 이득을 볼 수 있다. $dirichlet$ 을 사용한 것으로 $\phi_z$ 와 $\theta$ 가 integrate out 당하므로. 몇번의 iteration 이후 우리는 획득한 statistics (통계량) $\n_{w|z}$ 와 $\theta_z$ 를 활용하여 $\phi_{w|z}$ 와 $\theta_z$ 의 distribution 을 이하와 같이 구성할 수 있게 된다.

$$
\phi_{w|z} = \frac{n_{w|z}}{\sum_w n_{w|z} + M \beta}, \; \; \; \; \; \theta_z = \frac{n+\alpha}{|B| + K \alpha}
$$

- $M$: 획득해두었던 corpus 의 총 갯수
- $B$: 넘버링된 각 biterm
- $K$: 설정한 총 topic 의 갯수


이제 해당 biterm을 쓰는 것으로 우리는 



이제 우리는 주제군 하에서의 corpus 분포 $\phi_{w|z}$ 와 주제 자체의 출현 분포 $\theta_z$ 을 획득했음.

우리가 목표로 하는 것은 글줄 모음에서 얻을 수 있는 각 주제별의 상관관계
지금까지 진행한 작업으로
주제별로 coefficient 를 얻어서 배치하는 건 가능하나 각 주제를 이름붙일 수 없으면 이는 무의미

따라서 이렇게 획득한 각 주제 하에서의 단어 출현 확률에서 각 주제를 어떻게 이름붙일것인가에 대한 재료를 확보해야함

이에 가장 직접적으로 활용할 수 있는 재료는 앞서 획득한 단어별 발생 확률

타 문서에서의 발생 확률이 낮고, 해당 주제군에 속하는 문서들에서만 여러번 발생하는 단어들이라면 해당 단어는 해당 주제군에만 묶여 있다는 것으로 해석할 수 있으며, 이는 곧 해당 주제를 어떻게 이름붙일것인가 하는 고민에서 유의미하게 활용될 수 있을 것

따라서 해당 고민을 해결하고자 하는 과정에는 모든 단어를 참고해서는 안되고 다른 주제군에서는 출현빈도가 낮고, 이 주제군에서는 높다는 조건을 만족해야함

이 조건을 해결하기 위한 기준으로서 

우리는 앞서 $M \times K$ 크기의 matrix 를 획득하였음. 이때 각 row 는 개별 단어의 각 주제군에서의 출현도, 각 column 은 각 주제군에서의 개별 단어의 출현율이 됨. 

여기서 우리는 각 row 에서의 coefficient variation 과 maximum probability 를 활용할 것. 전자는 주제군별 단어 출현 확률의 변동 정도를, 후자는 특정 주제에 단어가 얼마나 강하게 묶여 있는지에 대한 척도가 됨. 


BTM 은 topic-word distribution 을 생산하며, 이는 각 주제들 내부에서 각 단어의 확률을 측정하므로, 우리는 이들의 variation 을 조정해주어야 한다. 단순히 variance 를 측정하는 것만으로는 불충분. 따라서 우리는 standard deviation 을 각 주제군에서 획득한 각 단어의 확률의 평균으로 나눔하며, 이것이 곧 ```coefficient variation```이다.

행렬 $X_i$의 각 행에서 단어를 선택하는 기준으로 계수 변동과 최대 확률을 선택하는 두 가지 이유가 있습니다. 

첫째, 중요한 단어는 주제 간에 변동성이 낮으면 그 단어가 구체적으로 어떤 주제를 나타내지 않을 가능성이 높다. 따라서 확률의 variation 이 높은 단어야말로 주제를 판정함에 있어 유의미한 선택지로 판단될 수 있다. 따라서 의미 있는 단어를 판정함에 있어 variation을 사용하는 것은 타당하며, 여기서 coefficient variation 을 사용하는 것으로 더더욱 주제군간 topic 의 dispersion 을 증폭시키는 것이 가능하다.

두 번째, 의미 있는 단어가 되기 위해서는 적어도 하나의 주제에서 가능성이 높아야 합니다. 예를 들어, 단어의 variation 이 높다고 한들 그 어느 주제군에서도 높은 확률을 보이고 있지 못한다면 이는 결국 해당 주제군을 표현한다고 하기 어려우며 주제군을 표현함에 있어 기능을 다하기 어렵다. 그렇기 때문에 적어도 하나의 주제에서 확률이 높은 단어와, 앞문단에서 언급하였듯 변화가 큰 단어를 선택한다는 두가지 기준을 통해 효과적으로 주제를 특징지을 수 있습니다.





```


BTM 을 적용하기 위해 우리는 topic 갯수를 20으로 지정. hyper 패러미터로서는 $\alpha=3, \beta=0.01$ 을 부여. 궁극적인 목표는 topic 간의 관계를 시각화하는 것이기에 이에 필요한 hyper 패러미터는 empirically 결정하였다. topic-word 의 posterior 분포, 즉 BTM 과정 자체는 Gibbs Sampler 를 통해 결정되었으며, 이는 20000번의 burn-in, 55000 회의 iteration, 그리고 100 iteration 마다 thining 진행.


BTM 으로부터 획득한 각 topic-word 분포에서, 각 주제군들 하에서 높은 출현확률을 보이는 단어야말로 해당 주제를 특징짓기 적합함.

이에 대해서는 각 주제군들 별로 부여된 각 단어들의 확률의 로그 히스토그램을 구하면

bimodal 한 형태

좌측의 mode 는 낮은 확률, 즉 주제를 특징짓기 부적합한 라인업들이며, 우측의 mode 는 높은 확률로 출현하는 단어들.

따라서 noise 를 줄이기 위해 topic relationship 을 우측의 mode 에 등장하는 단어들만을 참고하여 판정하는 것은 실로 합리적일 것. 

이 히스토그램에 기반하여 최하 cutoff value, normal distribution의 최한도를 결정하는, 은 

우리는 

topic 을 유의미하게 표현하기 위해선 최소한 1000개의 단어가 필요함을 empirically

이 rationale 을 기반으로 하여 우리는 적어도 1000개의 단어는 사용하기로 결정

topic 의 특징을 추출하기 위한 단어의 기준선으로 우리는 

1. topic과 topic 간에 variance 가 큼 - coefficient variation
2. max probability 가 상대적으로 높음 - max probability

의 2가지 기준을 만족하는 단어들을 골라냈음. 해당 논문에서는 정해진 갯수의 단어를 사용하기 보다는 다른 갯수의 단어들을 사용하는 것으로 발생하는 변화를 관측하고자 하였음. **가령 포함하는 단어의 수가 변동함에 따라 topic 의 latent coordinate 가 격렬하게 변동한다면 이는 주제군으로 성립하기는 조금 어렵거나 주제군이 다루고 있는 바운더리가 넓어 그때그때 변동함을 의미할 것.** 특히, 우리는 다양한 매트릭스를 획득했다. 40%~60% 사이를 이용. 









이의 실적용에서는 상대적 편의를 위하여 

topic 들의 latent position 들 $\mathbf V = \{\mathbf v_i\}$ 를 획득ㄱ하기 위해 MCMC 가 적용되었다. MCMC 는 iteration 55000회, burn-in 5000회, thining 5. 해당 MCMC에 사용된 패러미터는 이하와 같다. 주제군들 간의 관계를 시각화하기 위해 우리는 2차원 Euclidean space 를 사용. 사용된 패러미터는 이하와 같다.

jumping 룰에 관해서는:
```
$$
\alpha = ?
\\
\beta = 0.28
\\
\theta = 1
\\
w_k = z_i = 0.06
$$

$$
prior \beta = fixed
\\
\theta \sim N(0,1)
\\
a_\sigma = b_\sigma = 0.001
$$

```
LSIRM 은 앞단계에서 이루어진 X_i 를 받아 결과값으로 $A_i$ 를 내놓는다. 이에 proc2와 oblim 을 적용하는 것으로 최종적 시각화에 사용될 matrix 를 내놓을 예정. 



topicnaming 에는 $A_max$ 를 활용하여 주제군별로 높게 랭킹된 단어를 활용하여 topic naming 진행. 왜? baseline matrix 야말로 topic 들을 characterize 함에 있어 가장 연고한 dependency 구조를 보유하고 있으니까. 



```

























### 2.1.3 Latent Space Item Response Model  


해당 단계에서는 위에서 획득한 단어들의 출현빈도를 사용하여 각 주제군들 간의 관계성을 확인하고 이 관계성을 interaction map 에 표시하여 각 글줄들 간의 관계를 구성한다.

원본: Latent Space Model, 네트워크에서의 각 actor (node) 들의 unobserved space 에서의 관계를 표현
후속: Latent Space Item Response Model (LSIRM). item response 를 biparite nwtwrok 로 인식하고, respondent 와 item 간의 관계를 latent space 를 사용하여 획득하는 가ㅓㅅ]

LSIRM 은 이하의 2가지로 모델링된다.

- Attribute: 특정 item 에 몇 명의 응답자가 응답했는지와, 특정 응답자들에 의해 몇 개의 item 이 응답되었는가
- Interaction: 각 item과 응답자의 latent position, 그리고 item 과 응답자 사이의 interaction을 측정

이를 응용하는 것으로 목표하는 바 달성 가능

해당 알고리즘의 목적은 주제 간의 관계를 추정하는 것과, 각 주제들에 연관된 단어를 근거로 하여 interaction map에서 주제의 latent position을 추정하는 것.

즉 topic 간의 관계를 획득하고 이 관계를 나타내는 coefficient 들을 연관된 단어를 기반으로 하여 interaction map 에 표방하고자 하는 일련의 과정을


앞서 획득한 $\phi_{w|z}$ 의 matrix $X_i$ 를 biparite network 로 인식하자. 이때 topic 은 item, respondent 은 word 가 된다.


|topic|item|
|word|respondent|


이는 위에서 서술한 LSIRM에서 

단 본디 원본 LSIRM 은 binary 데이터를 서술하기 위해 작성. 따라서 해당 문제에 직접 적용은 불가하다. 해당 문제의 경우 word2vec을 거쳐 각 단어의 출현 확률에 0에서 1 사이의 실수값을 부여하였기에 binary 모델이 아닌 Gaussian 버전. 이를 보정하기 위하여 해당 문제의 기본 아이디어만을 살리고 사용하는 확률을 Gaussian 확률로 변경하는 것으로 해당 문제를 보완 가능.

해당 문제를 보정하기 위하여 

모델을 Gaussian 버전으로 변경.


binary 가 아닌 Gaussian 용도로 변형된 LSIRM 은 이하와 같이 서술될 수 있다.


$$
x_{i,j}|\Theta = \theta_j + \beta+ \| \pmb u_i - \pmb v_j \| + \epsilon_{j,i}
$$


- $\epsilon_{j,i} \sim N(0, \sigma^2)$
- $i= 1\sim P$, $j=1\sim N$
- $x_{j,i}$: 단어 $x$가 주제 $i$에 속할 확률 (횟수?)
- $\Theta = \bigg\{ \pmb \theta= \{\theta_j\}, \pmb \beta= \{\beta_j\}, \pmb U = \{u_j\}, 	\pmb V = \{v_j\} \bigg\}$
- $\| u_i - v_j \|$: 단어 i 와 주제 j 각각의 latent position 사이의 Euclidean Distance.

원본 LSIRM 의 경우 binary 자료를 연속형으로 변환하기 위해 logit link 함수를 사용했음.

따라서 여기서 우리는 interaction 부분, attribute 부분과 $x_{j,i}$ 사이의 선형성 가정을 이용. normality equation을 만족시키기 위해 error term $\epsilon_{i,j}$ 를 추가.

이때 $\| u_i - v_j \|$ 가 짧을 경우, 이는 곧 word 의 latent position $u_i$ 와 topic 의 latent position $v_j$ 의 연관성이 존재할 가능성이 높다는 것을 의미하며, 이는 곧 word $i$ 가 topic $j$ 에 link 되어 있을 확률이 높음을 암시. 따라서, topic 의 latent position 은 word 들과의 거리에 기반하여 측정되는 것이 가능하다.

위에 주어진 모델을 given 했을 때, 우리는 LSIRM 의 gaussian 버전에서의 패러미터를 측정하기 위해 베이지안 추론을 활용하였다. 우리는 패러미터에 대한 prior 분포를 이하와 같이 특정한다:



$$
\begin{alignedat}{2}
\beta_{i} \mid \tau_{\beta}^{2} & \sim \mathrm{N}\left(0, \tau_{\beta}^{2}\right), &&\quad \tau_{\beta}^{2}&&>0 \\
\theta_{j} \mid \sigma^{2} & \sim \mathrm{N}\left(0, \sigma_{\theta}^{2}\right), &&\quad \sigma^{2}&&>0 \\
\sigma^{2} & \sim \operatorname{Inv-Gamma}(a, b), &&\quad a &&> 0, \quad b>0 \\
\sigma_{\theta}^{2} & \sim \operatorname{Inv-Gamma}\left(a_{\sigma}, b_{\sigma}\right), &&\quad a_{\sigma}&&>0, \quad b_{\sigma}>0 \\
\mathbf{u}_{\mathbf{j}} & \sim \mathrm{MVN}_{d}\left(\mathbf{0}, \mathbf{I}_{d}\right) \\
\mathbf{v}_{\mathbf{i}} & \sim \mathrm{M V N}_{d}\left(\mathbf{0}, \mathbf{I}_{d}\right) .
\end{alignedat} 
$$
- $\mathbf 0$: $d$ 크기의 0 vector
- $\mathbf I_d$: $d \times d$ 크기의 identity matrix

여기서 $\tau_\beta^2$ 은 constant value 로 고정한다.

이제 LSIRM 의 posterior 분포를 살펴보자. 이는 이하와 같다.




$$
\begin{alignedat}{2}
\pi\left(\boldsymbol{\Theta}, \sigma^{2} \mid \mathbf{X}\right)  \propto &\prod_{j} \prod_{i} \mathbb{P}\left(x_{j i} \mid \boldsymbol{\Theta}\right) \\
* 
&\prod_{j} \pi\left(\theta_{j} \mid \sigma_{\theta}^{2}\right) \pi\left(\sigma_{\theta}^{2}\right) 
&&\prod_{i} \pi\left(\beta_{i}\right) \\
* 
&\prod_{j} \pi\left(\mathbf{u}_{\mathbf{j}}\right) 
&&\prod_{\mathbf{i}} \pi\left(\mathbf{v}_{\mathbf{i}}\right) \pi\left(\sigma^{2}\right)
\end{alignedat}
$$


여기서 우리는 Markov Chain Monte Carlo (이하 MCMC) 를 사용하여 LSIRM 의 패러미터를 추정해 나간다. 이 방법으로 우리는 interaction map 에서 $u_j$ 와 $v_i$ 의 latent position 을 획득하는 것이 가능해진다. 우리는 topic network 를 획득하는 것에 관심이 있으므로, 우리는 $u_j$ 를 활용하여 이를 $A_i$ 의 매트릭스로 만들 것이다. **이거 $v_i$ 아니냐???**





### Procrustes Matching and Oblique Roation




다양한 matrix $X_i$ 각각에 대해 LSIRM 을 진행한 것을 통해 우리는 각 주제군들이 보유한 coordinate 로 구성된 matrix $A_i$ 들을 보유하고 있다. 

주제군들 간의 관계의 해석을 더욱 진전시키기 위해 우리는 word set 의 함수의 결과값으로서의 latent position 이 어떻게 변화하는지를 체크하고자 한다. 특히, 우리는 각 matrix $X_i$ 로부터 생산한 각 주제군의 latent position $A_i$ 간을 이하의 과정을 거쳐 비교하고자 함. 

이는 이하의 과정을 거쳐 진행.

1. LSIRM 에서 생산한 MCMC 샘플들 각각에 대해 procrustes matching 진행. 이는 invariance property 를 제어하기 위함. (소위 within-matrix matching)
2. 1에서 procrustes matching 을 통해 조정된 각각의 MCMC matrix 샘플들을 평균내는 것으로 최종적으로 사용할 estimated matrix 획득. 이렇게 획득한 esimated matrix 들에 대해 topic 들을 동일한 quadrant 에 위치시키기 위해 다시 한 번 procrustes matching.
3 각 주제들의 latent postion 으로부터 원점까지의 거리를 구한다. 이는 곧 dependency structure 의 강도를 구하기 위함. 특히, latent position 의 거리가 길다면 이것은 곧 네트워크의 더 강한 dependency 를 의미함. 

$X_i$ 를 동일한 quadrant 에 위치시키기 위해 우리는 baseline matrix 를 구해야 한다. 이는 dependency structure amnong topic 을 최대화 시키는 녀석이어야 함. 

이는 곧 topic 의 latent position 의 변화를 보여줌에 있어서 도움을 크게 줌. 왜냐? 각 matrix $X_i$ 로부터의 rotated positions $A_i$ 는 원점으로부터 가장 뻗어있는 (stretched, 멀리 떨어져 있는) 네트워크를 기준으로 하였기 때문. 이 가장 뻗어있는 ㅔㄴ트워크에 대한 notation 은 $A_{max}$. 

4. 마지막으로, 우리는 축을 회전시켜 topic 들 간의 관계의 해석성을 높이고자 함. 이 회전에는 ```oblique factor roation``` 을 사용. 이 과정들을 적용한 후 우리는 각 topic 의 coordinate 의 변화를 추적하여 topic 들 간의 관계를 추정하고자 함.

















# Latent Space Item Response Model 구현

## 3.1. python 네이티브로 모델 설계

해당 알고리즘의 구현은 1차적으로 python 으로 진행되었다. 해당 패키지를 제작하는 1차적인 목표는 다름이 아닌 통계적 백그라운드가 부족한 유저도 해당 알고리즘을 활용하기 용이한 형태로 배포하는 것에 있다. 이러한 목적을 감안할 때 해당 알고리즘을 구현하기 위한 언어를 선정함에 있어 점유율이 높은 언어를 우선하는 것은 지극히 타당하다. 다양한 설문조사 및 통계를 기반으로 살펴보았을 때, 웹 환경과 모바일 환경을 제외하였을 때 파이썬의 점유율은 다양한 분야에 걸쳐 상위권을 놓치지 않고 있으며 1등을 차지하는 경우도 드물지 않다.[^주석] 따라서 타 언어에서의 구현보다 파이썬에서의 구현을 우선하는 것은 충분한 타당성을 지닌다.

이렇게 파이썬에서 구현하고자 할 경우 몇가지 고려되어야 할 부분들이 존재한다. 우선 해당 알고리즘은 BTM 알고리즘 적용 과정에서 각 주제 하에서의, 각 단어의 출현 확률을 따지며, 또한 latent coordinate 를 각 주제마다 2개 추정하므로 결국 2차원 행렬을 다루는 것이 필수불가결하다. 그러나 여기서 python 은 R 과 달리 자체적으로는 2차원 행렬 연산를 지원하지 않으므로 2차원 행렬을 구현하기 위해 외부 라이브러리를 도입해야 한다. 이러한 선형연산 자체만 본다면 가장 강력하면서도 널리 사용되는 라이브러리는 `numpy` 이나, 해당 라이브러니는 자료형이 숫자일 때의 행렬을 담아두는 것에 특화되어 있다. 그러나 해당 알고리즘의 경우 자연어처리값을 담아두는 과정에서 숫자 이외의 자료값을 행렬에 담아두어야 하는 상황이 존재한다. 따라서 해당 상황을 고려하여 `numpy` 와 `pandas` 양쪽 라이브러리 모두를 사용한다.

또한 알고리즘 상에서 자연어처리 








### 3.1.1. python 네이티브에서의 속도 퍼포먼스

속도 퍼포먼스 예시로서 이하의 샘플을 사용한다.

| 문서갯수 | corpus | 주제갯수 |
| :-: | :-: | :-: | 
| 15281 | 3079 | 10 |

이를 통해 현재의 속도 퍼포먼스를 측정하고자 한다. corpus 갯수에 따른 속도를 측정하기 위하여, 총 corpus 의 1퍼센트부터 100퍼센트까지 1퍼센트p 간격으로, 즉 corpus 30개부터 3079개 전부를 사용하는 각 상황에서의 소요 시간을 측정한다. 이를 그래프로 나타내면 이하와 같다.

![plot_for_each_corpus_usages]()

주제의 갯수를 가리키는 패러미터를 $K$로 지정하자. 이때 50퍼센트, 즉 corpus 1500개 가량에서 iteration 1회에 약 10회가 소모된다. 이는 곧 단순 산술계산하였을 때 해당 알고리즘을 제안한 논문에서 사용한 iteration 횟수인 55000을 적용하였을 경우 총 소모시간은 $10 * 55000$초, 즉 약 6일이 소모된다는 것을 말한다.

단순 iteration 에서 시간이 이만큼이나 걸린다는 것은 정상적으로 사용 가능한 종류의 패키지라고 보기 어렵다. 따라서 해당 패키지를 배포하기 위해서는 속도 퍼포먼스 관련하여 최적화할 필요가 요구된다.





## 3.2. python에 c++ 접합한 모델 설계

시간 최적화에 고려해볼 수 있는 요소는 다양하다. 대표적으로는 이하와 같은 요소들을 고려해볼 수 있다.

- 알고리즘 최적화
- 자료구조 최적화
- 반복문 최소화


/*또한 n번 반복하는 iteration이 $a$개라고 쳤을 때, 이의 반복을 `for` 문에만 의존하였을 때 이의 시간복잡도는 $O(n^a)$*/

그러나 현재 해당 패키지는 내부연산 중에 많은 부분을 외부 라이브러리에 의존하고 있어 이러한 부분에서 건드릴 수 있는 포인트는 다소 한정적이다. 따라서 기존의 패키지 구성을 크게 터치하지 않는 방향에서 이를 해결할 방법을 모색하자. 

이때 가장 간단하면서도 직접적인 방법은 파이썬이 아닌 속도가 빠른 단어로 해당 알고리즘을 구현하는 것이다. 파이썬은 인터프리터 언어로 작성 및 활용도 측면에서는 타 언어들에 비해 부동의 강점을 지니지만, 언어의 태생적인 속도의 경우 컴파일 언어에 비해 다소 희생한 부분이 존재한다. 이에 대해서는 이하를 참조.

![comparison between other programming languages by graph]()

실제로 통계상 c++과 파이썬 사이의 속도차이는 극단적인 상황에서는 약 10배 가량 나고 있다. 따라서 c++ 로 해당 알고리즘을 작성한다면 현재 직면하고 있는 문제의 대다수는 해결할 수 있을 것.

그러나 이러한 목적 하에 해당 알고리즘을 컴파일 언어만으로 패키지를 작성한다면 앞서 언급하였던 "사용률이 높은 단어로 패키지를 작성하고자 하는 목적"에 부합하지 않게 될 것이다. 따라서 이러한 방향성을 가감없이 수용하는 것은 불가능하다.

그러나 해당 방안을 가감하여 수용한다면 해당 방안은 직면하고 있는 문제에 대한 강력한 해결책이 될 수 있으며, 실제로 이를 양립할 수 있는 방법이 있다. 

파이썬의 내부 구조를 살펴보면, 파이썬 자체는 파이썬 자체적인 문법을 따르는 인터프리터 언어이되 실제로 스스로를 실행하는 타이밍에는 스스로를 c++로 컴파일해서 실행하는 구조로 구성되어 있다. 따라서 적절한 전처리가 이루어진 컴파일된 c++ 코드는 파이썬의 인터프리터 단을 거치지 않고 바로 컴파일 단에 포함시켜서 실행시키는 것으로, 파이썬에 포함하여 파이썬 실행시에 해당 알고리즘을 c++의 성능으로 활용하는 것이 가능하다.

/*주로 시간을 잡아먹는 부분은 역시 iteration 파트와 gibbs sampling (각 부위별 소모시간 표로) / dynamic programming을 응용하여*/

이때, c++ 에서 다루는 자료형과 python 에서 다루는 자료형은 직접적으로 호환되지 않는다. 따라서 c++ 에서 출력한 값을 python 에서 받아서 활용하기 위해선, c++ 에서 생산한 값을 받아 파이썬이 인식할 수 있는 값으로 바꿔주는, 앞에서 언급한 소위 '적절한 전처리' 에 해당하는 일명 *'래핑함수'* 의 존재가 필수불가결하다. 

래핑함수를 위한 선택지는 크게 이하의 3가지가 존재한다:

1. `Cython` 라이브러리
2. `pybind11` 라이브러리
3. 필요에 맞게 래핑 함수를 직접 작성

인풋 아웃풋 효율 문제와 신뢰성 문제로 코드를 직접 짜기보다는 외부 라이브러리 사용. 여기선 범용적으로 사용되는 래핑용 라이브러리인 `pybind11`을 사용하겠다.


### Wrapping Timing

위에서 확인하였듯 c++ 에서의 처리속도는 python보다 빠름. 그러나 c++에서 생산한 값을 python 단에서 받을 때, 속도가 급격하게 느려지는 현상 발생함. 

이러한 문제점들을 고려할 때 iteration 부분 작업을 최대한 c++ 파트에 몰아넣은 후 모든 iteration을 처리하였을 때 값을 수령해야함. 

그러나 이렇게 몰아넣는다고 한다면 파이썬 파트에서 현재 `numpy` 형식으로 데이터를 처리하고 있으므로 c++ 쪽에서도 `numpy` 형태에 맞추어 값을 전달해야 하나 c++ 쪽에서 직접적으로 `numpy` 자료형을 지원하는 것은 불가능. 

이를 해결하기 위해 c++ 쪽에서 획득한 결과값을 모두 container에 포함시킨 후 파이썬 쪽에서 수령한 후 해당 컨테이너에서 값을 꺼내어 numpy 자료형에 맞도록 재배치. 다소 시간의 손실은 있을지언정 각 iteration마다 값을 수령하는 것보다는 훨씬 빠름.



### Library needed in `c++`

위에서 iteration 파트를 c++에서 모두 돌리기로 결정하였다. 여기서 iteration 은 크게 2개, BTM 부분과 lsirm 파트. 이 둘은 모두 2차원 행렬에 대해 적용되므로 c++ 에서 활용할 수 있는 선형연산 수단이 필요함. c++ 자체로 선형연산을 지원하고 있지는 않으므로 c++ 라이브러리를 적용해야 함. 

c++에서 사용할 수 있는 메이저한 선형연산 라이브러리에는 크게 `armadillo` 와 `eigen` 의 2가지가 존재. 둘사이의 차별점을 정리하면 아래와 같다. 

| Package | `armadillo` | `eigen` |
| :-: | :-: | :-: |
| Matrix Multiplication | available | available |
| More than 2d Matrix | cube (3d) | - |
| generating function for probability | None | $Dirichlet$ |

`eigen` 또란 확률생산 기능이 `armadillo` 보다 강력하다는 점에서 충분한 차별점을 지니고 있음. 그러나 해당 패키지에서는 이터레이션 내부에서 2차원 행렬을 샘플로서 여러번 생산해 이를 묶어서 파이썬으로 보내야 함. 이인즉 이를 3차원 행렬로 인식할 수 있다는 것이며, 이는 곧 3차원 행렬을 지원하는 쪽이 데이터를 다룸에 있어서 유리하다는 것을 의미함. 따라서 3차원 행렬을 지원하는 `armadillo` 를 `eigen` 보다 우선하여 채택한다. 








### 3.2.1. 접합 모델 검증 및 성능 비교

위에서 사용했던 예시와 동일하게 속도 퍼포먼스 예시로서 이하의 샘플을 사용한다.

| 문서갯수 | corpus | 주제갯수 |
| :-: | :-: | :-: | 
| 15281 | 3079 | 10 |

위와 동일한 방법으로 corpus 갯수 별 소모시간을 그래프로 표기하면 다음과 같다.

![plot_for_each_corpus_usages]()

보면 알 수 있듯이 python 에서 이터레이션을 진행했을 때에 반해 평균 약 3배의 속도 향상을 보임. 실사용 가능한 수준으로 유의미하게 개선되었다고 볼 수 있다.









# Implementation


이 section은 앞에서 제시한 알고리즘을 string input 에 실적용할 수 있는  `topic_cluster_visualizer` 패키지의 function에 대해 논한다. 해당 package 는 https://pypi.org/project/topic-cluster-visualizer/ 에서 설치할 수 있으며, python 환경에서는 이하의 command 를 실행하는 것으로 설치할 수 있다.

The latest version of `topic_cluster_visualizer` can be installed directly from PyPI repository of `Python` pacakges using:

```
pip install topic-cluster-visualizer
``` 


The package requires:

- `Python` programming language
- `numpy`, a package for efficient manipulation manipulation of multidimensional arrays,
- `pandas`, a package for efficient manipulation manipulation of non-numeric 2-dimensional arrays,
- `plotly`, a plotting package,
- `factor_analyzer`, a package for 
- `nltk`, a package for Natural Language Processing (NLP)
- `gensim`, a package for Natural Language Processing (NLP)
- `pybind11`, a `python` library for wrapping `c++` function module for multiple iteration part

And also system must support `c++`, which means c++ tools have to be installed.



`topic_cluster_visualizer` 는 크게 4가지로 나뉜다. 

- `preprocess()`: `word2vec` 을 통해 corpus 획득
- `btmize()`: corpus list 를 넣으면 Biterm Model 을 통해 각 corpus 들에 확률을 부여
- `lsirmize()`: 부여된 확률 기반으로 Gibbs Sampling 을 돌려서 각 corpus 들의 latent topic 을 추정하고 추정한 topic 들의 latent coefficient 추정
- `fit()`: 획득한 latent space coefficient 들에 procrustes matching 2번과 oblique rotation 을 적용하여 동일 quadrant 에 coefficient 들을 배치시켜 해당 주제들간의 interaction 시각화


The functions feature a consistent syntax. The following are the arguments of the fisher()
function as an illustration.



```
python> args(fisher)
function (p, adjust = "none", R, m, size = 10000, threshold,
side = 2, batchsize, nearpd = TRUE, ...)
NULL
```


We will explain the purpose of the various arguments in the following sections.

```
class TopicClusterVisualizer:
    def __init__(self, target_data):
```

need to be initialized with `target_data`, which is wanted to be analyzed.





## `preprocess()`

```
preprocess(self, train_data = None, keywords = None, train = False):
```

상기하였듯이 해당 함수에서는 자연어처리하여 corpus 를 획득. 이는 이하와 같은 절차로 이루어진다. 이의 기본적인 corpus 처리는 `nltk` 패키지를 통해 이루어지며, 해당 word2vec 기반 자연어처리를 활성화시켰을 경우 이는 `gensim` 패키지의 `word2vec()` 함수를 이용한다.

절차는 다음과 같다.

1. python 내부에서 자연어처리. 입력값으로 받은 다수의 documents 들을 1차적으로 자연어처리하여 corpus 로 분해. word_tokenize
이때 tagging 해서 건지는 언어는 명사와 형용사로 한정한다 - 명사는 주제어, 형용사는 주제어를 수식할 수 있으나 동사는 상대적으로 주제를 드러냄에 있어서 그 역할이 약함 

<br>

2. 모드 따라서 변경. <br>`train` 사용을 끌 경우 단순 NLP 후 corpus 생산에서만 끝냄. 이는 corpus 빈도에 따른 필터링 없이 생산된 모든 corpus 들을 다 사용하므로 퀄리티 크게 낮아짐. 입력된 train용 값들과 keyword용 값들을 총합하여 model 생성. using internally-used-only function `_train_corpus`.<br><br>`train` 사용을 켤 경우 word2Vec 을 적용. 적용의 구체적인 프로세스는 이하와 같다.
	1. 우선 `train_data` 통하여 word2Vec 을 통하여 모델 생산. 
	- min_freq 라는 변수 임의로 지정. keyword 와 corpus 출현 단어들 중 최소한도 이상으로 출현하는 단어들 추려내기 위한 바로미터. 
	2. 키워드에서 상위출현 단어 골라내고, 키워드에서 골라낸 상위출현 단어 중에서, (일례로 a) a가 model 에서 판정한 단어에 포함되어 있다면, a와 유사도가 높은 단어들을 포함시킨다. 패러미터 `near_term_topn_val` 사용. 디폴트값은 10. 
	term 이 인풋되었을 때, 그것이 우리가 제작한 모델에 속해있는 term이라면, - model.wv.key_to_index.keys() 라는 값을 사용한다. 해당 term 과 유사도가 높은 단어를 뽑아둔다 - model.wv.most_similar(term, topn=near_term_topn)]
	3. corpus에서 상위출현 단어 골라내고. 앞에서 모델과 keyword 간의 교집합 단어들과의 높은 유사도 단어랑, corpus 단어와의 교집합만 뽑아서 저장한다.

※ run with `train` parameter as 1 is STRONGLY RECOMMENDED. performance of the algorithm is drastically weakened without `word2vec` sequence.











## `btmize()`

위에서 획득한 corpus 들을 BTM 알고리즘을 통하여 샘플 갯수를 늘린 후 각 주제 하에서의 등장 확률을 추정. BTM 을 거치는 이유는 최대한 샘플 갯수를 늘려 추정의 정확성을 높이기 위함. 각 document 로부터 추려낸 단어들 각각에 대해 BTM 적용해서, 얘들을 각각 쌍으로 묶어서 sample 의 절대개수를 늘림. 이렇게 절대개수를 늘린 샘플들에서 바탕에 두고 있는 샘플의 개수를 empirical 하게 세팅하고, MCMC 방법론을 통해 이터레이션을 다횟수 돌리는 것으로 매 이터레이션에서 각 단어의 출현 확률을 보정해나감. 

이 이터레이션의 속도를 높이기 위해 pybind11 으로 래핑한 `btm_cpp` 함수 도입. 해당 함수의 argument 는 이하와 같다.



## `lsirmize()`

```
lsirmize(
	percentage_range = [50],
	
	data,

	ndim = 2, 
	niter = 55000, 
	nburn = 5000, 
	nthin = 5, 
	nprint = 5000,
            
	jump_beta = 0.28,
	jump_theta = 1.0,
	jump_gamma = 0.01,
	jump_z = 0.06,
	jump_w = 0.06,
	
	pr_mean_beta = 0,
	pr_sd_beta = 1,
	pr_a_th_sigma = 0.001,
	pr_b_th_sigma = 0.001,
	pr_mean_theta = 0,
	pr_a_sigma = 0.001,
	pr_b_sigma = 0.001,
	pr_mean_gamma = 0.0,
	pr_sd_gamma = 1.0,
	
	missing = 99
)
```

해당 함수에서는 위의 BTM 과정을 거쳐 각 주제가 조건으로 주어졌을 때, 각 단어에 부여된 확률 기반으로 Gibbs Sampling 을 돌려서 각 corpus 들의 latent topic 을 추정하고 추정한 topic 들의 latent coefficient 추정한다. 이때 부여해둔 값은 원본 논문에서 이터레이션용 하이퍼패러미터로 사용했던 값들에 해당한다. 변경이 필요하다면 입력한 후 사용.

상술하였듯이 해당 알고리즘을 돌림에 있어서 다양한 corpus 확률 범위에 걸쳐 알고리즘을 돌려본 후, corpus 범위별로 판정된 주제의 coordinate 를 2차원 그래프에 매핑한다. 따라서 확률 범위를 정해주는 것이 필요하다. 해당 확률 범위는 % 단위로 디폴트값은 50 하나로 설정되어 있다. 만약 여러가지 구간에 걸쳐 corpus 비율을 설정하고 싶다면 상응하는 확률구간의 % 값을 list 혹은 tuple 자료형으로 입력하면 된다. 가령 50퍼센트부터 55퍼센트 구간까지 1퍼센트p 차이로 coordinate 변화를 체크하고 싶다면 `[50,51,52,53,54,55]`를 패러미터로 주면 된다.

이때 언급하였듯이 해당 파트에서의 깁스 샘플링에서의 이터레이션의 속도를 높이기 위해 `pybind11` 으로 래핑한 `c++` 함수를 도입해주어야 한다. 해당 패키지에서는 이를 위하여 using internally-used-only function `onepl_lsrm_cont_missing` 함수를 도입하였다. 해당 함수의 parameter 는 이하와 같다.


```
std::vector<py::array_t<double>> onepl_lsrm_cont_missing
(
    arma::Mat<double> data,

    const int ndim,
    const int niter,
    const int nburn,
    const int nthin,
    const int nprint,

    const double jump_beta,
    const double jump_theta,
    const double jump_gamma,
    const double jump_z,
    const double jump_w,

    const double pr_mean_beta,
    const double pr_sd_beta,
    const double pr_a_th_sigma,
    const double pr_b_th_sigma,
    const double pr_mean_theta,
    const double pr_a_sigma,
    const double pr_b_sigma,
    const double pr_mean_gamma,
    const double pr_sd_gamma,

    const double missing
)
```

`c++` 로 작성했기에 데이터형이 `c++` 기반으로 쓰여있긴 하나 이 자체는 `python` 함수로서 작동한다. 해당 함수는 각 확률구간마다 lsirm 파트를 실행한 후, lsirm 을 통해 각 이터레이션 별로 획득된 패러미터의 값들을 총합하여 해당 확률구간에서의 패러미터를 추정한다. 이를 통해 결과값은 `dict` 포맷으로 반환되며, 해당 `dict` 에는 `z`, `map`, `phiwz`, `words` 의 4가지 key 가 존재한다. 각각의 담고있는 내용은 이하와 같다.


- `z`: 각 이터레이션에서 추정된 각 주제별 2차원 latent coordiante. #ofiteration × #oftopics × 2 크기의 행렬.
- `map`: 각 이터레이션 별로 얻어진 원점과의 총 거리.
- `phiwz`: topic $z$ 가 주어졌을 경우의 corpus $w$ 의 출현확률
- `words`: 해당 corpus 에서 어떤 corpus 들이 사용되었는가










# 구현 모델 실적용 예시
## 4.1 데이터 서술

상술하였듯이 해당 알고리즘의 결과값을 도드라지게 만들기 위해서는 문단이 짧으면서도, 해당 문단의 의미하는 바가 명확한 글줄들을 입력값으로 넣었을 때 결과값이 도드라진다. 따라서 만족스러운 결과를 위해 해당 조건에 맞는 데이터를 사용하자. 

앞서 언급하였듯이 해당 논문의 목적은 특정 연구분야를 빠르게 개괄하고 이를 유저에게 제공하는 것에 있다. 따라서 이의 실사용례를 제공하기 위해선 특정 연구분야를 정해야 할 필요가 있다. 가령 아래와 같은 주제는 어떨까. 2016년 알파고의 등장 이래 분야를 가리지 않고 딥러닝을 위시한 컴퓨터 과학에 대한 관심이 증가하였다. 특히 경영학에서는 MIS 라는 이름으로 타 분야에 비해 학문 자체에서 컴퓨터를 다루는 비중를 다루는 비중이 다소 높았던 편이다. 이러한 측면을 감안할 때 알파고의 도래 이후 모든 학문영역에 미쳤던 충격은 경영학에게 있어서는 크면 컸지 작다고 보기 어려울 것이며, 이는 곧 알파고 등장 이후 학계 논문의 주제 트렌드에 있어서 변화가 있지 않았을까 하는 의심을 품는 것에 대한 합리성을 부여해준다. 이러한 생각을 가정하였을 때 우리는 MIS 에서 딥러닝 등장에 따른 학계 논문의 주제 변화를 살펴보는 것으로 학계의 딥러닝에 대한 반응을 확인할 수 있다. 

우리는 해당 알고리즘에서 상위 몇퍼센트의 corpus 를 주제 추정에 사용할 것인가에 대한 확률구간을 임의로 설정하고 각 확률구간에서의 latent coordinate 를 살펴볼 수 있다. 이때 해당 주제에 속한 논문들의 논지가 해당 주제에 확고하게 묶여있다면 이런 확률구간의 변화에 따른 coordinate 의 변화는 크지 않을 것이며 이에 따라 latent coordinate 들은 각각 어떤 형태의 cluster 를 이루게 될 것이다. 반면 해당 주제의 coordinate 들이 cluster 를 이루지 못하고 확률구간의 변화에 따라 2차원 상에서 계속 움직이는 꼴이 된다면 이는 곧 해당 주제 속한 문헌들의 주제가 해당 주제에 확고하게 묶여있지 못하다는 것으로, 해당 문헌들의 주제가 명확하게 드러나는 것이 아닌 다소 두루뭉술하다는 것을 나타낸다고 인식될 수 있다. 이는 바꾸어 말하면 해당 주제가 부차적인 영역에 그쳤다는 것일 것이므로 학계 내에서의 해당 주제의 입지가 그리 높지 않다는 것으로 해석될 수 있을 것이다. 따라서 곧 논문 주제의 cluster 정도를 살피는 것은 우리가 목표로 하는 경영학에서의 MIS 분야가 딥러닝 도래에 어떤 반응을 보였는지에 대한 인식을 확인할 수 있는 수단이 된다.

이를 분석하기 위해 알파고의 등장인 16년을 기준으로 하여 17년부터 21년까지의 경영학 학계에서의 MIS 관련 논문들의 5년치 데이터를 모아 위의 알고리즘을 통하여 분석을 진행하자. 해당 조건에 맞는 데이터로는 논문 아카이브 사이트인 Web of Science 에서 Management, Business 분야의 논문들 중 MIS 를 다루는 논문들로부터의 abstract 를 확보하여 진행하였다. 이렇게 획득한 데이터와 empirical 하게 지정한 주제의 개수를 서술하면 이하와 같다.

| 문서갯수 | corpus | 주제갯수 |
| :-: | :-: | :-: | 
| 15281 | 3079 | 10 |


## 4.2 알고리즘 결과

이렇게 획득한 데이터에 위의 패키지를 적용하여 시각화한 결과를 획득하였다. 이때 타 확률구간에 대한 procrustes matching 에 있어 기준선으로 작동한, 가장 거리가 멀었던 확률구간 기준으로 표기한 coordinate 는 이하와 같다. 

![plot_for_max_matrix_coordinate]()




- **TOPIC NEED TO BE NAMED**

상술하였듯이 일련의 과정을 통해 얻어지는 주제는 단순히 다를 뿐 이 각각 다른 주제가 무엇에 대한 것인지에 대해서는 오롯이 연구자의 몫으로 남아있습니다. 이 이름을 어떻게 지정할 것인가에 대해서는 분석을 진행하는 연구자의 주관에 따라 결정되어야 할 것입니다. 이를 위해 해당 패키지에서는 설정한 확률 구간에 따라 사용된 corpus들이 무엇인지를 반환하는 attribute 로 `lsirmize()` 함수에 의해 배정되는 `words` attribute 가 배정되어 있습니다. 해당 attribute 를 사용해서 주관적으로 이름을 지정해주십시오. 본 논문에서 주제를 명명함에 있어서는 이하와 같은 룰로 이름을 지정하겠습니다.

1. 타 논문에서 출현하지 않은 corpus를 최우선으로 참고하여 이름 지정
2. 위에서 이름을 지정한 주제군을 제외하고 나머지 주제군으로 corpus 사용 여부를 참고하여 이때 출현하지 않은 corpus 를 기준으로 이름 지정
3. 최종적으로 이름이 지정되지 않은 주제군들이 있을 경우, 타 주제들을 통하여 각 coefficient 들의 대소가 갖는 의미를 추측한 후 이를 참고하여 주제들의 coefficient 들과 겹치는 corpus 들을 통해 주제의 이름 추정

이를 위하여 각 documents 들에서 유일하게 등장한 corpus 들과, 그렇지 않은 corpus들 중 고확률로 등장하였던 corpus 들을 나타내면 다음과 같습니다.

| | Unique Corpus | High-probability Corpus |
|:-:|:---:|:---:|
| 1 | 'load-depend', 'lithium-ion’, 'n-vehicl', 'europcar', …  | ‘econometr’, ‘guidelin’, ‘socio-techn’, ‘reproduct’, …
| 2 | 'human-machine-environ', 'datasheet' | ‘guideline, ‘budget-constraint’, ‘fintech’, ‘classification-base’, … |
| 3 | ‘eql’ (equity loan) | ‘naval’, ‘sea-land’, ‘risk-rel’, ‘blockchain’, ‘obsolesce’, … |
| 4 | - | ‘state-of-the-art’, ‘ubiquitous’, ‘seaport’, ‘warehous’, ‘techniq’, … |
| 5 | 'incentive-bas', ‘s-crm', 'nation-dyad', 'ai-aug', 'accultur’, … | ‘discret’, ‘transact’, ‘state’, ‘civil’, ‘telemat’, ‘transform’, … |
| 6 | - | ‘techniq’, ‘cross-sect’, ‘transmiss’, ‘worldwide’, ‘sement’, ‘agricult’, …  |
| 7 | 'margin-trad', 'future-focus', 'protection-motiv' | ‘mathematic’, ‘econometr’, assess’, ‘itil’, … |
| 8 | 'reuse-bas', 'geo-ecolog', 'molybdenum-contain’, … | ‘textile’, ‘robust’, ‘retrain’, ‘quantity-pay’, ‘geograph’, … |
| 9 | 'assemble-to-ord', 'evm', 'chat-bot', 'feature-process-machin’, … | ‘transboundary’, ‘quantity-pay’, ‘translat’, ‘multi-type’, … |
| 10 | 'hardware-softwar', 'regime-switch', 'competition-bas', … | ‘benchmark’, ‘simulat’, ‘ontology-bas’, ‘human-computer’, … |

이에 기반하여 위에서 서술하였던 룰에 따라 주제를 명명하면 다음과 같습니다.

|  | Name of Topics |
|:-:|:-----:|
| 1 | 전기차 |
| 2 | Excel 등 DB 관리 |
| 3 | 회계 분야에서의 신기술 사용 관련 |
| 4 | 최신기술, DB 관리 |
| 5 | 이문화 조직구성원 간 소통 |
| 6 | 글로벌, 분야간 통섭 |
| 7 | 금융시장 분야 |
| 8 | 지속 가능한 환경경영 |
| 9 | 비트코인 위시한 블록체인 및 딥러닝 관련 |
| 10 | 경영 최전선에서의 디지털 기술 활용 |




이제 주제를 명명한 바 이상으로 해당 데이터들에 대한 인사이트를 획득하기 위해 각 확률구간에 따른 coordinate 의 변화를 확인하겠습니다. 이는 다음과 같습니다. 

![plot_for_each_matrix_coordinate](C:\Users\Song1\Documents\GitHub\202201_phd_paper\newplot (9).png)

여기서 타 사분면들 대비 1, 4분면 근방의 점이 많다는 점을 통해 근 5년간 딥러닝을 위주로 한 컴퓨터 과학 기술이 발전하였음에도 여전히 mis 논문들은 고전적인 경영학 이론을 다루는 경우가 많다는 것을, 그리고 네이처나 서스테이너블한 요소보다는 지오그래피컬한 실제적이고 구체적인 주제에 집중하고 있다는 사실을 파악할 수 있습니다.

이때 여기에, 결과의 시인성을 높이기 위해 확률구간의 변화에 따른 coordinate 이동을 화살표로 명시해주는 것으로 주목해볼 만한 유의미한 인사이트를 얻을 수 있습니다.






![trajectory_for_each_matrix_coordinate](C:\Users\Song1\Documents\GitHub\202201_phd_paper\Rplot03.bmp)


아까 말씀드렸듯이 동일 컬러링 상에서의 서로 다른 점들은 해당 topic 에서 확률구간에 따라 서로 다르게 나타난 coordinate 로, topic에서의 각 확률구간마다 corpus 등장 확률에 기반하여 추정에 사용된 corpus 데이터가 다릅니다. 확률 구간을 좁게 잡으면 가령 상위 40%의 확률로 등장하는 corpus들만이 주제 추정에 사용되지만 확률 구간을 넓혀감에 따라 최종적으로 상위 60%까지의 corpus들이 주제 추정에 사용되게 됩니다. 이는 곧 토픽 추정에 사용되는 corpus의 총량이 변화한다는 의미이며 이에 따라 추정된 주제의 형태가 변하는 경우가 발생하는 것은 당연하다고 말씀드렸습니다.

그러나 trajectory 를 보시면 확인하실 수 있듯이 디지털 경향이 강한 topic이 아날로그 쪽이나 organization 쪽으로 주제가 변하는 경우는 없으며 반대 또한 마찬가지입니다. 즉 확률 구간에 따른 topic의 coordiante 의 이동이 각 axis의 양 극단을 쌍으로 하여 그 사이에서만 이루어지고 있으며 이는 mis 연구에서의 방법론 현황에 대한 주목해볼 만한 단서를 던져줍니다.

즉 topic 들 중 소속된 문헌이 하나의 강력한 주제에 묶여있는 것이 아니어서 corpus 사용량에 따라 추정된 topic 이 변화하는 케이스에서조차도, nature 나 서스테이너빌리티의 관점을 다룬 topic이 클래시컬한 기존 경영학에서의 관리 일원들이나 아날로그한 측면의 토픽들과는 어울리지 못하고 디지털 및 테크놀로지 관점과만 상호 작용하고 있는 것입니다. 또한 역으로 logistic 이나 geography 측면의 터팩들은 analogue와 technology 사이에서 균형을 잡은 이론이 한계일 뿐 디지털 디지털 측면에 치우친 topic은 찾기 어렵습니다.

이는 곧 필드를 불문하고 학계 전체에 충격을 주었던 딥러닝 혁명이 아직 디지털 분야에서만 한정되어 논해지고 있다고 볼 수 있으며 딥러닝 혁명이 가지는 강력한 잠재력을 볼 때 이는 학계에 있어 커다란 손실이라고 할 수 있을 것입니다. 이러한 부분을 보완하여 서스테이너빌리티 측면과 클래식한 기존 경영학 이론을 좀 더 적극적으로 융합한 논문이 늘어나는 것을 통해 학계에서 진행되는 논의 토양이 조금 더 비옥해질 수 있지 않을까 조심스레 제안해 봅니다.






# 결론 














































































































































































































































































































