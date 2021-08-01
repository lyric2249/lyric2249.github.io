``` python
numpy.empty

library(ggplot2)
colors <- c("Sepal Width" = "blue", "Petal Length" = "red", "Petal Width" = "orange")

ggplot(iris, aes(x = Sepal.Length)) +
    geom_line(aes(y = Sepal.Width, color = "Sepal Width"), size = 1.5) +
    geom_line(aes(y = Petal.Length, color = "Petal Length"), size = 1.5) +
    geom_line(aes(y = Petal.Width, color = "Petal Width"), size = 1.5) +
    labs(x = "Year",
         y = "(%)",
         color = "Legend") +
    scale_color_manual(values = colors)






```


```r

library(dplyr)
mtcars %>% 
    group_by(cyl, gear) %>%
    summarise_all("mean")

mtcars %>% 
group_by(cyl, gear) %>%
summarise(across(everything(), mean))

mtcars %>%
     mutate(mpg=replace(mpg, cyl==4, NA)) %>%
     as.data.frame()

You can use the unite function from tidyr

require(tidyverse)

df %>% 
  unite(round_experiment, c("round", "experiment"))

Note that %in% returns a logical vector of TRUE and FALSE. To negate it, you can use ! in front of the logical statement:

You could use colnames<- or setNames (thanks to @David Arenburg)

group_by(mtcars, cyl) %>%
  summarise(mean(disp), mean(hp)) %>%
  `colnames<-`(c("cyl", "disp_mean", "hp_mean"))
  
 Or pick an Alias (set_colnames) from magrittr:

library(magrittr)
group_by(mtcars, cyl) %>%
  summarise(mean(disp), mean(hp)) %>%
  set_colnames(c("cyl", "disp_mean", "hp_mean"))

y ~ lm(x:z)

data[rowSums(is.na(data)) > 0, ]    

statsmodels.stats.multivariate.test_cov_oneway¶

library("FactoMineR")
data(decathlon2)
PCA(X, scale.unit = TRUE, ncp = 5, graph = TRUE)

Pandas: Apply a function to single or selected columns or rows in Dataframe

drop_na(data, ...)




Python list | index()
Difficulty Level : Basic
Last Updated : 08 Sep, 2020
index() is an inbuilt function in Python, which searches for a given element from the start of the list and returns the lowest index where the element appears. 
Syntax : 
 

list_name.index(element, start, end)


got multiple values for argumentPermalink
사소한 오류이기는 한데, 정리합니다.
아래 코드에서 보는 것과 같이, func에 변수를 함께 넘길 경우에는
해당 함수가 선언되었을 때의 변수 순서에 맞춰서 넘기거나
아니면 위치와 상관없이, 변수 명을 분명하게 작성해서 넘겨야 합니다.
def temp_func(a=1, b=3):
    print(a, b)
temp_func(1, 3) #OK 
temp_func(b=5, a=3)#OK 
temp_func(1, a=3) #NOT OK
세번째처럼 그 순서를 마음대로 할 경우에는 아래와 같은 오류가 뜹니다.
TypeError: temp_func() got multiple values for argument 'a'





```
sqlite3.InterfaceError: Error binding parameter 16 - probably unsupported type.
pythone error 2017. 2. 10. 11:56
sqlite execute에서 인자의 네임이 잘못되었을 때



출처: https://fold22.tistory.com/17 [나의 흔적]

https://twitter.com/cand1e/status/1400150211490508800
그라뉴
선데이버거클럽


<개인공부>/[C++]

[C++] 가상함수와 순수가상함수의 차이(virtual, pure virtual)에 대해서


출처: https://blockdmask.tistory.com/277 [개발자 지망생]


antithetic, strata, 

# JAVA
dedicated

Reserved for a specific use. In communications, a dedicated channel is a line reserved exclusively for one type of communication. This is the same as a leased line or private line.

쉽게 말해서 '전용'으로 해석하면 된다. 한가지 목적으로 쓰이는 것을 말한다.

ex) dedicated tablespace: 데이터 이관시에만 사용될 이관 전용 테이블 스페이스

 

deprecated

Used typically in reference to a computer language to mean a command or statement in the language that is going to be made invalid or obsolete in future versions.

자바언어에서 자주 쓰이는 용어로 명령 혹은 문장이 나중에는 쓰이지 않게 될 것이라는 뜻이다.

쉽게 말해 다른 것으로 대체되었거나 될 수 있으니 주의해서 사용하라는 말이다.

ex) Tar.TRUNCATE is deprecated and is replaced with Tar.TarLongFileMode.

Tar.TRUNCATE 가 Tar.TarLongFileMode 로 대체됨


# arbitrary

