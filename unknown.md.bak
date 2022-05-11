Untitled
본 논문에서는 불특정 다수의 글줄 입력값에 대한 latent space model 알고리즘을 구현하였다. 해당 알고리즘은 다수의 글줄 입력값을 받아 이를 word2vec을 통해 전처리하고, 해당 과정의 도중 데이터가 부족할 상황을 상정하여 Biterm model 의 방법론을 활용하여 총 corpus 개수를 늘리는 작업을 병행한 후 각 주제별로 각 단어의 등장 확률을 계산한다. 이후 이에 latent space response item model 의 변형 알고리즘을 적용하는 것으로 latent coordinate 를 획득한 후, 이의 시인성을 높이고자 procrustes rotation 과 oblique rotation 을 적용하여 얻어낸 각 coordinate 의 차이를 극대화한다. 이후 이를 2차원 plot 에 매핑하는 것으로 최종적으로 결과값을 시각적으로 보여준다.

위의 알고리즘을 python 기반으로 구현하였으며 속도 퍼포먼스의 향상을 위해 c++을 접합하여 대량의 계산을 필요로 하는 부분을 c++로 처리하였다. 본 논문에서는 해당 구현의 결과값이 유효하다는 것을 증명하고자 동일 주제를 갖는 Web of Science에서 논문 abstract 들을 크롤링하여 이를 대상으로 알고리즘을 적용하고, 최종적으로 획득한 시각화 결과값을 통해 최신 논문 트렌드를 서술하는 것으로 해당 알고리즘 및 패키지의 쓸모를 밝히고자 한다.







1 서 론
1.1 연구 배경
현대에 들어서는 분야별로 전문성이 심화되고 있으며 해당 분야에 대한 전문적인 지식 없이는 해당 분야를 얕게나마 이해하는 것도 벅차지고 있습니다. 그럼에도 통섭이라는 단어로 대표되는 분야 간의 협업 및 심화된 전문영역간의 상호교류의 수요는 계속해서 높아지고 있는 상황입니다. 이런 상황에서 각 분야에 대한 지식 없이는 협업의 생산성이 담보되지 않으면서도, 생산성을 갖추기 위해 해당 분야의 공부에 시간을 투자하기에는 자신의 분야에 집중하는 것만 해도 시간이 부족하다는 진퇴양난의 상황이 발생합니다.

Graph-based Trajectory Visualization for Text Mining of COVID-19 Biomedical Literature 논문은 이러한 상황을 타파하기 위해 해당 분야와 관련된 documents 들을 이용하는 것을 제안합니다. 해당 분야와 관련된 대량의 documents 들을 획득한 후 이에 해당 알고리즘을 적용하여 시각화 하는 것으로 해당 분야에 대한 documents 들의 주제들을 개략적으로 하나의 단어로 표시한 후, 이를 2차원 그래프에 배치하는 것으로 해당 주제들 간의 관계성을 드러내는 것이 가능합니다. 이를 통해 분야에 대한 지식 없이도 분야에 관한 documents 들의 흐름을 통해 피상적으로나마 해당 분야를 개괄적으로 파악하여 해당 분야에 엮인 외부인에게 요구되는 노력을 줄일 수 있다고 기대합니다. 이러한 목적을 달성하기 위해 해당 알고리즘을 독립적인 패키지로 배포하고자 하는 것이 해당 프로젝트의 목표였습니다.

1.2 연구 목적
이렇듯 해당 논문은 분야를 이해하는데 있어 유효한 도구가 될 수 있는 알고리즘을 제공하고 있습니다. 그러나 구현과정에서 각종 통계학 이론 및 분포, 그리고 딥러닝 처리방법을 사용하기 있기 때문에 통계학 지식이 부족한 연구자들이 해당 알고리즘을 사용해내는 것은 그다지 쉬운 일이 아닙니다. 이는 곧 연구자로 하여금 해당 알고리즘을 구현하여 실사용하기 위해서는 추가적인 통계적 지식 및 기초적인 프로그래밍 지식을 요한다는 것과 같은 의미이며, 이는 곧 통계적 역량이 부족한 연구자들에게 목적으로 하는 분야 이외에 통계학적인 지식 또한 요구하는 상황이 되고 맙니다. 해당 알고리즘 수요자에게 이렇듯 추가적인 부담을 지우는 것은 트렌드 분석을 용이하게 하고자 했던 당초의 목적과는 상반된다고 말할 수 있습니다. 따라서 이러한 불편함을 덜어주기 위해 해당 알고리즘을 분석한 후 일련의 과정을 코드로 작성한 후 하나의 패키지화 하여 배포하는 것은 충분한 실익이 있다고 말할 수 있습니다.

이러한 목적 아래서 본 논문의 내용은 다음과 같습니다. 우선 해당 알고리즘의 바탕으로 하고 있는 이론들과 기초적인 흐름을 서술합니다. 그 후 다양한 프로그래밍 언어들 중 해당 언어를 채택한 이유와, 해당 언어를 통해 구현하는 과정에서 고려되었던 사항들과 실구현 과정을 서술하겠습니다. 이때 실구현 과정에서 마주친 문제점들과 해당 문제점들에 대한 해결책을 제시합니다. 마지막으로 해결책을 적용한 구현 방법론을 통해 해당 알고리즘을 구현한 패키지의 사용법을 서술하고, 실제 데이터를 사용하여 해당 패키지의 퍼포먼스를 보일 것입니다.







2 Method
해당 알고리즘이 목표로 하는 바는 명확하며, 해당 과정에서는 통계적 절차를 걸쳐 입력된 문단의 주제를 확인하는 것이 요구됩니다. 이때 문단의 길이가 길면 길수록 하나의 글줄에서 주제를 파악하기 위해 사용되는 corpus 의 숫자는 늘어나며, 그 숫자가 늘어남에 따라 글줄의 주제를 한두단어로 갈무리하고자 하는 시도는 더욱 어려워질수밖에 없습니다. 따라서 이러한 목적에 맞는 성질이 도드라지는 결과값을 얻기 위해서는 문단의 길이가 짧으면서도 문단 자체가 강력한 힘을 가지는 부류의 글줄을 사용하는 것이 최선입니다. 이런 성질을 가지는 글줄의 종류로는 기사의 서문, 정부발표 요약문, 그리고 논문의 abstract 등을 생각해볼 수 있을 것입니다.

2.1 Natural Language Processing
입력된 문단을 그대로 사용하는 것으로 불가능하므로 적절한 전처리 과정을 거칠 필요가 있습니다. latent space response item model 을 적용하기 위해서는 각 주제에서의 각 확률의 등장 확률을 계산해낼 필요가 있습니다. 이 자체는 단순한 MCMC 알고리즘으로 이터레이션을 여러차례 돌려 각 단어의 등장 확률을 추정하는 것만으로 성립할 수 있습니다만, 한 단어에서 획득할 수 있는 corpus 의 선정 및 갯수는 사용하는 어떤 알고리즘을 사용하는가에 따라 달라집니다.

