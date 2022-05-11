
---
title: "Untitled"
output: 
  html_document:
    number_sections: true
---

```{r, setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE)
```

```{css, echo=FALSE}
.header-section-number::after {
  content: ".";
}
```










저작자표시-비영리-변경금지 2.0 대한민국
이용자는 아래의 조건을 따르는 경우에 한하여 자유롭게

⚫    이 저작물을 복제, 배포, 전송, 전시, 공연 및 방송할 수 있습니다.
다음과 같은 조건을 따라야 합니다:

저작자표시. 귀하는 원저작자를 표시하여야 합니다.

비영리. 귀하는 이 저작물을 영리 목적으로 이용할 수 없습니다.

변경금지. 귀하는 이 저작물을 개작, 변형 또는 가공할 수 없습니다.

⚫    귀하는, 이 저작물의 재이용이나 배포의 경우, 이 저작물에 적용된 이용허락조건
을 명확하게 나타내어야 합니다.

⚫    저작권자로부터 별도의 허가를 받으면 이러한 조건들은 적용되지 않습니다.

저작권법에 따른 이용자의 권리는 위의 내용에 의하여 영향을 받지 않습니다.
이것은 이용허락규약(Legal Code)을 이해하기 쉽게 요약한 것입니다.

Disclaimer


Joint Latent Space Model for Analyzing
Egos’ Network and Alters’ Attributes

Jeewon Lim

The Graduate School
Yonsei University

Department of Statistics and Data Science


Joint Latent Space Model for Analyzing
Egos’ Network and Alters’ Attributes

A Masters Thesis

Submitted to the Department of Statistics and Data Science
and the Graduate School of Yonsei University

in partial fulfillment of the
requirments for the degree of
Master of Arts in Statistics

Jeewon Lim

February 2022


This certifies that the masters thesis
of Jeewon Lim is approved.

Thesis Supservimsor: prohfessor Ick Hoon Jin

professor Hakbae Lee

professor Jongho IM

The Graduate School
Yonsei University
February 2022


Contents

List of  Figures                                                                                    
                     iii

Abstract                                                                                            
                         iv

1    Introduction                                                                                   
                       1

2    Related Work                                                                                   
                    5

2.1     Latent  Space  Model                                                                        
               5

2.2     Latent  Space  Item  Response  Model                                                        
     6

3    Proposed Method                                                                                
               9

3.1     Model                                                                                       
                        9

3.2     Bayesian  Inference                                                                         
               10

4    Application                                                                                    
                      14

4.1     Data                                                                                        
                        14

4.2     Objective                                                                                   
                    16

4.3     Model                                                                                       
                      17

4.4     Result                                                                                      
                       18

5    Conclusion                                                                                     
                      22

i


References                                                                                          
                      23

Abstract in  Korean                                                                                 
              26

ii


List of Figures

4.1     Network  Relationships  in  the  Tala  Immigrant  Community                   16

4.2     Latent  Positions  of  Egos  and  Alters’  Attributes                                      
19

iii


ABSTRACT

It  is  widely  known  that  Mexican  immigrants  have  less  access  to  medical  care
and  have  significant  difficulty  acquiring  necessary  dental  services  compared  to
American-born Latinos. It is also known that Latino culture values Familismo and
tends  to  form  a  network  including  kin,  fictive  kin  and  peers  who  all  contribute
to  one’s  well-being.  Therefore,  it  is  not  surprising  that  when  it  comes  to  vital
problems  like  dental  care,  Mexican  immigrants  rely  largely  on  close  friends.  The
relationship  between  Mexican  immigrants’  networks  and  their  access  to  dental
treatments,  on  the  other  hand,  is  poorly  understood.  As  a  result,  it’s  critical
to  analyze  how  Mexican  immigrants’  social  networks  influence  their  utilization
of  oral  health  services.  This  paper  attempts  to  model  the  relationship  between
Mexican  immigrants’  network  and  dental  conditions  using  a  joint  latent  space
model that combines the network model of the ego, and the item response model
on the attributes of the alter. By reflecting the network of ego in the item response
model, joint latent space model can observe the ego and the attributes of the alter
in one latent space. We apply joint latent space model to Tala Survey Study and
the findings reveal that items such as whether alter often sees dentist lies on the
opposite direction to the items such as whether alter has frequent dental problems

iv


on  the  latent  space.  This  paper  examines  the  interaction  between  ego  and  alter
by  applying  network  of  Mexican  immigrants  and  the  attribute  data  of  alters  to
the  joint  latent  space  model.

v


Chapter 1

Introduction

