#

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
| https://docs.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax |
| http://docs.mathjax.org/en/latest/input/tex/macros/index.html |
| [T-test 와 F-test?](https://m.cafe.daum.net/DOE/6xWC/20) |
| [GitHub.io 페이지 만들기](https://dnight.tistory.com/entry/GitHubio-%ED%8E%98%EC%9D%B4%EC%A7%80-%EB%A7%8C%EB%93%A4%EA%B8%B0) |

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