단순한 NLP 를 거쳐 단어를 tokenize 한 결과값만을 사용할 수 있을 것입니다만, 이는 단순한 알고리즘의 반복일 뿐이므로 얻어지는 corpus 들의 품질이 다소 떨어질 우려를 지울 수 없습니다. 조금 더 성능높게 corpus 들을 획득하고 싶다면 이에 더해 더욱 발전된 corpus 획득 방식을 적용해볼 수 있습니다. 이러한 목적 하에 ‘비슷한 의미를 가지는 단어들은 비슷한 문맥에서 등장한다’ 는 가정 하에서 각 단어가 보유하는 스테이터스를 부여하고 corpus 들을 인식하고 추려내는 Word-To-Vector, 속칭 word2vec 알고리즘을 활용하여 corpus 들을 추려내면 더욱 높은 성능으로 corpus 들을 획득해낼 수 있습니다.

2.2 Biterm
이때 1차적으로 input 하는 글줄의 양도 적을 뿐더러, 같은 분야의 글줄들을 다루기 때문에 개별 글줄마다 고유하게 가지는 단어의 갯수가 적어 특성을 통계적으로 파악하기에 충분하지 않을 정도로 개별 글줄들이 을 수 있다. 이를 보완하기 위해서 Biterm Model을 도입.1 Biterm Model 은 본질적으로 통계적 확률을 가리기 위한 재료의 가짓수가 적을 경우 이를 판단하기 위한 재료를 늘리기 위한 과정에 해당한다. 원본 문서에서 corpus의 갯수가 n 개였다면 Biterm 과정을 거치는 것으로 n2으로 확률 추정에 사용되는 샘플들의 갯수를 늘리는 것이 가능하다는 것입니다. 이렇게 샘플을 늘린 것으로 개별 단어의 확률 추정의 정밀도를 높인 채로 획득하는 것이 가능.

Biterm Model 은 다음과 같은 가정에 존재.

두 단어는 겉보기로 인식할 수 없는 단어의 클러스터에 함께 속한다
각 글줄에는 인식할 수 없는 주제가 존재하며, 각각의 주제 내부에는 유사한 의미를 보유하는 단어들이 모여있다
인식할 수 없는 단어의 클러스터가 함께 속해있는 그것을, 인식할 수 없는 주제라고 인식할 수 있다
이의 과정은 이하와 같다.

θ∼Dirichlet(α) 로부터 모든 주제들의 분포를 샘플링.
Biterm set B 의 각 biterm b 에 대해, 해당 biterm을 구성하는 2개의 단어의 합이 전체 주제들 중 어느 주제 z에 속하는지를 샘플링. 이때 z∼Mult(θ).
주제가 주어졌을 경우의 단어의 분포, 즉 주제 z의 topic-word 분포를 샘플링. 이때 ϕz∼Dirichlet(β).
topic-word 분포로부터 골라진 topic z 에 대응하는 각 두 단어들의 출현 확률을 샘플링. 이때 wi,wj∼Mult(ϕz).
이의 단계를 모두 거치는 것으로, 모든 biterm set B 의 joint likelihood 는 이하와 같이 표현될 수 있다.

p(B)=∏i,j∑zθzϕi|zϕj|z

이에 의해 latent topic z 의 조건부 posterior 는 이하와 같은 비례식을 따른다.

p(z|z−b,B,α,β)∝(nz+α)(nwi+β)(nwj|z+β)(∑wnw|z+Mβ)2

nz: biterm 가 주제 z에 할당된 횟수
n−b: biterm b 가 포함되지 않았던 주제들
nw|z: 주제 z에 할당된 단어 w 의 횟수
이때 p(z|z−b,B,α,β) 에의 깁스 샘플링의 직접적인 적용은 변수들 간의 dependency 때문에 convergence 로 이르지 못할 우려를 배제할 수 없음. 따라서 우리는 collapsed 깁스 샘플링을 사용하여 불필요한 패러미터들을 integrate out 하여 이의 영향을 억제한다. 이때 prior 을 dirichlet 으로 사용한 것의 이득을 볼 수 있다. dirichlet 을 사용한 것으로 ϕz 와 θ 가 integrate out 당하므로. 몇번의 iteration 이후 우리는 획득한 statistics (통계량) nw|z 와 θz 를 활용하여 ϕw|z 와 θz 의 distribution 을 이하와 같이 구성할 수 있게 된다.

ϕw|z=nw|z∑wnw|z+Mβ,θz=n+α|B|+Kα

M: 획득해두었던 corpus 의 총 갯수
B: 넘버링된 각 biterm
K: 설정한 총 topic 의 갯수
이처럼 우리는 corpus 에서 biterm 을 구성한 후, 각 biterm 을 이용해 추정한 것으로 주제군 하에서의 corpus 분포 ϕw|z 와 주제 자체의 출현 분포 θz 을 정밀도 높게 추정하는데에 성공했다.

2.3 Latent Space Item Response Model
해당 단계에서는 위에서 획득한 단어들의 출현빈도를 사용하여 각 주제군들 간의 관계성을 확인하고 이 관계성을 interaction map 에 표시하여 각 글줄들 간의 관계를 구성한다.

원본: Latent Space Model, 네트워크에서의 각 actor (node) 들의 unobserved space 에서의 관계를 표현
후속: Latent Space Item Response Model (LSIRM). item response 를 biparite nwtwrok 로 인식하고, respondent 와 item 간의 관계를 latent space 를 사용하여 획득하는 것
LSIRM 은 이하의 2가지로 모델링된다.

Attribute: 특정 item 에 몇 명의 응답자가 응답했는지와, 특정 응답자들에 의해 몇 개의 item 이 응답되었는가
Interaction: 각 item과 응답자의 latent position, 그리고 item 과 응답자 사이의 interaction을 측정
이를 응용하는 것으로 목표하는 바를 달성할 수 있다. 해당 알고리즘의 목적은 주제 간의 관계를 추정하는 것과, 각 주제들에 연관된 단어를 근거로 하여 interaction map에서 주제의 latent position을 추정하는 것이다. 즉 topic 간의 관계를 획득하고 이 관계를 나타내는 coefficient 들을 연관된 단어를 기반으로 하여 interaction map 에 매핑하고자 하는 일련의 과정을 특정한 수리적 과정을 거쳐 달성해야 한다.

앞서 획득한 ϕw|z 의 matrix Xi 를 biparite network 로 인식하자. 이때 topic 은 item, respondent 은 word 가 된다.

topic	item
word	respondent
단 본디 원본 LSIRM 은 binary 데이터를 서술하기 위해 작성. 따라서 해당 문제에 직접 적용은 불가하다. 해당 문제의 경우 word2vec을 거쳐 각 단어의 출현 확률에 0에서 1 사이의 실수값을 부여하였기에 binary 모델이 아닌 Gaussian 버전. 해당 문제를 보정하기 위하여 해당 문제의 기본 아이디어만을 살리고 사용하는 확률을 Gaussian 확률로 변경하는 것으로 해당 문제를 보완할 수 있다. binary 가 아닌 Gaussian 용도로 변형된 LSIRM 은 이하와 같이 서술될 수 있다.