It  is  commonly  known  that  Lations  have  a  disproportionate  number  of  dental
problems  (Dye  B,  2015;  Eke  PI,  2015).  According  to  a  2019  CDC  analysis,  the
prevalence  of  caries  and  untreated  decay  was  more  than  2  times  higher  among
Mexican  American  (15.1%)  2-5  year  old  children  between  2011  and  2016,  com-
pared  to  white,  non-hispanic  groups  (6.7%).  The  preceding  data  are  not  just
for  kids.  Untreated  deterioration  was  more  common  among  Mexican  American
adolescents  (20.8%)  than  among  non-Hispanic  white  adolescents  (15.6%)  (CDC,
2019). This situation stems from the fact that Mexican immigrants have less ac-
cess to medical care, such as dental treatments, than other racial/ethnic groups,
resulting in  poor  dental  health  (WALL and  BROWN,  2004).

Biological susceptibility, constraints in the health-care system, and lifestyle
choices  (Maupome  G,  2015)  have  all  been  identified  as  possible  explanations
of  these  disparities  in  oral  health.  Another  study  looked  into  how  Mexican-
Americans’ dental health is influenced by networks and acculturation (Maupome G,
2016).  Mexican  immigrants,  unlike  other  racial/ethnic  groups,  tend  to  develop
clan  structures  that  encompass  family  and  community  networks.  This  network

1


is  known  as  Familismo  (McAdoo,  1999).  Familismo  plays  an  important  role  in
the community and is frequently utilized as a foundation for how Mexican Amer-
icans  approach  health  and  sickness  (Maupome  G,  2016).  Familismo determines
how  its  members  behave  and  make  decisions  multidimensional  system  of  val-
ues that underpins conventions and beliefs as well as transgenerational solidarity
(Stein et al., 2015). In fact, according to a qualitative study (Maupome G, 2015),
obtaining  emergency  dental  care  was  encouraged  by  peers  (parents,  co-workers,
etc)  (Cohen  LA,  2009).

Tala  Survey  Study  data  was  designed  to  collect  egocentric  network  data
on  Mexican  immigrants  in  the  Midwest  of  the  United  States.  327  Mexican  im-
migrants  (egos)  were  asked  about  their  oral  health,  health  practices,  and  views
around  oral  health,  and  their  network  structure  was  collected.  There  is  also  in-
formation on the oral health, health practices, and oral health attitudes of 1,017
people with whom egos share important issues, as well as their network structure.

Using  data  from  the  Tala  Survey  Study,  various  studies  have  attempted
to  investigate  the  association  between  the  network  of  Mexican  Americans  and
their  dental  issues.  Using  Social  Network  Analysis  (SNA),  Maupome  discovers
individual  actor  traits  and  dyadic  ties  that  determine  whom  Mexican-American
immigrants  communicate  to  regarding  oral  health  problems  in  relation  to  their
usual  dialogue.  By  fitting  random-intercept  logistic  regression  models  that  nest
alters with egos, the study study found that egos with lesser behavioral accultur-
ation are more likely to rely on competent peers for discussion of dental concerns,
whereas egos with higher behavioral acculturation are less likely to leverage such

2


alters  (Maupome  G,  2016).  Pullen  uses  logistic  regression  to  look  at  how  net-
work  characteristics  influence  oral  health  behaviors  among  Mexican  Americans,
and finds that network size, network dental service utilization, and the frequency
with  which  Mexican  Americans  discuss  acute  problems  with  network  ties  posi-
tively correlate with the use of oral health services (Pullen E, 2018). Both studies
use  a  random-intercept  logistic  regression  model  and  a  logistic  regression  model
to try to uncover the association between Mexican Americans’ network structure
and their usage of oral health services. Both methodologies, however, can only ex-
amine  the  relationship  between  egos’  network  and  alters’  attributes  respectively
and  cannot  capture  the  dependence  structure.

In  order  to  model  the  dependence  structure  of  network  data,  there  are
several  statistical  methods  based  on  Latent  Space  approach.  The  basic  model
is  Latent  Space  Model  (Ho↵  et  al.,  2002).  Latent  Space  Model  is  one  approach
to  Social  Network  Analysis  where  the  probability  of  a  relation  between  actors
depends  on  the  positions  of  individuals  in  an  unobserved  “social  space”.  Latent
Space  Model  models  the  relation  between  actors  in  undirected/directed  network
data and maps into latent space to capture the pattern of actors. Another Latent
Space  approach  model  is  Latent  Space  Item  Response  Model  (Jeon  et  al.,  2021)
which  can  model  bipartite  network  data.  Latent  Space  Item  Response  Model  is
a combination of Latent Space Model and Item Response Model where Item Re-
sponse Model is a widely used approach for analyzing responses to items given by
respondents. Latent Space Item Response Model can model the dependence struc-
ture of respondents and items in a single latent space and generate an interaction