[equation](http://www.sciweavers.org/tex2img.php?eq=1%2Bsin%28mc%5E2%29&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=)

https://seoncheolpark.github.io/book/_book/

https://losskatsu.github.io/statistics/

http://jaejunyoo.blogspot.com/2018/08/what-is-relationship-between-orthogonal.html

하우스도르프 차원

beware of
pneumonia
importance weight
fraying omnipotence


예전에 애니 관계 회사에서 강연할 때 'a와 the의 차이점을 알려주세요' 라는 질문을 받고 'a는 자쿠에게 쓰고, the는 샤아 자쿠에게 씁니다' 라고 했던 설명은 내가 한 거지만 회심의 역작이라고 지금도 생각한다. 불특정 아무 자쿠 a zaku, 특정한 그 빨간 자쿠 the red jaku.

혹여나 MST를 모르시는 분이 읽으실까봐 'arbitrary'를 설명할 때 그것을 예시로 들고 싶지는 않았습니다. 그런데, 딱히 그것 말고는 이렇다 할 좋은 예시가 떠오르지가 않더군요. 혹시 MST를 잘 모르신다면 송구할 따름입니다. 기회가 되면 학부 자료구조, 알고리즘 쪽으로도 포스팅을 해보도록 하겠습니다.

만일 'random' 절을 다 읽어보셨다면 아마도 다음과 같은 질문이 자연스럽게(?) 떠오르실 겁니다. 과연 2를 기대하는 알고리즘보다 더 좋은 알고리즘을 구현할 수 있을까요? 우리가 조절할 수 있는 것은 각각의 카드를 뽑는 확률 분포가 되겠죠. 예를 들면 첫 번째, 두 번째, 세 번째를 각각 20%, 40%, 40%로 뽑는다든지 말이죠.

어느 정도 예상하셨겠지만, 더 이상 좋아질 수 없습니다. 이를 어떻게 증명할 수 있을까요? 바로 야오의 법칙(Yao's principle)을 통해서 보일 수 있습니다. 이 법칙은 randomized algorithm의 성능을 분석할 때 가장 중요한 법칙 중 하나입니다. 다음 포스트에서는 이 법칙에 대해서 알아보도록 하죠.

# p-value

근본적으로 주어진 사상(sample)이 특정 전제조건에서 얼마나 그럴듯하게 발생할 수 있는가에 대한 이야기. $$H_0$$는 검증이 간단한 쪽을 $$H_0$$로 삼는다. 같다는 조건은 다르다는 조건에 비해 간단하므로 보통 같다는 조건이 $$H_0$$에 오게 된다. $$H_0$$이 전제되었을 때 우리가 관측한 사상이 발생할 확률(p-value)을 체크하여, 해당 확률이 작으면 주어진 사상 뒤에 있는 전제($$H_0$$ or $$H_1$$) 중 우리가 가정하였던 전제($$H_0$$)에서는 우리가 관측한 결과값이 등장할 확률이 적으므로 $$H_0$$를 전제라고 생각하는건 합리적이지 않다. 따라서 p-value가 작으면 $$H_0$$를 기각한다.

| $$N$$ |
| --- |
| $$t$$ |
| $$\chi^2$$ |
| $$F$$ |

가장 이상적인건 모집단의 패러미터를 전부 파악하는 것이지만 모집단 전체를 조사하는 건 불가능하므로 이는 불가능. 샘플링 후 샘플을 조사해서 모집단의 특성을 파악한다. 이때 샘플 = 주어진 사상. 이러한 샘플들을 표상할 수 있는 특성을 **test statistics**로 갈무리(표현)한 후, 이 test stat이 획득 과정에서 따라야 하는 분포에서의 **rejection region**에 들어간다면 생각했던 조건($$H_0$$)을 이를 기각한다. rejection region은 극단적인, 즉 $$H_0$$ 하에서는 발생하지 않는 건 아니지만 상식적으로 $$H_0$$ 하에서 주어진 사상이 발생했다고 생각하기에는 확률이 너무 낮은 녀석. 즉 test stat이라는 것은 결국 주어진 사상을 드러내는 통계량의, 분포에서의 x축 위치를 구하는 것과 동치된다.




# jupyter-lab

```
{
"shortcuts": [
        {
            "command": "notebook:hide-cell-outputs",
            "keys": [
                "H"
            ],
            "selector": ".jp-Notebook:focus"
        },
        {
            "command": "notebook:show-cell-outputs",
            "keys": [
                "Shift H"
            ],
            "selector": ".jp-Notebook:focus"
        }
    ]
}
```


# 210419


two over three

diffuse <br/>
Aforethought 뜻<br/>
sarcasm 뜻<br/>
american way	<br/>
영어 savant 뜻<br/>

|e.g. |The abbreviation "e.g." is from the Latin exempli gratia and means, literally, "for example." Periods come after each letter and a comma normally follows unless the example is a single word and no pause is natural|
|i.e. | The abbreviation "i.e." is from the Latin id est, meaning "that is." Loosely, "i.e." is used to mean "therefore" or "in other words." Periods come after each letter and a comma normally follows, depending on whether the wording following the abbreviation dictates a natural pause|
|et al. | The phrase "et al."—from the Latin et alii, which literally means "and others"—must always be typed with a space between the two words and with a period after the "l" (since the "al." is an abbreviation). A comma does not follow the abbreviation unless the sentence’s grammar requires it. Some journals italicize the phrase because it comes from the Latin, but most do not.|
||Never begin a sentence with any of these three abbreviations; if you want to begin a sentence with "for example" or "therefore," always write the words out.|



> 의심하는 것은 유쾌한 일이 아니다.<br>
> 하지만 확신하는 것은 어리석은 일이다.<br>
> <br>
> ─ 『열두 발자국』, 정재승

> "The fundamental cause of the trouble is that in the modern world the stupid are cocksure while the intelligent are full of doubt."<br>
><br>
> ─ Bertrand Russell


|ahead | 내꺼, 쌓임, 위에꺼에 없음 | 합쳐지면 부모가 받는 충격 |
|behind | 내꺼아님, 쌓임, 위에꺼에 있음 | 부모가 지금까지 받아온 충격 |

site:math.stackexchance.com/

site:stats.stackexchange.com/

```
Convert from list to numeric

as.numeric(unlist(x))
```

```
ipython 파일인 ipynb을 py로 바꾸는 법

jupyter nbconvert --to script [filename].ipynb 
```


시퀀스 $$\textbf x_n$$ 이 확률수렴하면 이는 확률에 bounded.

확률수렴을 가정. given 임의의 $$\epsilon$$ and $$\eta >0$$,

empty set $$\emptyset$$


```
나꼼수 자체가 이명박한테 아나테마이긴 한데 주진우가 대표성이 제일 큰듯 나꼼수 터지고 나서도 계속 물어뜯고 다녔고

/K C:\Ruby27-x64\bin\setrbvars.cmd 

"is a real-valued random variable with an absolutely continuous"

잉크 CL-80
```


[Split expressions with parentheses in align environment](https://tex.stackexchange.com/questions/89615/split-expressions-with-parentheses-in-align-environment)
| [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/) |
| [](https://ko.overleaf.com/learn/latex/Brackets_and_Parentheses) |
| [https://docs.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax]() |

| [https://www.overleaf.com/learn/latex/bold,_italics_and_underlining](https://www.overleaf.com/learn/latex/bold,_italics_and_underlining) |
| https://angeloyeo.github.io/2020/09/14/normal_distribution_derivation.html#fnref:1 |
| https://www.overleaf.com/learn/latex/Integrals,_sums_and_limits |
| http://tancro.e-central.tv/grandmaster/textex/coexist-character.html |
| https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference |
| https://theqoo.net/square/479075602 |
| https://angeloyeo.github.io/2019/07/15/Matrix_as_Linear_Transformation.html |
| https://angeloyeo.github.io/2020/09/17/MCMC.html |
| [Github Pages, Basic Writing & Formatting Syntax](https://docs.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax) |
| [MathJax, Supported TeX/LaTeX commands] (http://docs.mathjax.org/en/latest/input/tex/macros/index.html) |
| [T-test 와 F-test?](https://m.cafe.daum.net/DOE/6xWC/20) |
| [GitHub.io 페이지 만들기](https://dnight.tistory.com/entry/GitHubio-%ED%8E%98%EC%9D%B4%EC%A7%80-%EB%A7%8C%EB%93%A4%EA%B8%B0) |
| [RStudioでRStanを実行する際のTips](https://qiita.com/kazutan/items/6cc162bc3c4b1b9062f2) |

```Note
"consider the following hierarchical model," W, X, Y, Z

와이블 분포

can be exponential family with 1

Cov(x,y) can be written with conditional expectation
if there is function which is 1 in exponential family
is it able to T(x) become constant in exponential family

Joint moment generating function
```

| http://norman3.github.io/prml/ |
| https://roseline124.github.io/data-analytics/2019/03/30/ML-Deep-Delta.html |
| https://en.wikipedia.org/wiki/Proofs_of_convergence_of_random_variables#propB3 |
| https://hemos.tistory.com/43 |
| https://simcho999.blogspot.com/2021/02/financial-engineering-lindeberg-central.html |

| [product distribution of two uniform distribution, what about 3 or more](https://math.stackexchange.com/questions/659254/product-distribution-of-two-uniform-distribution-what-about-3-or-more) |
| [subtraction b/w X, Y ~exp](https://math.stackexchange.com/questions/115022/pdf-of-the-difference-of-two-exponentially-distributed-random-variables) |
| [Independence and Order-Statistics](https://math.stackexchange.com/questions/2068567/independence-and-order-statistics) |

| [수리통계학에서의 확률 유계, bounded in probability](https://freshrimpsushi.github.io/posts/bounded-in-probability/#%EC%A0%95%EC%9D%98-1) |
| [Lyapunov CLT](https://dawoum.ddns.net/wiki/Central_limit_theorem#Lyapunov_CLT) |
| [10.4 Big Op와 small op (big Op and small op)](https://seoncheolpark.github.io/book/_book/10-4-big-op-small-op-big-op-and-small-op.html) | 

| [미적분, 라이프니츠 규칙](https://kyoungseop.tistory.com/entry/%EB%AF%B8%EC%A0%81%EB%B6%84-%EB%9D%BC%EC%9D%B4%ED%94%84%EB%8B%88%EC%B8%A0-%EA%B7%9C%EC%B9%99-Leibniz-Rule) |
| [Continuous mapping theorem](https://en.wikipedia.org/wiki/Continuous_mapping_theorem) |
| [Big O_p and little o_p notation](https://statisticaloddsandends.wordpress.com/2019/05/22/big-o_p-and-little-o_p-notation/) |
| [Derivatives of Some Special Functions](http://people.reed.edu/~mayer/math111.html/header/node58.html) |
| [연속 사상 정리 증명, proof of continuous mapping theorem](https://freshrimpsushi.github.io/posts/proof-of-continuous-mapping-theorem/) |

| [Covariance of order statistics (uniform case)](https://math.stackexchange.com/questions/400677/covariance-of-order-statistics-uniform-case) |
| [Examples of sufficient statistics for non-exponential family distributions?](https://math.stackexchange.com/questions/149065/examples-of-sufficient-statistics-for-non-exponential-family-distributions) |
| [How to find the factorial of a fraction?](https://math.stackexchange.com/questions/396889/) |
| [Expected value and Lindeberg condition](https://math.stackexchange.com/questions/3772563/) |
| [Pdf of the difference of two exponentially distributed random variables](https://math.stackexchange.com/questions/115022/) |
| [product distribution of two uniform distribution, what about 3 or more](https://math.stackexchange.com/questions/659254) |
| [Sampling distribution of sample mean](https://math.stackexchange.com/questions/3934367/sampling-distribution-of-sample-mean) |
| [Sum of independent Gamma distributions is a Gamma distribution](https://math.stackexchange.com/questions/250059/) |
| [Proving that l2 is a vector space - how is the following true?](https://math.stackexchange.com/questions/1988969/) |
| [Find the pdf of Y = 1/X and compute E(Y)](https://math.stackexchange.com/questions/1728569/) |
| [Help me understand the quantile (inverse CDF) function](https://stats.stackexchange.com/questions/212813/) |
| [What is the rationale behind the exponential family of distributions?](https://stats.stackexchange.com/questions/326830/) |


# 210420

```
$$
\begin{flalign}
	&x=y&
\end{flalign}
$$
```

| Language    |   |  |  |
| ------- | -------- | ------- | ------- |
| Ruby | Bundler | Gem, Gemfile |  |
| Python | Pip | library | Anaconda |
| Git |  |  | Branch |

$$
\[
    X(m,n) = \left\{\begin{array}{@{}lr@{}}
	\multirow {2}{*}{x(n),} & \text{for }0\leq n\leq 1\\
                               & \text{or }0\leq n\leq 1\\
        x(n-1), & \text{for }0\leq n\leq 1\\
        x(n-1), & \text{for }0\leq n\leq 1
        \end{array}\right\} = xy
		\]
$$


| revise | modify | amend | alter | change | edit |
| --- | --- | --- | --- | --- | --- |
| 가다듬다 | 개정하다 | | | | |
| to change your opinions or plans, for example b/c of sth you have learned| to change sth slightly, especially in order to make it more suiable for a particular purpose (adapt)| | | | |
| (I can see I will have to revise my opinions of his abilities)| to make sth less extreme (adjust)| | | | |
|(The government may need to revise its policy in the light of this report) | make less severe or harsh or extreme| | | | |
| to change sth, such as a book or an estimate, in order to correct or improve it| "please modify this letter to mkae it more polite" | | | |
|(a revised edition of a textbook) | "he modified his views on same-gender marriage"| | | | |
|(I'll prepare a revised estimate for you.) | add a modifier to a constituent| | | | |
| (we may have to revise this figure upwards.)| cause to change; make different; cause a transformation| | | | |
| make revisions in "revise a thesis"| | | | | |
| revise or reorganize, especially for the purpose of updating and improving| | | | | |