xi,j|Θ=θj+β+∥uui−vvj∥+ϵj,i

ϵj,i∼N(0,σ2)
i=1∼P, j=1∼N
xj,i: 단어 x가 주제 i에 속할 확률 (횟수?)
Θ={θθ={θj},ββ={βj},UU={uj},VV={vj}}
∥ui−vj∥: 단어 i 와 주제 j 각각의 latent position 사이의 Euclidean Distance.
원본 LSIRM 의 경우 binary 자료를 연속형으로 변환하기 위해 logit link 함수를 사용했음. 따라서 여기서 우리는 interaction 부분, attribute 부분과 xj,i 사이의 선형성 가정을 이용. normality equation을 만족시키기 위해 error term ϵi,j 를 추가.

이때 ∥ui−vj∥ 가 짧을 경우, 이는 곧 word 의 latent position ui 와 topic 의 latent position vj 의 연관성이 존재할 가능성이 높다는 것을 의미하며, 이는 곧 word i 가 topic j 에 link 되어 있을 확률이 높음을 암시. 따라서, topic 의 latent position 은 word 들과의 거리에 기반하여 측정되는 것이 가능하다.

위에 주어진 모델을 given 했을 때, 우리는 LSIRM 의 gaussian 버전에서의 패러미터를 측정하기 위해 베이지안 추론을 활용하였다. 우리는 패러미터에 대한 prior 분포를 이하와 같이 특정한다:

βi∣τ2βθj∣σ2σ2σ2θujvi∼N(0,τ2β),∼N(0,σ2θ),∼Inv-Gamma(a,b),∼Inv-Gamma(aσ,bσ),∼MVNd(0,Id)∼MVNd(0,Id).τ2βσ2aaσ>0>0>0,b>0>0,bσ>0
- 0: d 크기의 0 vector - Id: d×d 크기의 identity matrix

여기서 τ2β 은 constant value 로 고정한다.

이제 LSIRM 의 posterior 분포를 살펴보자. 이는 이하와 같다.

π(Θ,σ2∣X)∝∗∗∏j∏iP(xji∣Θ)∏jπ(θj∣σ2θ)π(σ2θ)∏jπ(uj)∏iπ(βi)∏iπ(vi)π(σ2)

여기서 우리는 Markov Chain Monte Carlo (이하 MCMC) 를 사용하여 LSIRM 의 패러미터를 추정해 나간다. 이 방법으로 우리는 interaction map 에서 uj 와 vi 의 latent position 을 획득하는 것이 가능해진다. 우리는 topic network 를 획득하는 것에 관심이 있으므로, 우리는 uj 를 활용하여 이를 Ai 의 매트릭스로 만들 것이다. 이거 vi 아니냐???

2.4 Procrustes Matching and Oblique Roation
다양한 matrix Xi 각각에 대해 LSIRM 을 진행한 것을 통해 우리는 각 주제군들이 보유한 coordinate 로 구성된 matrix Ai 들을 보유하고 있다. 주제군들 간의 관계의 해석을 더욱 진전시키기 위해 우리는 word set 의 함수의 결과값으로서의 latent position 이 어떻게 변화하는지를 체크하고자 한다. 특히, 우리는 각 matrix Xi 로부터 생산한 각 주제군의 latent position Ai 간을 이하의 과정을 거쳐 비교하고자 함.

이는 이하의 과정을 거쳐 진행.

LSIRM 에서 생산한 MCMC 샘플들 각각에 대해 procrustes matching 진행. 이는 invariance property 를 제어하기 위함. (소위 within-matrix matching)
1에서 procrustes matching 을 통해 조정된 각각의 MCMC matrix 샘플들을 평균내는 것으로 최종적으로 사용할 estimated matrix 획득. 이렇게 획득한 esimated matrix 들에 대해 topic 들을 동일한 quadrant 에 위치시키기 위해 다시 한 번 procrustes matching.
각 주제들의 latent postion 으로부터 원점까지의 거리를 구한다. 이는 곧 dependency structure 의 강도를 구하기 위함. 특히, latent position 의 거리가 길다면 이것은 곧 네트워크의 더 강한 dependency 를 의미함. 이때 Xi 를 동일한 quadrant 에 위치시키기 위해 우리는 baseline matrix 를 구해야 한다. 이는 dependency structure amnong topic 을 최대화 시키는 녀석이어야 함. 
이는 곧 topic 의 latent position 의 변화를 보여줌에 있어서 도움을 크게 줌. 왜냐? 각 matrix Xi 로부터의 rotated positions Ai 는 원점으로부터 가장 뻗어있는 (stretched, 멀리 떨어져 있는) 네트워크를 기준으로 하였기 때문. 이 가장 뻗어있는 네트워크에 대한 notation 은 Amax.
마지막으로, 우리는 축을 회전시켜 topic 들 간의 관계의 해석성을 높이고자 함. 이 회전에는 oblique factor roation 을 사용. 이 과정들을 적용한 후 우리는 각 topic 의 coordinate 의 변화를 추적하여 topic 들 간의 관계를 추정하고자 함.
2.4.1 About procrustes rotation
우리는 두 행렬간의 정확한 차이를 찾아내기 위하여, procrustes 를 사용해 하나의 행렬을 다른 행렬에 가장 유사한 구도가 되도록 회전, 반사, transfomation 시켜 둘을 비슷하게 만든다고 말하였다. 어째서 procrustes rotation 이 행렬 간의 유사도를 극대화하는가?

Xn×p 와 Yn×p 의 두 임의의 행렬을 설정하자.

goodness of fit 에 대한 측정값은 지점 yr 들을 지점 xr 들에 가깝게 옮기는 것으로 얻어진다. 언제까지? “residual” sum of squares ∑nr=1(xr−yr)′(xr−yr) 가 최소화가 될 때까지. 우리는 회전, 반사, translation 등을 통하여 이 포인트들을 움직여낼 수 있으며, 이는 이하의 수식으로 표현될 수 있다.

A′yr+b,r=1,…,n, 

where A′ is a (p×p) orthogonal matrix.

따라서 우리의 목적은 A 와 b 에 대해 이하의 문제를 푸는 것과 동일해지며, 이때 A 와 b 는 least squares 들을 통해 얻어질 수 있음에 유의하자.

R2=minA,b∑r=1n(xr−A′yr−b)′(xr−A′yr−b)(a)

이를 b 에 대해 미분한 것으로, 우리는 b^=x¯−A′y¯ 임을 알고 있다. 이때 y¯=∑yrn and x¯=∑xrn. Since both configurations are centred, b^=0.

그렇다면 우리는 (a) 를 이하와 같이 다시 작성할 수 있다.

The constraints on A are AA′=I, i.e. a′iai=1,a′iaj=0,i≠j, where a′i is the i th row of A. Hence there are p(p+1)2 constraints.

R2=minAtr(X−YA)(X−YA)′=trXX′+trYY′−2maxAtrX′YA(x)