3


map  that  depicts  interactions  of  respondents  and  items.  However,  Latent  Space
Model can only model network structure, and Latent Space Item Response Model
can only model bipartite network structure, which is not sufficient to model both
network  structure  and  bipartite  network  structure  of  Tala  Survey  Study  data
simultaneously.

To overcome the constraint, we apply Joint Latent Space Model to analyze
the  interaction  between  ego  and  alter  and  to  take  into  account  the  dependence
structure  in  one  latent  space.  Joint  Latent  Space  Model  is  a  joint  latent  space
approach combining Latent Space Model and Latent Space Item Response Model.
In  this  paper,  we  propose  joint  Latent  Space  Model  and  apply  to  Tala  Survey
study  in  order  to  model  the  dependence  structure  of  egos’  network  and  alters’
bipartite  network  and  analyze  the  interaction  between  egos’  network  and  alters’
attributes  mapped  in  one  latent  space.

This  paper  is  organized  as  follows:  We  describe  previous  Latent  Space
approach  methods  in  Chapter  2,  introduce  our  proposed  method  in  Chapter  3,
apply the proposed method to Tala Survey study data in Chapter 4. We conclude
the  paper  in  Chapter  5.

4


Chapter 2

Related Work

2.1     Latent  Space  Model

Ho↵  proposed  Latent  Space  Approaches  to  Social  Network  Analysis,  where  the
dependence structure between actors are reflected on an unobserved latent space
called  “social  space”.  Latent  Space  Model  can  analyze  both  directed  and  undi-
rected relations, and the probability of a relation between actors depends on the
positions  of  individuals  in  a  visualized  latent  space.  Latent  Space  Model  takes  a
conditional  independence  approach  to  modeling  by  assuming  that  the  presence
or  absence  of  a  tie  between  two  individuals  is  independent  of  all  other  ties  in
the system, given the unobserved positions in social space of the two individuals,
where  X and  xi,j are  observed  characteristics,  and  ✓ and  Z are  parameters  and


positions  to be  estimated.

P (Y |Z, X, ✓) = Qi

j P (yi,j|zi, zj, xi,j, ✓)                                 (2.1)

There  are  two  methods  to  measure  latent  position  in  Latent  Space  Model:  (i)
distance  models,  (ii)  projection  models.  Distance  model  is  a  convenient  parame-
terization  of  P (Y |Z, X, ✓)  using  the  logistic  regression  model  in  which  the  prob-

5


ability  of  a  tie  depends  on  the  Euclidean  distance  between  zi and  zj,  as  well  as

on observed covariates xi,j that measure characteristics of the dyad. If two actors

are far away from each other on the latent space, it indicates that the probability
of  a  relation  between  actors  are  smaller,  therefore  the  absolute  value  of  distance
a↵ects  the  log-odds  of  the  probability  in  the  negative  direction.

⌘i,j = logit(P (yi,j = 1 | zi, zj, xi,j, ↵, β)) = ↵ + β⁰xi,j—k zi — zj k         (2.2)

Latent Space Model is used to represent relational information among interacting
units and provides a visual and interpretable model-based spatial representation
of  social  relationships.

2.2     Latent  Space  Item  Response  Model

Latent  Space  Item  Response  Model  was  proposed  by  Jeon  to  model  Item  Re-
sponses  and  analyze  the  interaction  between  respondents  and  items  at  the  same
time.  Latent  Space  Item  Response  Model  is  a  combination  two  models:  (i)  La-
tent  Space  Model,  (ii)  Item  Response  Model.  Item  Response  Theory  is  a  widely
used approach for analyzing test takers (respondents) and their responses to test
questionnaires  (items)  by  taking  into  account  both  the  level  of  test  takers  and
the  difficulty  of  the  test  items.  The  basic  Item  Response  Theory  model  is  Rasch
model (Rasch, 1961), which assumes that the log-odds of the probability that the
test  taker  j answers  the  test  item  i correctly  (Yj,i = 1)  is  as  follows:

logit(P (Yi,j = 1 | ↵j, βi)) = ↵j + βi                            (2.3)

6


It  can  be  interpreted  that  log-odds  of  the  probability  of  a  correct  response  to
item  i by  respondent  j is  the  summation  of  the  main  e↵ect  ↵j,  which  represents

the  ability  of  respondent  j,  and  the  main  e↵ect  βi,  which  represents  how  easily

item  i can  be  correctly  answered.  Rasch  model  assumes  that  the  item  responses
of  any  respondent  are  independent  to  each  other,  which  can  be  easily  violated
when  using  Item  Response  data.  Therefore,  Latent  Space  Item  Response  Model
combines Item Response Model and Latent Space Model in order to model Item
Response  and  the  dependence  structure  between  respondents  and  items  at  the