여기서 이야기를 진행하기 전 notation 을 몇개 지정하자.

Let Xn×p and Yn×p be two configurations of n points, for convenience centred at the origin, so x¯¯¯=y¯¯¯=0.

Let Z=Y′X and using the singular value decomposition theorem (Theorem A.6.5), write

Z=VΓU′, 

where V and U are orthogonal (p×p) matrices and Γ is a diagonal matrix of non-negative elements.

Then the minimizing values of A and b in (14.7.3) are given by

b^=0,A^=VU′,
and further
R2=trXX′+trYY′−2trΓ(y)

이제 이상을 보일 것이다.

이제 이러한 제약들에 대한 Lagrange multipliers 를 생각해보자. 이를 12Λ 로 가정하고, 이는 이(p×p) symmetric matrix. 이때 목적은 이하를 최대화하는 것이다.

tr{Z′A−12Λ(AA′−I)}(b)

where Z′=X′Y. By direct differentiation it can be shown that

∂∂Atr(Z′A)=Z,∂∂Atr(ΛAA′)=2ΛA

따라서 on differentiating (b) and equating the derivatives to zero, we find that A must satisfy

Z=ΛA(c)

우리는 위에서 Z=VΓU′ 라고 지정하였다. Z 에 이를 적용하고, Λ 가 symmetric 인 것과 A 가 orthogonal 라는 부분을 유의하자. 이와 Z=ΛA 라는 지점을 복합하는 것으로 우리는 이하를 얻을 수 있다.

Λ2=ZA′AZ=ZZ′=(VΓU′)(UΓV′)

Thus we can take Λ=VΓV′. (c) 에서 Λ 의 이 값을 대체하는 것으로 우리는 이하를 얻을 수 있다.

A^=VU′

바로 이것이 (c) 의 해답이 된다. 이때 A^ 는 orthogonal 임에 유의하자. 이 A^ 의 값을 (x) 에 넣는 것으로 최종적으로 (y) 를 얻을 수 있다.

최종적으로

A^ 가 (b) 를 극대화시킨다는 것을 증명하기 위해 (그리고 단순한 stationary point 가 아님을 보이기 위해) 다시 한 번 (b) 를 A 로 미분합니다.

이 목적을 이루기 위해선 A 를 벡터 a=(a′(1),…,a′(p))′ 로 서술하는 쪽이 편하다.

이 경우 (b) 는 a 의 quadratic function 이며, (b) 의 a 에 대한 second derivative 는 matrix −Ip⊗Λ 로서 서술될 수 있다.

Λ=VΓV′ 이며 Γ 의 diagonal elements 들은 nonnegative 이므로, 우리는 second derivative matrix 가 negative semidefinite 임을 확인할 수 있다. 따라서 A^ 는 (b) 를 극대화하며, procrustes 를 거리는 것으로 한 행렬이 다른 행렬에 가장 가깝게 가공된 값을 파악하는 것이 가능하다.







3 Latent Space Item Response Model 구현
3.1 python 네이티브로 모델 설계
해당 알고리즘의 구현은 1차적으로 python 으로 진행되었다. 해당 패키지를 제작하는 1차적인 목표는 다름이 아닌 통계적 백그라운드가 부족한 유저도 해당 알고리즘을 활용하기 용이한 형태로 배포하는 것에 있다. 이러한 목적을 감안할 때 해당 알고리즘을 구현하기 위한 언어를 선정함에 있어 점유율이 높은 언어를 우선하는 것은 지극히 타당하다. 다양한 설문조사 및 통계를 기반으로 살펴보았을 때, 웹 환경과 모바일 환경을 제외하였을 때 파이썬의 점유율은 다양한 분야에 걸쳐 상위권을 놓치지 않고 있으며 1등을 차지하는 경우도 드물지 않다.[^주석] 따라서 타 언어에서의 구현보다 파이썬에서의 구현을 우선하는 것은 충분한 타당성을 지닌다.

이렇게 파이썬에서 구현하고자 할 경우 몇가지 고려되어야 할 부분들이 존재한다. 우선 해당 알고리즘은 BTM 알고리즘 적용 과정에서 각 주제 하에서의, 각 단어의 출현 확률을 따지며, 또한 latent coordinate 를 각 주제마다 2개 추정하므로 결국 2차원 행렬을 다루는 것이 필수불가결하다. 그러나 여기서 python 은 R 과 달리 자체적으로는 2차원 행렬 연산를 지원하지 않으므로 2차원 행렬을 구현하기 위해 외부 라이브러리를 도입해야 한다. 이러한 선형연산 자체만 본다면 가장 강력하면서도 널리 사용되는 라이브러리는 numpy 이나, 해당 라이브러니는 자료형이 숫자일 때의 행렬을 담아두는 것에 특화되어 있다. 그러나 해당 알고리즘의 경우 자연어처리값을 담아두는 과정에서 숫자 이외의 자료값을 행렬에 담아두어야 하는 상황이 존재한다. 따라서 해당 상황을 고려하여 numpy 와 pandas 양쪽 라이브러리 모두를 사용한다.

또한 알고리즘 상에서 자연어처리

3.1.1 python 네이티브에서의 속도 퍼포먼스
속도 퍼포먼스 예시로서 이하의 샘플을 사용한다.

문서갯수	corpus	주제갯수
15281	3079	10
이를 통해 현재의 속도 퍼포먼스를 측정하고자 한다. corpus 갯수에 따른 속도를 측정하기 위하여, 총 corpus 의 1퍼센트부터 100퍼센트까지 1퍼센트p 간격으로, 즉 corpus 30개부터 3079개 전부를 사용하는 각 상황에서의 소요 시간을 측정한다. 이를 그래프로 나타내면 이하와 같다.


plot_for_each_corpus_usages

주제의 갯수를 가리키는 패러미터를 K로 지정하자. 이때 50퍼센트, 즉 corpus 1500개 가량에서 iteration 1회에 약 10회가 소모된다. 이는 곧 단순 산술계산하였을 때 해당 알고리즘을 제안한 논문에서 사용한 iteration 횟수인 55000을 적용하였을 경우 총 소모시간은 10∗55000초, 즉 약 6일이 소모된다는 것을 말한다.

단순 iteration 에서 시간이 이만큼이나 걸린다는 것은 정상적으로 사용 가능한 종류의 패키지라고 보기 어렵다. 따라서 해당 패키지를 배포하기 위해서는 속도 퍼포먼스 관련하여 최적화할 필요가 요구된다.

3.2 python에 c++ 접합한 모델 설계
시간 최적화에 고려해볼 수 있는 요소는 다양하다. 대표적으로는 이하와 같은 요소들을 고려해볼 수 있다.

알고리즘 최적화
자료구조 최적화
반복문 최소화
/또한 n번 반복하는 iteration이 a개라고 쳤을 때, 이의 반복을 for 문에만 의존하였을 때 이의 시간복잡도는 O(na)/

그러나 현재 해당 패키지는 내부연산 중에 많은 부분을 외부 라이브러리에 의존하고 있어 이러한 부분에서 건드릴 수 있는 포인트는 다소 한정적이다. 따라서 기존의 패키지 구성을 크게 터치하지 않는 방향에서 이를 해결할 방법을 모색하자.