same time. When Latent Space Item Response Model is applied, both respondents
and  items  are  embedded  in  an  unobserved  latent  space  with  the  probability  of  a
correct  response  decreasing  depending  on  the  distance  between  the  respondents’
and items’ latent position. By mapping both respondents and items in one latent
space,  the  underlying  pattern  of  the  interaction  between  respondents  and  items

can be easily captured. The probability of a correct response by respondent j to
item  i depends  on  the  latent  position  aj of  respondent  j and  the  latent  position

bi of  item  i in  the  shared  latent  space.  Now  the  log-odds  of  the  probability  that

the  test  taker  j answers  the  test  item  i correctly  (Yj,i =  1)  can  be  expressed  as
follows:

logit(P (Yi,j = 1 | ↵j, βi, aj, bi)) = ↵j + βi — цd(aj, bi)                    (2.4)

where  d(aj, bi)  is  the  distance  between  latent  position  of  aj and  bi,  and  ц is  the
weight of the distance term. Combining Latent Space Model into Item Response
Model takes the interaction of respondent j and item i into account and enable to
visualize both respondents and items in a shared latent space. Latent Space Item

7


Response Model is viewed as a network model in the sense that item response data
can  be  viewed  as  a  bipartite  network,  which  contains  links  between  respondents
and  items  (Wasserman  and  Faust,  1994).

8


Chapter 3

Proposed Method

Latent Space Model and Latent Space Item Response Model are both useful mod-
els  to  analyze  network  data.  However,  Latent  Space  Model  can  only  model  the
dependence  structure  of  egos’  network,  and  Latent  Space  Item  Response  Model
can         only  model  the  dependence  structure  of  respondents’  item  responses  respec-
tively.  If  there  is  a  known  network  structure  of  the  respondents,  on  top  of  the
respondents’  bipartite  network  structure,  then  it  would  be  better  to  reflect  both
dependence  structures  in  the  latent  space.  Our  proposed  method  is  to  capture
the dependence structure of both respondents’ network and their item responses
simultaneously.

3.1     Model

The  likelihood  of  Joint  Latent  Space  Model  can  be  expressed  as  the  product  of
Latent  Space  Model  for  network,  and  Latent  Space  Item  Response  Model  for

9


bipartite  network  as  follows:

P (Y, X | Z, W, ↵, ✓j, βi)


N

j=1

N

k=1,k6=j

exp(↵—kzj —zkk)
1+exp(↵—kzj —zkk)

Yj,k                              1

1+exp(↵—kzj —zkk)

⌘1—Yj,k

(3.1)


N

j=1

P

i=1

exp(✓j +βi—kzj —wik)
1+exp(✓j +βi—kzj —wik)

Xj,i                                    1

1+exp(✓j +βi—kzj —wik)

⌘1—Xj,i

where  Y  is  network  data,  X  is  bipartite  network  data,  Z  is  latent  position  of
respondents, and W is latent position of items, ✓j is the main e↵ect of a respondent
j,  and  βi is  the  main  e↵ect  of  an  item  i.

Then  the  log-odds  of  the  probability  that  the  actor  j responses  to  the  item  i
positively  (Xj,i =  1)  when  actor  j and  actor  k have  relation  (Yj,k  =  1)  can  be
expressed  as  follows:


logit(P (Yj,k = 1, Xj,i = 1|zj, zk, wi, ↵, ✓j, βi))

= ↵ + ✓j + βi—k zj — zk k— k zj — wi k

(3.2)

The  proposed  model  has  theoretical  advantage  in  the  fact  that  it  reflects  the
relation among actors as well as the interaction between actors and items simul-
taneously.

3.2     Bayesian  Inference

Markov  Chain Monte Carlo (MCMC)

We  propose  a  fully  Bayesian  approach  by  applying  MCMC  methods  to  estimate
the  proposed  Joint  Latent  Space  Model.  Priors  are  as  follows:

10


↵ ⇠ N(0, σ↵)


✓j | σ²

⇠ N(0, σ² ), σ²

> 0,j = 1 ·· · N


βi ⇠ N(0, σβ),i = 1 ·· · P

2   | a, b ⇠ InvGamma(a, b),a > 0,b > 0

zj | D ⇠ MV ND(0, ID),j = 1 ·· · N
wi | D ⇠ MV ND(0, ID),i = 1 ·· · P

(3.3)

Then  the  posterior  of  the  parameters  ↵,  ✓,  and  β,  and  the  unobserved  latent
positions  of  actors  Z and  items  W  given  an  observation  y of  Y  and  x of  X is
proportional  to

f(↵, ✓, β, Z, W |y, x)


/ f(↵) hQN

f(✓j)i hQP

f(βi)i

(3.4)


N

j=1

P

i=1

P (Yj,k = yj,k, Xj,i = xj,i | Z, W, ↵, ✓j, βi)i

Estimation

We used Metropolis Hastings within Gibbs sampler to generate posterior samples
of  parameters  at  tth  iteration  as  follows:

Step  1) Propose  ↵⇤ from  a  symmetric  proposal  distribution  and  ac-
cept  the  proposed  sample  with  probability

min   1,  f(↵⇤ | y, x, z, w, ✓, β)                                (3.5)

f(↵(t) | y, x, z, w, ✓, β)

11


Step  2) Propose  zj⇤  from  a  symmetric  proposal  distribution  and  ac-
cept  the  proposed  sample  with  probability

min   1,  f(zj⇤ | y, x, ↵, z—j, w, ✓, β)                           (3.6)

f(z⁽ᵗ⁾ | y, x, ↵, z—j, w, ✓, β)

z—j = (z₁,. .., zj—₁, zj₊₁,. .., zN )

Step  3) Propose  βi⇤  from  a  symmetric  proposal  distribution  and  ac-
cept  the  proposed  sample  with  probability

min   1, f(βi⇤ | y, x, ↵, z, w, ✓, β—i)                           (3.7)

f(β⁽ᵗ⁾ | y, x, ↵z, w, ✓, β—i)

β—i = (β₁,. .., βi—₁, βi₊₁,. .., βP )

Step  4) Propose  ✓j⇤  from  a  symmetric  proposal  distribution  and  ac-
cept  the  proposed  sample  with  probability

min   1, f(✓j⇤ | y, x, ↵, z, w, ✓—j, β)                           (3.8)

f(✓⁽ᵗ⁾ | y, x, ↵z, w, ✓—j, β)

✓—j = (✓₁,. .., ✓j—₁, ✓j₊₁,. .., ✓N )

Step 5) Propose wi⇤  from a symmetric proposal distribution and ac-
cept  the  proposed  sample  with  probability

min   1,  f(wi⇤ | y, x, ↵, z, w—i, ✓, β)                           (3.9)

f(w⁽ᵗ⁾ | y, x, ↵, z, w—i, ✓, β)

w—i = (w₁,. .., wi—₁, wi₊₁,. .., wP )


Step 6) Propose  σ²

from  its  full  conditional  distribution:


N       ⌃N

✓2 !

We use Gaussian distribution for the symmetric proposal  distribution  where the
mean  is  the  current  values  of  the  parameters  or  the  latent  positions  of  actors

12


and  items  at  tth  iteration,  and  the  diagonal  variance-covariance  matrice  for  the
variance.

Identifiability

Since we used distance model to measure latent position in Latent Space Model,
there lies an identifiability issue as distances between a set of points in Euclidean
space are invariant under rotation, reflection, and translation (Ho↵ et al., 2002).
Such issue of identifiability can be resolved by applying a post-processing proce-
dure  called  Procrustes  transformation  (Gower,  1975).

13


Chapter 4

Application

4.1     Data

Data  for  this  research  are  from  the  Tala  Survey  Study,  which  was  designed  to
capture egocentric network data on Mexican immigrants living in the Midwestern
United States (Pullen E, 2018). Tala Survey Study data is consisted of two data
sets:  (i)  Network  data  of  egos,  (ii)  Item  Response  data  of  alters.  There  are  327
egos  and  their  relations  to  each  other  is  captured  in  network  data  set.  Each  ego
has  alters  whom  they  share  import  matters  with.  There  are  total  1,017  alters
where  the  minimum  number  of  alters  of  an  ego  is  1,  and  the  maximum  number
of  alters  of  an  ego  is  17.  Each  ego  has  approximately  4  alters  on  average.  Egos
were  asked  about  personal  information  and  oral  health  related  questions  of  each
alter and the collected information is stored in the Item Response data of alters.
There  are  9  items  of  1,017  alters  in  Item  Response  data,  and  the  items  includes
follows:

•  Aeducfive:  Highest  level  of  eduction  completed  (1:  higher  than  college,  0:
otherwise)

14


•  ARdentinsdum:  Dental  insurance  (1:  yes,  0:  no)

•  ARhlthinsdum:  Health  insurance  (1:  yes,  0:  no)

•  ARclosedum:  How  close  is  ego to alter  (1:  very  close,  0:  otherwise)

•  ARseedentdum:  Does  alter  see  a  dentist/dental  hygienist  at  least  once  a
year?  (1:  yes,  0:  no)

•  ARknowl: How much do you think alter knows about matters of teeth, gums
and  mouth?  (1:  a lot,  0:  otherwise)