이때 가장 간단하면서도 직접적인 방법은 파이썬이 아닌 속도가 빠른 단어로 해당 알고리즘을 구현하는 것이다. 파이썬은 인터프리터 언어로 작성 및 활용도 측면에서는 타 언어들에 비해 부동의 강점을 지니지만, 언어의 태생적인 속도의 경우 컴파일 언어에 비해 다소 희생한 부분이 존재한다. 이에 대해서는 이하를 참조.


comparison between other programming languages by graph

https://en.wikipedia.org/wiki/Comparison_of_programming_languages#/media/File:Barplot_language_speeds_(Benchmarks_Game_Mandelbrot).svg

실제로 통계상 c++과 파이썬 사이의 속도차이는 극단적인 상황에서는 약 10배 가량 나고 있다. 따라서 c++ 로 해당 알고리즘을 작성한다면 현재 직면하고 있는 문제의 대다수는 해결할 수 있을 것이다. 그러나 이러한 목적 하에 해당 알고리즘을 컴파일 언어만으로 패키지를 작성한다면 앞서 언급하였던 “사용률이 높은 단어로 패키지를 작성하고자 하는 목적”에 부합하지 않게 될 것이다. 따라서 이러한 방향성을 가감없이 수용하는 것은 불가능하다.

그러나 해당 방안을 가감하여 수용한다면 해당 방안은 직면하고 있는 문제에 대한 강력한 해결책이 될 수 있으며, 실제로 이를 양립할 수 있는 방법이 있다.

파이썬의 내부 구조를 살펴보면, 파이썬 자체는 파이썬 자체적인 문법을 따르는 인터프리터 언어이되 실제로 스스로를 실행하는 타이밍에는 스스로를 c++로 컴파일해서 실행하는 구조로 구성되어 있다. 따라서 적절한 전처리가 이루어진 컴파일된 c++ 코드는 파이썬의 인터프리터 단을 거치지 않고 바로 컴파일 단에 포함시켜서 실행시키는 것으로, 파이썬에 포함하여 파이썬 실행시에 해당 알고리즘을 c++의 성능으로 활용하는 것이 가능하다.

/주로 시간을 잡아먹는 부분은 역시 iteration 파트와 gibbs sampling (각 부위별 소모시간 표로) / dynamic programming을 응용하여/

이때, c++ 에서 다루는 자료형과 python 에서 다루는 자료형은 직접적으로 호환되지 않는다. 따라서 c++ 에서 출력한 값을 python 에서 받아서 활용하기 위해선, c++ 에서 생산한 값을 받아 파이썬이 인식할 수 있는 값으로 바꿔주는, 앞에서 언급한 소위 ‘적절한 전처리’ 에 해당하는 일명 ‘래핑함수’ 의 존재가 필수불가결하다.

래핑함수를 위한 선택지는 크게 이하의 3가지가 존재한다:

Cython 라이브러리
pybind11 라이브러리
필요에 맞게 래핑 함수를 직접 작성
인풋 아웃풋 효율 문제와 신뢰성 문제로 코드를 직접 짜기보다는 외부 라이브러리 사용. 여기선 범용적으로 사용되는 래핑용 라이브러리인 pybind11을 사용하겠다.

3.2.1 Wrapping Timing
위에서 확인하였듯 c++ 에서의 처리속도는 python보다 빠름. 그러나 c++에서 생산한 값을 python 단에서 받을 때, 속도가 급격하게 느려지는 현상 발생함.

이러한 문제점들을 고려할 때 iteration 부분 작업을 최대한 c++ 파트에 몰아넣은 후 모든 iteration을 처리하였을 때 값을 수령해야함.

그러나 이렇게 몰아넣는다고 한다면 파이썬 파트에서 현재 numpy 형식으로 데이터를 처리하고 있으므로 c++ 쪽에서도 numpy 형태에 맞추어 값을 전달해야 하나 c++ 쪽에서 직접적으로 numpy 자료형을 지원하는 것은 불가능.

이를 해결하기 위해 c++ 쪽에서 획득한 결과값을 모두 container에 포함시킨 후 파이썬 쪽에서 수령한 후 해당 컨테이너에서 값을 꺼내어 numpy 자료형에 맞도록 재배치. 다소 시간의 손실은 있을지언정 각 iteration마다 값을 수령하는 것보다는 훨씬 빠름.

3.2.2 Library needed in c++
위에서 iteration 파트를 c++에서 모두 돌리기로 결정하였다. 여기서 iteration 은 크게 2개, BTM 부분과 lsirm 파트. 이 둘은 모두 2차원 행렬에 대해 적용되므로 c++ 에서 활용할 수 있는 선형연산 수단이 필요함. c++ 자체로 선형연산을 지원하고 있지는 않으므로 c++ 라이브러리를 적용해야 함.

c++에서 사용할 수 있는 메이저한 선형연산 라이브러리에는 크게 armadillo 와 eigen 의 2가지가 존재. 둘사이의 차별점을 정리하면 아래와 같다.

Package	armadillo	eigen
Matrix Multiplication	available	available
More than 2d Matrix	cube (3d)	-
generating function for probability	None	Dirichlet
eigen 또란 확률생산 기능이 armadillo 보다 강력하다는 점에서 충분한 차별점을 지니고 있음. 그러나 해당 패키지에서는 이터레이션 내부에서 2차원 행렬을 샘플로서 여러번 생산해 이를 묶어서 파이썬으로 보내야 함. 이인즉 이를 3차원 행렬로 인식할 수 있다는 것이며, 이는 곧 3차원 행렬을 지원하는 쪽이 데이터를 다룸에 있어서 유리하다는 것을 의미함. 따라서 3차원 행렬을 지원하는 armadillo 를 eigen 보다 우선하여 채택한다.

3.2.3 접합 모델 검증 및 성능 비교
위에서 사용했던 예시와 동일하게 속도 퍼포먼스 예시로서 이하의 샘플을 사용한다.

문서갯수	corpus	주제갯수
15281	3079	10
위와 동일한 방법으로 corpus 갯수 별 소모시간을 그래프로 표기하면 다음과 같다.


plot_for_each_corpus_usages

보면 알 수 있듯이 python 에서 이터레이션을 진행했을 때에 반해 평균 약 3배의 속도 향상을 보임. 실사용 가능한 수준으로 유의미하게 개선되었다고 볼 수 있다.







4 Implementation
이 section은 앞에서 제시한 알고리즘을 string input 에 실적용할 수 있는 topic_cluster_visualizer 패키지의 function에 대해 논한다. 해당 package 는 https://pypi.org/project/topic-cluster-visualizer/ 에서 설치할 수 있으며, python 환경에서는 이하의 command 를 실행하는 것으로 설치할 수 있다.

The latest version of topic_cluster_visualizer can be installed directly from PyPI repository of Python pacakges using:

pip install topic-cluster-visualizer
The package requires:

Python programming language
numpy, a package for efficient manipulation manipulation of multidimensional arrays,
pandas, a package for efficient manipulation manipulation of non-numeric 2-dimensional arrays,
plotly, a plotting package,
factor_analyzer, a package for
nltk, a package for Natural Language Processing (NLP)
gensim, a package for Natural Language Processing (NLP)
pybind11, a python library for wrapping c++ function module for multiple iteration part
And also system must support c++, which means c++ tools have to be installed.

topic_cluster_visualizer 는 크게 4가지로 나뉜다.

preprocess(): word2vec 을 통해 corpus 획득
btmize(): corpus list 를 넣으면 Biterm Model 을 통해 각 corpus 들에 확률을 부여
lsirmize(): 부여된 확률 기반으로 Gibbs Sampling 을 돌려서 각 corpus 들의 latent topic 을 추정하고 추정한 topic 들의 latent coefficient 추정
fit(): 획득한 latent space coefficient 들에 procrustes matching 2번과 oblique rotation 을 적용하여 동일 quadrant 에 coefficient 들을 배치시켜 해당 주제들간의 interaction 시각화
The functions feature a consistent syntax. The following are the arguments of the fisher() function as an illustration.

python> args(fisher)
function (p, adjust = "none", R, m, size = 10000, threshold,
side = 2, batchsize, nearpd = TRUE, ...)
NULL
We will explain the purpose of the various arguments in the following sections.

class TopicClusterVisualizer:
    def __init__(self, target_data):
need to be initialized with target_data, which is wanted to be analyzed.

4.1 preprocess()
preprocess(self, train_data = None, keywords = None, train = False):
상기하였듯이 해당 함수에서는 자연어처리하여 corpus 를 획득. 이는 이하와 같은 절차로 이루어진다. 이의 기본적인 corpus 처리는 nltk 패키지를 통해 이루어지며, 해당 word2vec 기반 자연어처리를 활성화시켰을 경우 이는 gensim 패키지의 word2vec() 함수를 이용한다.

절차는 다음과 같다.

python 내부에서 자연어처리. 입력값으로 받은 다수의 documents 들을 1차적으로 자연어처리하여 corpus 로 분해. word_tokenize 이때 tagging 해서 건지는 언어는 명사와 형용사로 한정한다 - 명사는 주제어, 형용사는 주제어를 수식할 수 있으나 동사는 상대적으로 주제를 드러냄에 있어서 그 역할이 약함


모드 따라서 변경. 
train 사용을 끌 경우 단순 NLP 후 corpus 생산에서만 끝냄. 이는 corpus 빈도에 따른 필터링 없이 생산된 모든 corpus 들을 다 사용하므로 퀄리티 크게 낮아짐. 입력된 train용 값들과 keyword용 값들을 총합하여 model 생성. using internally-used-only function _train_corpus.

train 사용을 켤 경우 word2Vec 을 적용. 적용의 구체적인 프로세스는 이하와 같다.
우선 train_data 통하여 word2Vec 을 통하여 모델 생산.
min_freq 라는 변수 임의로 지정. keyword 와 corpus 출현 단어들 중 최소한도 이상으로 출현하는 단어들 추려내기 위한 바로미터.
키워드에서 상위출현 단어 골라내고, 키워드에서 골라낸 상위출현 단어 중에서, (일례로 a) a가 model 에서 판정한 단어에 포함되어 있다면, a와 유사도가 높은 단어들을 포함시킨다. 패러미터 near_term_topn_val 사용. 디폴트값은 10. term 이 인풋되었을 때, 그것이 우리가 제작한 모델에 속해있는 term이라면, - model.wv.key_to_index.keys() 라는 값을 사용한다. 해당 term 과 유사도가 높은 단어를 뽑아둔다 - model.wv.most_similar(term, topn=near_term_topn)]
corpus에서 상위출현 단어 골라내고. 앞에서 모델과 keyword 간의 교집합 단어들과의 높은 유사도 단어랑, corpus 단어와의 교집합만 뽑아서 저장한다.
※ run with train parameter as 1 is STRONGLY RECOMMENDED. performance of the algorithm is drastically weakened without word2vec sequence.

4.2 btmize()
위에서 획득한 corpus 들을 BTM 알고리즘을 통하여 샘플 갯수를 늘린 후 각 주제 하에서의 등장 확률을 추정. BTM 을 거치는 이유는 최대한 샘플 갯수를 늘려 추정의 정확성을 높이기 위함. 각 document 로부터 추려낸 단어들 각각에 대해 BTM 적용해서, 얘들을 각각 쌍으로 묶어서 sample 의 절대개수를 늘림. 이렇게 절대개수를 늘린 샘플들에서 바탕에 두고 있는 샘플의 개수를 empirical 하게 세팅하고, MCMC 방법론을 통해 이터레이션을 다횟수 돌리는 것으로 매 이터레이션에서 각 단어의 출현 확률을 보정해나감.

이 이터레이션의 속도를 높이기 위해 pybind11 으로 래핑한 btm_cpp 함수 도입. 해당 함수의 argument 는 이하와 같다.

4.3 lsirmize()
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
해당 함수에서는 위의 BTM 과정을 거쳐 각 주제가 조건으로 주어졌을 때, 각 단어에 부여된 확률 기반으로 Gibbs Sampling 을 돌려서 각 corpus 들의 latent topic 을 추정하고 추정한 topic 들의 latent coefficient 추정한다. 이때 부여해둔 값은 원본 논문에서 이터레이션용 하이퍼패러미터로 사용했던 값들에 해당한다. 변경이 필요하다면 입력한 후 사용.

상술하였듯이 해당 알고리즘을 돌림에 있어서 다양한 corpus 확률 범위에 걸쳐 알고리즘을 돌려본 후, corpus 범위별로 판정된 주제의 coordinate 를 2차원 그래프에 매핑한다. 따라서 확률 범위를 정해주는 것이 필요하다. 해당 확률 범위는 % 단위로 디폴트값은 50 하나로 설정되어 있다. 만약 여러가지 구간에 걸쳐 corpus 비율을 설정하고 싶다면 상응하는 확률구간의 % 값을 list 혹은 tuple 자료형으로 입력하면 된다. 가령 50퍼센트부터 55퍼센트 구간까지 1퍼센트p 차이로 coordinate 변화를 체크하고 싶다면 [50,51,52,53,54,55]를 패러미터로 주면 된다.

이때 언급하였듯이 해당 파트에서의 깁스 샘플링에서의 이터레이션의 속도를 높이기 위해 pybind11 으로 래핑한 c++ 함수를 도입해주어야 한다. 해당 패키지에서는 이를 위하여 using internally-used-only function onepl_lsrm_cont_missing 함수를 도입하였다. 해당 함수의 parameter 는 이하와 같다.

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
c++ 로 작성했기에 데이터형이 c++ 기반으로 쓰여있긴 하나 이 자체는 python 함수로서 작동한다. 해당 함수는 각 확률구간마다 lsirm 파트를 실행한 후, lsirm 을 통해 각 이터레이션 별로 획득된 패러미터의 값들을 총합하여 해당 확률구간에서의 패러미터를 추정한다. 이를 통해 결과값은  dict 포맷으로 반환되며, 해당 dict 에는 z, map, phiwz, words 의 4가지 key 가 존재한다. 각각의 담고있는 내용은 이하와 같다.