•  ARprobsdum: Does alter have frequent problems with teeth/gums? (1: yes,
0:  no)

•  ARhassleissdum:  In  general,  how  much  does  alter  hassle  or  bug  you  about
dental  issues?  (1:  a  lot,  some,  a  little,  0:  otherwise)

•  ARtalkacdum:  During  the  past  12  months,  how  often  did  you  and  X  talk
about acute dental problems, such as a tooth ache? (1: at least once a year,
0:  otherwise)

15


4.2     Objective

Figure  4.1:  Network  Relationships  in  the  Tala Immigrant  Community

Figure  4.1  shows  the  network  relationships  in  the  Tala  Immigrant  Community,
where red ties represents whether egos and alters talks about Important matters,
green  ties  representing  whether  egos  and  alters  talks  about  Oral  Health  mat-
ters,  and  blue  ties  when  egos  and  alters  talk  about  both  Important  and  Oral
Health matters. From the figure above, we can clearly see the dependence struc-
ture  between  egos  and  alters,  and  the  purpose  of  this  research  is  to  analyze  the
interaction between egos and alters. We achieve this goal by applying the network
of        egos  and  the  attribute  of  alters  to  the  Joint  Latent  Space  Model.  Note  that
the network data is from egos and the item response data is from alters. In other
words, there should be a slight modification of the model stated from Chapter 3.

16


4.3     Model

We  apply  Joint  Latent  Space  Model  to  model  the  dependence  structure  of  egos’
network  and  the  dependence  structure  of  alters’  bipartite  network  simultane-
ously.  Instead  of  using  alter’s  latent  position  when  modeling  Latent  Space  Item
Response  Model,  we  use  ego’s  latent  position,  that  the  alter  corresponds  with,
so  that  we  can  reflect  egos’  network  structure  onto  alters’  item  responses.  By
modeling egos’ network and alters’ bipartite network that is a↵ected by egos’ la-
tent position, we can visualize egos’ latent position and latent positions of alters’
items  in  one  latent  space.

Likelihood

The  likelihood  of  Joint  Latent  Space  Model  of  Latent  Space  Model  for  egos’
network  and  Latent  Space  Item  Response  Model  for  alters’  attributes  are  as
follows:

P (Y, X | Z, W, ↵, ✓, β)


327

k=1

327

l=1,l   k

exp(↵—kzk—zlk)
1+exp(↵—kzk—zlk)

Yk,l                              1

1+exp(↵—kzk—zlk)

⌘1—Yk,l


Q1,017 Q9

✓  exp(✓j +βi—kzn

(j)

—wik)

♦Xj,i  ✓

♦1—Xj,i


⇥   j=1

i=1

1+exp(✓j +βi—kzn(j) —wik)

1+exp(✓j +βi—kzn(j) —wik)

(4.1)

where  Y  is  network  data  of  egos,  X  is  Item  Response  data  of  alters,  Z  is  latent
position  of  egos,  and  W  is  latent  position  of  alters’  attributes,  ✓j  is  the  main
e↵ect  of  a  alters  j,  and  βi is  the  main  e↵ect  of  an  item  i.  zn(j)   in  the  third  
line
of  Equation  4.1  represents  the  latent  position  of  ego  where  n(j)  implies  the  ego
index  of  the  alter  j.

17


The log-odds of the probability that the alter j responses to the item i positively
(Xj,i  =  1)  when  ego  k and  ego  l have  relation  (Yk,l  =  1)  can  be  expressed  as


follows:

logit(P (Yk,l = 1, Xj,i = 1|↵, ✓j, βi, zk, zl, zn(j) , wi))

= ↵ + ✓j + βi—k zk — zl k— k zn(j)  — wi k

(4.2)

Implementation

Estimation  procedure  is  implemented  as  stated  from  Chapter  3.2.  We  used  2.5
respectively  for  the  standard  deviation  of  ↵ and  β,  and  used  0.001  respectively
for  the  shape  parameter  a and  and  scale  parameter  b in  the  Inverse-Gamma
distribution  which  is  used  to  generate  the  standard  deviation  of  ✓  (σ² ).  The
MCMC  sampling  included  30,000  iterations  with  the  first  half  15,000  iterations
discarded  as  a  burn-in  period.  The  thinning  interval  was  10,  which  resulted  in
1,5000  samples.  The  acceptance  rate  for  each  parameter  showed  between  0.2
and  0.5  and  the  trace  plot  seemed  appropriate,  which  can  be  thought  of  as  the
algorithm  converged  well.

4.4     Result

Figure  4.2  shows  the  latent  positions  of  egos  and  alters’  attributes,  where  egos
are  represented  in  black  dots,  and  alters’  attributes  are  represented  in  red  dots
with their names. From the Figure 4.2a, we can see that the itens can be roughly
clustered  into  four  groups:  (i)  3  items  in  first  quadrant  (ARprobsdum,  ARtalka-
cdum,  ARhassleissdum),  (ii)  2  items  in  second  quadrant  (ARknowl,  Aeducfive),

(iii) 2 items in third quadrant (ARhlthinsdum, ARdentinsdum, ARseedentdum),

18


(a)  original  latent  positions  of  egos  and  alters’  attributes

(b)  latent  positions  of  egos  and  alters’  attributes  after  rotation

Figure  4.2:  Latent  Positions  of  Egos  and  Alters’  Attributes

19


(iv) 1 item in fourth quadrant (ARclosedum). Group1 is grouped with the items
that represents if the alter has dental problems and discuss related matters with
egos. Group2 is grouped with the items that represents if the alter has high edu-
cation and have certain amount of dental knowledge. Group3 is grouped with the
items  that  represents  if  the  alter  has  health  related  insurances  and  visit  dental
services  often.  It  is  notable  that  the  latent  position  of  Group1  and  Group3  lies
in    the  opposite  direction  on  the  latent  space,  which  seems  plausible  as  having
dental problems (Group1) and going to doctors (Group3) can be thought to have
a conflicting  tendencies.

As stated above, distances between a set of points in Euclidean space are
invariant  under  rotation,  therefore  x-axis  and  y-axis  in  the  Figure  4.2a  doesn’t
signify anything. In order to add the meaning of the axis to the latent space, we
proceeded  principal  component  analysis  using  oblique  rotation  (Jennrich,  2002)
in  the  R  package  psych  (Revelle,  2021).  Oblique  rotation  is  a  way  of  rotating
principal  scores  which  lets  factors  to  be  correlated  to  each  other  and  makes  the
interpretation easy. The result of the latent positions of egos and alters’ attributes
after  oblique  rotation  is  shown  in  the  Figure  4.2b.  6  items  from  the  previous
Group1  and  Group3  is  now  close  to  the  x-axis,  and  3  items  from  the  previous
Group2 and Group4 is close to the y-axis. Considering the items of each axis, we
can name the first factor in x-axis as ‘oral health of alters’ where the right side of
the axis tends to have oral health problems and discuss with egos, whereas the left
side  of  the  axis  tends  to  have  health  insurance  and  visit  doctor’s  office  often.  In
the same way, we can name the second factor in y-axis as ‘personal information of

20


alters’ where the upper side tends to have high education and have knowledge on
oral matters whereas the lower side tends to be close to egos. Then the egos in the
first quadrant, which is 74 of them among 327, can be thought of as whose alters
are  knowledgeable  in  oral  matters  but  also  has  frequent  oral  problems.  Egos  in
the second quadrant, which is 90 of them, can be thought of as whose alters have
high education and also has health insurance. Egos in the third quadrant, which
is  81  of  them,  can  be  thought  of  as  whose  alters  visit  dentist  often  and  close  to
egos. Lastly, egos in the fourth quadrant, which is 82 of them, can be thought of
as  whom  alters  have  close  relationship  with  and  talk  about  dental  related  issues
often  with.

21


Chapter 5

Conclusion

In this paper, we propose Joint Latent Space Model, which is Latent Space Item
Response  Model  combined  with  Latent  Space  Model.  Latent  Space  Model  and
Latent  Space  Item  Response  Model  can  both  model  the  dependence  structure
of  the  network  data  and  the  bipartite  network  data  respectively.  However,  both
models are not sufficient to model the dependence structure of the network data
and the bipartite network data simultaneously where they share the same respon-
dents. In this sense, Joint Latent Space Model is useful to capture the dependence
structure  of  both  network  data  and  item  response  data  at  the  same  time.  It  can
be   also applied to the Item Response data of alters instead of egos as implemented
in the Tala Survey study. By reflecting egos’ network onto alters’ item responses,
it  is  possible  to  see  the  interaction  between  egos  and  alters  on  the  same  latent
space.  In  this  research,  we  used  only  one  Item  Response  data  of  alters  but  the
model  can  be  further  extended  adding  one  more  Item  Response  data  of  egos,
which then becomes the joint model of one Latent Space Model with two Latent
Space  Item  Response  Models.

22


References

CDC   (2019).       Oral   health   surveillance   report:   Trends   in   dental   caries
and  sealants,  tooth  retention,  and  edentulism,  united  states,  1999–2004  to
2011–2016.

Cohen  LA,  Bonito  AJ,  A.  D.  e.  a.  (2009).  Toothache  pain:  behavioral  impact
and  self-care  strategies.  Special Care in Dentistry.