z: 각 이터레이션에서 추정된 각 주제별 2차원 latent coordiante. #ofiteration × #oftopics × 2 크기의 행렬.
map: 각 이터레이션 별로 얻어진 원점과의 총 거리.
phiwz: topic z 가 주어졌을 경우의 corpus w 의 출현확률
words: 해당 corpus 에서 어떤 corpus 들이 사용되었는가
이때 다른 attribute 들에 비해 words attribute 가 왜 필요한지에 대한 의문이 있을 것. 우리가 목표로 하는 것은 글줄 모음에서 얻을 수 있는 각 주제별의 상관관계이다. 지금까지 진행한 작업으로 주제별로 coefficient 를 얻어서 배치하는 건 가능하나 각 주제를 이름붙일 수 없으면 이는 무의미할 것이다. 따라서 이렇게 획득한 각 주제 하에서의 단어 출현 확률에서 각 주제를 어떻게 이름 붙일 것인가에 대한 재료를 확보해야할 필요가 있다.

이에 가장 직접적으로 활용할 수 있는 재료는 앞서 획득한 단어별 발생 확률이다. 타 문서에서의 발생 확률이 낮고, 해당 주제군에 속하는 문서들에서만 여러번 발생하는 단어들이라면 해당 단어는 해당 주제군에만 묶여 있다는 것으로 해석할 수 있으며, 이는 곧 해당 주제를 어떻게 이름 붙일 것인가 하는 고민에서 유의미하게 활용될 수 있을 것이다.

본 논문에서는 이 과정에는 모든 단어를 참고해서는 안되고 다른 주제군에서는 출현빈도가 낮고, 이 주제군에서는 높다는 조건을 설정하고 corpus를 선택하였으나, 단어를 어떻게 사용할 것인지 자체는 유저의 자유.

4.4 fit()






5 구현 모델 실적용 예시
5.1 데이터 서술
상술하였듯이 해당 알고리즘의 결과값을 도드라지게 만들기 위해서는 문단이 짧으면서도, 해당 문단의 의미하는 바가 명확한 글줄들을 입력값으로 넣었을 때 결과값이 도드라진다. 따라서 만족스러운 결과를 위해 해당 조건에 맞는 데이터를 사용하자.

앞서 언급하였듯이 해당 논문의 목적은 특정 연구분야를 빠르게 개괄하고 이를 유저에게 제공하는 것에 있다. 따라서 이의 실사용례를 제공하기 위해선 특정 연구분야를 정해야 할 필요가 있다. 가령 아래와 같은 주제는 어떨까. 2016년 알파고의 등장 이래 분야를 가리지 않고 딥러닝을 위시한 컴퓨터 과학에 대한 관심이 증가하였다. 특히 경영학에서는 MIS 라는 이름으로 타 분야에 비해 학문 자체에서 컴퓨터를 다루는 비중를 다루는 비중이 다소 높았던 편이다. 이러한 측면을 감안할 때 알파고의 도래 이후 모든 학문영역에 미쳤던 충격은 경영학에게 있어서는 크면 컸지 작다고 보기 어려울 것이며, 이는 곧 알파고 등장 이후 학계 논문의 주제 트렌드에 있어서 변화가 있지 않았을까 하는 의심을 품는 것에 대한 합리성을 부여해준다. 이러한 생각을 가정하였을 때 우리는 MIS 에서 딥러닝 등장에 따른 학계 논문의 주제 변화를 살펴보는 것으로 학계의 딥러닝에 대한 반응을 확인할 수 있다.

우리는 해당 알고리즘에서 상위 몇퍼센트의 corpus 를 주제 추정에 사용할 것인가에 대한 확률구간을 임의로 설정하고 각 확률구간에서의 latent coordinate 를 살펴볼 수 있다. 이때 해당 주제에 속한 논문들의 논지가 해당 주제에 확고하게 묶여있다면 이런 확률구간의 변화에 따른 coordinate 의 변화는 크지 않을 것이며 이에 따라 latent coordinate 들은 각각 어떤 형태의 cluster 를 이루게 될 것이다. 반면 해당 주제의 coordinate 들이 cluster 를 이루지 못하고 확률구간의 변화에 따라 2차원 상에서 계속 움직이는 꼴이 된다면 이는 곧 해당 주제 속한 문헌들의 주제가 해당 주제에 확고하게 묶여있지 못하다는 것으로, 해당 문헌들의 주제가 명확하게 드러나는 것이 아닌 다소 두루뭉술하다는 것을 나타낸다고 인식될 수 있다. 이는 바꾸어 말하면 해당 주제가 부차적인 영역에 그쳤다는 것일 것이므로 학계 내에서의 해당 주제의 입지가 그리 높지 않다는 것으로 해석될 수 있을 것이다. 따라서 곧 논문 주제의 cluster 정도를 살피는 것은 우리가 목표로 하는 경영학에서의 MIS 분야가 딥러닝 도래에 어떤 반응을 보였는지에 대한 인식을 확인할 수 있는 수단이 된다.

이를 분석하기 위해 알파고의 등장인 16년을 기준으로 하여 17년부터 21년까지의 경영학 학계에서의 MIS 관련 논문들의 5년치 데이터를 모아 위의 알고리즘을 통하여 분석을 진행하자. 해당 조건에 맞는 데이터로는 논문 아카이브 사이트인 Web of Science 에서 Management, Business 분야의 논문들 중 MIS 를 다루는 논문들로부터의 abstract 를 확보하여 진행하였다. 이렇게 획득한 데이터와 empirical 하게 지정한 주제의 개수를 서술하면 이하와 같다.

문서갯수	corpus	주제갯수
15281	3079	10
5.2 알고리즘 결과
이렇게 획득한 데이터에 위의 패키지를 적용하여 시각화한 결과를 획득하였다. 이때 타 확률구간에 대한 procrustes matching 에 있어 기준선으로 작동한, 가장 거리가 멀었던 확률구간 기준으로 표기한 coordinate 는 이하와 같다.


plot_for_max_matrix_coordinate

TOPIC NEED TO BE NAMED
상술하였듯이 일련의 과정을 통해 얻어지는 주제는 단순히 다를 뿐 이 각각 다른 주제가 무엇에 대한 것인지에 대해서는 오롯이 연구자의 몫으로 남아있습니다. 이 이름을 어떻게 지정할 것인가에 대해서는 분석을 진행하는 연구자의 주관에 따라 결정되어야 할 것입니다. 이를 위해 해당 패키지에서는 설정한 확률 구간에 따라 사용된 corpus들이 무엇인지를 반환하는 attribute 로 lsirmize() 함수에 의해 배정되는 words attribute 가 배정되어 있습니다. 해당 attribute 를 사용해서 주관적으로 이름을 지정해주십시오. 본 논문에서 주제를 명명함에 있어서는 이하와 같은 룰로 이름을 지정하겠습니다.