Dye  B,  Thornton-Evans  G,  L.  X.  I.  T.  (2015).  Dental  caries  and  tooth  loss  in
adults  in  the  united  states,  2011-2012.  National Center for Health Statistics.

Eke  PI,  Dye  BA,  W.  L.  e.  a.  (2015).  Update  on  prevalence  of  periodontitis  in
adults  in  the  united  states:  Nhanes  2009 to 2012.  Journal of Periodontology.

Gower, J. C. (1975). Generalized procrustes analysis. Psychometrika, 40(1):33–
51.

Ho↵,  P.  D.,  Raftery,  A.  E.,  and  Handcock,  M.  S.  (2002).   Latent  space  ap-
proaches to social network analysis.  Journal of the American Statistical Asso-
ciation,  97(460):1090–1098.

Jennrich,  R.  I.  (2002).   A  simple  general  method  for  oblique  rotation.   Psy-
chometrika,  67(1):7–19.

23


Jeon, M., Jin, I. H., Schweinberger, M., and Baugh, S. (2021).  Mapping unob-
served item–respondent interactions: A latent space item response model with
interaction  map.  Psychometrika,  86(2):378–403.

Maupome  G,  McConnell  WR,  P.  B.  (2016).   Dental  problems  and  familismo:
social  network  discussion  of  oral  health  issues  among adults  of  mexican  origin
living in  the  midwest  united  states.  Community Dent Health.

Maupome  G,  Aguirre-Zero  O,  W.  C.  (2015).  Qualitative  description  of  dental
hygiene  practices  within  oral  health  and  dental  care  perspectives  of  mexican-
american  adults  and  teenagers.  Journal of Public Health Dentistry.

McAdoo,  H.  (1999).  Family  ethnicity:  strength  in  diversity.

Pullen E, Perry BL, M. G. (2018).  “does this look infected to you?” social net-
work  predictors  of  dental  help-seeking  among  mexican  immigrants.  J Immigr
Minor Health.

Rasch,  G.  (1961).   On  general  laws  and  the  meaning  of  measurement  in  psy-
chology.

Revelle,  W.  (2021).   psych:  Procedures  for  Psychological,  Psychometric,  and
Personality Research.  Northwestern  University,  Evanston,  Illinois.  R  package
version  2.1.9.

Stein,  G.  L.,  Gonzalez,  L.  M.,  Cupito,  A.  M.,  Kiang,  L.,  and  Supple,  A.  J.
(2015). The protective role of familism in the lives of latino adolescents. Journal
of Family Issues,  36(10):1255–1273.

24


WALL,  T.  P.  and  BROWN,  L.  J.  (2004).   Dental  visits  among  hispanics  in
the  united  states,  1999.    The  Journal  of  the  American  Dental  Association,
135(7):1011–1017.

Wasserman,  S.  and  Faust,  K.  (1994).   Social network analysis: Methods and
applications,  volume  8.  Cambridge  university  press.

25


m8  ]

∞i †¨ı⌅® ¸ alter‰X ç1D t©\

egoX $∏Ãl M 

Ñ¿–

µƒpt0¨t∏§Y¸

8 YP |⇠ Y–

¯      lî ∞i †¨ı⌅® D ¨©XÏ U‹T tMê‰X $∏Ãl@ XD ¡‹

X ½ƒ| ®x¡X‡ê \‰. ¯m ‹›X |Ùƒ– Dt U‹T  tMê‰@ XÃ

⌘¸1t ♘¥¿p, D⇠ x X¸ XÃ ⌧D§– ⌘¸Xî p ¡˘\ ¥$¿tà 

‰.  0|⌧  U‹T  tMê‰X ¨å   $∏Ãl   l »X ½( XÃt©– ¥♘

 •D ¯Xî¿  EXî Ét ⌘îX‰. ¯      lî êDX $∏Ãl ®x¸ 8m

⇠Q ®x, ¿êX ç1– ½\ 8m ⇠Q ®xD ∞i\ †¨ı⌅® D ⌧⌧X 

‰. ∞i †¨ı⌅® @ 8m ⇠Q ®x– êDX $∏Ãl| ⇠ h<\h êD‰

¨tX ½ƒ  ⇠ ⌧ êD@ ¿êX ç1D XòX †¨ı⌅–⌧ ½0` ⇠ à‰.

U‹T–⌧ ¯m ⌘⌧Ä\ t¸\ U‹T tMê‰X pt0x Tala Survey Study

| ¨©XÏ U‹T tMêx êD 327ÖX $∏Ãl@ 8m ⇠Q¸ ¿ê 1,017ÖX

ç1 pt0| ∞i †¨ı⌅® –  ©XÏ êD@ ¿êX ¡8ë©D ¥¥Ù‡

ê \‰.

26