타 논문에서 출현하지 않은 corpus를 최우선으로 참고하여 이름 지정
위에서 이름을 지정한 주제군을 제외하고 나머지 주제군으로 corpus 사용 여부를 참고하여 이때 출현하지 않은 corpus 를 기준으로 이름 지정
최종적으로 이름이 지정되지 않은 주제군들이 있을 경우, 타 주제들을 통하여 각 coefficient 들의 대소가 갖는 의미를 추측한 후 이를 참고하여 주제들의 coefficient 들과 겹치는 corpus 들을 통해 주제의 이름 추정
이를 위하여 각 documents 들에서 유일하게 등장한 corpus 들과, 그렇지 않은 corpus들 중 고확률로 등장하였던 corpus 들을 나타내면 다음과 같습니다.

Unique Corpus	High-probability Corpus
1	‘load-depend’, ‘lithium-ion’, ‘n-vehicl’, ‘europcar’, …	‘econometr’, ‘guidelin’, ‘socio-techn’, ‘reproduct’, …
2	‘human-machine-environ’, ‘datasheet’	‘guideline, ‘budget-constraint’, ‘fintech’, ‘classification-base’, …
3	‘eql’ (equity loan)	‘naval’, ‘sea-land’, ‘risk-rel’, ‘blockchain’, ‘obsolesce’, …
4	-	‘state-of-the-art’, ‘ubiquitous’, ‘seaport’, ‘warehous’, ‘techniq’, …
5	‘incentive-bas’, ‘s-crm’, ‘nation-dyad’, ‘ai-aug’, ‘accultur’, …	‘discret’, ‘transact’, ‘state’, ‘civil’, ‘telemat’, ‘transform’, …
6	-	‘techniq’, ‘cross-sect’, ‘transmiss’, ‘worldwide’, ‘sement’, ‘agricult’, …
7	‘margin-trad’, ‘future-focus’, ‘protection-motiv’	‘mathematic’, ‘econometr’, assess’, ‘itil’, …
8	‘reuse-bas’, ‘geo-ecolog’, ‘molybdenum-contain’, …	‘textile’, ‘robust’, ‘retrain’, ‘quantity-pay’, ‘geograph’, …
9	‘assemble-to-ord’, ‘evm’, ‘chat-bot’, ‘feature-process-machin’, …	‘transboundary’, ‘quantity-pay’, ‘translat’, ‘multi-type’, …
10	‘hardware-softwar’, ‘regime-switch’, ‘competition-bas’, …	‘benchmark’, ‘simulat’, ‘ontology-bas’, ‘human-computer’, …
이에 기반하여 위에서 서술하였던 룰에 따라 주제를 명명하면 다음과 같습니다.

Name of Topics
1	전기차
2	Excel 등 DB 관리
3	회계 분야에서의 신기술 사용 관련
4	최신기술, DB 관리
5	이문화 조직구성원 간 소통
6	글로벌, 분야간 통섭
7	금융시장 분야
8	지속 가능한 환경경영
9	비트코인 위시한 블록체인 및 딥러닝 관련
10	경영 최전선에서의 디지털 기술 활용
이제 주제를 명명한 바 이상으로 해당 데이터들에 대한 인사이트를 획득하기 위해 각 확률구간에 따른 coordinate 의 변화를 확인하겠습니다. 이는 다음과 같습니다.


plot_for_each_matrix_coordinate

여기서 타 사분면들 대비 1, 4분면 근방의 점이 많다는 점을 통해 근 5년간 딥러닝을 위주로 한 컴퓨터 과학 기술이 발전하였음에도 여전히 mis 논문들은 고전적인 경영학 이론을 다루는 경우가 많다는 것을, 그리고 네이처나 서스테이너블한 요소보다는 지오그래피컬한 실제적이고 구체적인 주제에 집중하고 있다는 사실을 파악할 수 있습니다.

이때 여기에, 결과의 시인성을 높이기 위해 확률구간의 변화에 따른 coordinate 이동을 화살표로 명시해주는 것으로 주목해볼 만한 유의미한 인사이트를 얻을 수 있습니다.


trajectory_for_each_matrix_coordinate

아까 말씀드렸듯이 동일 컬러링 상에서의 서로 다른 점들은 해당 topic 에서 확률구간에 따라 서로 다르게 나타난 coordinate 로, topic에서의 각 확률구간마다 corpus 등장 확률에 기반하여 추정에 사용된 corpus 데이터가 다릅니다. 확률 구간을 좁게 잡으면 가령 상위 40%의 확률로 등장하는 corpus들만이 주제 추정에 사용되지만 확률 구간을 넓혀감에 따라 최종적으로 상위 60%까지의 corpus들이 주제 추정에 사용되게 됩니다. 이는 곧 토픽 추정에 사용되는 corpus의 총량이 변화한다는 의미이며 이에 따라 추정된 주제의 형태가 변하는 경우가 발생하는 것은 당연하다고 말씀드렸습니다.

그러나 trajectory 를 보시면 확인하실 수 있듯이 디지털 경향이 강한 topic이 아날로그 쪽이나 organization 쪽으로 주제가 변하는 경우는 없으며 반대 또한 마찬가지입니다. 즉 확률 구간에 따른 topic의 coordiante 의 이동이 각 axis의 양 극단을 쌍으로 하여 그 사이에서만 이루어지고 있으며 이는 mis 연구에서의 방법론 현황에 대한 주목해볼 만한 단서를 던져줍니다.

즉 topic 들 중 소속된 문헌이 하나의 강력한 주제에 묶여있는 것이 아니어서 corpus 사용량에 따라 추정된 topic 이 변화하는 케이스에서조차도, nature 나 서스테이너빌리티의 관점을 다룬 topic이 클래시컬한 기존 경영학에서의 관리 일원들이나 아날로그한 측면의 토픽들과는 어울리지 못하고 디지털 및 테크놀로지 관점과만 상호 작용하고 있는 것입니다. 또한 역으로 logistic 이나 geography 측면의 터팩들은 analogue와 technology 사이에서 균형을 잡은 이론이 한계일 뿐 디지털 디지털 측면에 치우친 topic은 찾기 어렵습니다.

이는 곧 필드를 불문하고 학계 전체에 충격을 주었던 딥러닝 혁명이 아직 디지털 분야에서만 한정되어 논해지고 있다고 볼 수 있으며 딥러닝 혁명이 가지는 강력한 잠재력을 볼 때 이는 학계에 있어 커다란 손실이라고 할 수 있을 것입니다. 이러한 부분을 보완하여 서스테이너빌리티 측면과 클래식한 기존 경영학 이론을 좀 더 적극적으로 융합한 논문이 늘어나는 것을 통해 학계에서 진행되는 논의 토양이 조금 더 비옥해질 수 있지 않을까 조심스레 제안해 봅니다.







6 결론
Xiaohui Yan, A Biterm Topic Model for Short Texts↩︎