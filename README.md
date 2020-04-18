# Decision-Tree
이 레포지터리에서 설명하는 내용은 파이썬 머신러닝 완벽 가이드 책에 나오는 내용을 정리한 것임
### Decision Tree 란?
&nbsp;결정 트리(Decision Tree)란 데이터에 있는 규칙을 학습을 통해 자동으로 찾아내 트리 기반의 분류 규칙을 만드는 것이다.
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700926574383464488/Decision_Tree.png" title="Decision Tree structure" alt="Decision Tree structure"></img><br>
&nbsp;위의 그림은 결정 트리의 구조를 간략하게 나타낸 것이다. 규칙 노드(Decision Node)로 표시된 노드는 규칙 조건이 되는 것이고, 리프 노드(Leaf Node)로 표시된 노드는 결정된 클래스 값이다. 그리고 새로운 규칙 조건마다 서브 트리(Sub Tree)가 생성된다. 데이터 세트에 피처가 있고 이러한 피처가 결합해 규칙 조건을 만들 때마다 규칙 노드가 만들어진다. 하지만 규칙이 많을수록, 즉 트리의 깊이가 깊어질수록 트리가 복잡해져 과적합으로 이어지기 쉽다. 가능한 한 적은 규칙 노드로 높은 예측 정확도를 가지려면 데이터를 분류할 때 최대한 많은 데이터 세트가 해당 분류에 속할 수 있도록 규칙 노드의 규칙이 정해져야 한다.
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700932957514367067/Uniformity.png" title="Data Uniformity" alt="Data Uniformity"></img> <br>
&nbsp;위 그림에서 데이터가 균일한 순서로 나타내면 C, B, A 순이다. 데이터를 분류할 때 최대한 많은 데이터 세트가 해당 분류에 속하기 위해서는 규칙 노드를 정할 때 데이터가 균일하도록 정해줘야 한다. 이러한 정보의 균일도를 측정하는 대표적인 방법은 엔트로피를 이용한 정보 이득 지수와 지니 계수가 있다. 정보 이득 지수는 엔트로피에서 1을 뺀 값으로 높을수록 정보의 균일도가 높다. 그리고 지니 계수는 원래 경제학에서 불평등 지수를 나타낼 때 사용하는 계수로 작을수록 균일도가 높다. 사이킷런에서는 기본으로 지니 계수를 사용한다.
### Decision Tree의 특징
#### Decision Tree의 장점
- 결정 트리는 정보의 균일도라는 룰을 기반으로 하고 있어 알고리즘이 쉽고 직관적이다. 때문에 시각화할 수 있다.
- 정보의 균일도만 신경 쓰면 되므로 특별한 경우를 제외하고 각 피처의 스케일링과 정규화 같은 전처리 작업이 필요 없다.
#### Decision Tree의 단점
- 과적합으로 알고리즘 성능이 떨어진다. 이를 극복하기 위해 트리의 크기를 사전에 제한하는 튜닝이 필요하다.
### Decision Tree의 파라미터
#### min_samples_split 
- 노드를 분할하기 위한 최소한의 샘플 데이터 수로 과적합을 제어하는 데 사용됨
- 디폴트는 2이고 작게 설정할수록 분할되는 노드가 많아져서 과적합 가능성 증가
- 과적합을 제어. 1로 설정할 경우 분할되는 노드가 많아져서 과적합 가능성 증가
#### min_sample_leaf
- 말단 노드(Leaf)가 되기 위한 최소한의 샘플 데이터 수
- Min_samples_split과 유사하게 과적합 제어 용도, 그러나 비대칭적(imbalanced) 데이터의 경우 특정 클래스의 데이터가 극도로 작을 수 있으므로 이 경우는 작게 설정 필요
#### max_features
- 최적의 분할을 위해 고려할 최대 피처 개수. 디폴트는 None으로 데이터 세트의 모든 피처를 사용해 분할 수행
- int 형으로 지정하면 대상 피처의 개수. float형으로 지정하면 전체 피처 중 대상 피처의 퍼센트임
- 'sqrt'는 전체 피처 중 sqrt(전체 피처 개수)
- 'auto'로 지정하면 sqrt와 동일
- 'log'는 전체 피처 중 log2(전체 피처 개수) 선정
- 'None'은 전체 피처 선정
#### max_depth
- 트리의 최대 깊이를 규정
- 디폴트는 None. None으로 설정하면 완벽하게 클래스 결정 값이 될 때까지 깊이를 계속 키우며 분할하거나 노드를 가지는 데이터 개수가 min_samples_split보다 작아질 때까지 계속 깊이를 증가시킴
- 깊이가 깊어지면 min_samples_split 설정대로 최대 분할하여 과적합할 수 있으므로 적절한 값으로 제어 필요
#### max_leaf_nodes
- 말단 노드(Leaf)의 최대 개수
### Decision Tree 시각화
다음 나오는 이미지들은 모두 붓꽃 데이터셋으로 시각화 했다.<br>
시각화 한 코드는 이 레퍼지토리에 있는 Decision Tree.ipynb을 참고하면 된다.<br>
다음에 나올 그래프를 보는 방법은 다음과 같다.
- petal length(cm) <= 2.45와 같은 피처의 조건이 있는 것은 자식 노드를 만들기 위한 규칙조건이다. 이 조건이 없으면 리프 노드이다.
- gini는 다음의 value=[]로 주어진 데이터 분포에서의 지니 계수이다. (지니계수가 낮을수록 데이터의 균일도가 높은 것으로 해석)
- value = []는 클래스 값 기반의 데이터 건수이다. 붓꽃 데이터 세트는 클래스 값으로 0, 1, 2를 가지고 있으며, 0 : Setosa, 1 : Versicolor, 2 : Virginica 품종을 가리킨다. 만일 value=[41, 40, 39]라면 클래스 값의 순서로 Setosa 41개, Vesicolor 40개, Virginica 39개로 데이터가 구성되어 있다는 것임
#### Default Params
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700992633140543538/unknown.png" title="Decision Tree Default Params" alt="Decision Tree Default Params" width="70%"></img><br>
위의 그래프는 모든 하이퍼 파라미터의 값을 디폴트로 둔 그래프이다.
#### max_depth=3
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700993147496431636/unknown.png" title="Decision Tree max_depth=3" alt="Decision Tree max_depth=3" width="70%"></img><br>
위의 그래프는 max_depth를 3으로 설정한 경우이다. depth가 3이 됐으므로 분할을 멈춘 것을 볼 수 있다. max_depth에 따라 트리의 깊이가 줄어들면서 더 간단한 결정트리가 된다.
#### min_samples_split=4
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700993318783549460/unknown.png" title="Decision Tree min_samples_split=4" alt="Decision Tree min_samples_split=4" width="70%"></img><br>
위의 그래프는 min_samples_split을 4로 설정한 경우이다. 이 경우 맨 하단 가운데 두 개의 리프 노드를 보면 서로 상이한 클래스 값이 있어도 샘플 수가 4개 미만인 3개 이므로 더이상 분할하지 않고 리프 노드가 됐음을 볼 수 있다. 따라서 자연스럽게 트리 깊이도 줄었고 더욱 간결한 결정 트리가 만들어졌다.
#### min_samples_leaf=4
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700992633140543538/unknown.png" title="Decision Tree min_samples_leaf=4" alt="Decision Tree min_samples_leaf=4" width="70%"></img><br>
위의 그래프는 min_samples_split을 4로 설정한 경우이다. 이 경우 모든 리프 노드를 살펴보면 샘플 수가 4 이상이다. 이 경우 샘플이 4 이하이면 리프 노드가 되기 때문에 지니 계수 값이 크더라도 샘플이 4인 조건으로 규칙 변경을 선호하게 되어 자연스럽게 브랜치 노드가 줄어들고 결정 트리가 더 간결하게 만들어진다.
### Decision Tree의 피처 중요도
&nbsp;결정 트리는 균일도에 기반해 어떠한 속성을 규칙 조건으로 선택하느냐가 중요하다. 중요한 몇 개의 피처가 명확한 규칙 노드를 만드는 데 기여하며, 모델을 좀 더 간결하고 이상치(Outlier)에 강한 모델을 만들 수 있기 때문이다. 사이킷런은 피처 중요도를 DecisionTreeClassifier 객체의 feature_importances_ 속성으로 제공한다.
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700990659506601985/TttUYcZ1dGHGtJyc50AGniQwZ9Hxy9YwWPynwuTJHXPy5iSpO4ZdpKk7hl2kqTuGXaSpO4ZdpKk7hl2kqTuGXaSpO79Pw4R0AOZ3.png" title="feature importance" alt="feature importance"></img><br>
위의 막대그래프를 보면 petal_length가 가장 중요도가 높은 피처임을 알 수 있다. 일반적으로 다른 알고리즘은 블랙박스라고 불리듯 알고리즘의 내부 동작 원리가 복잡하지만 결정 트리는 직관적이기 때문에 이러한 요소들을 시각적으로 표현할 수 있다.
### Decision Tree의 과적합
사이킷런은 분류를 위한 테스트용 데이터를 쉽게 만들 수 있도록 make_classification() 함수를 제공한다. 이 함수로 2개의 피처가 3가지 유형의 클래스 값을 가지는 데이터셋을 만들고 시각화해 보면 다음과 같은 그래프가 만들어진다.
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700990698584932422/AJ1uTWvQkpTIAAAAAElFTkSuQmCC.png" title="made dataset" alt="made dataset"></img><br>
이렇게 생성된 데이터셋을 아무런 하이퍼 파라미터도 건드리지 않은 결정 트리로 학습 시키면 다음과 같은 영역으로 나뉜다.<img src="https://cdn.discordapp.com/attachments/700926550945693846/700990721359872424/gEAwD9ApwsAoCCELgCA0AghC6AAAKQugCACgIoQsAoCCELgCAgv4A1Xv3t15qcE0AAAAASUVORK5CYII.png" title="default decision tree boundary" alt="default decision tree boundary"></img><br>
리프 노드 안에 데이터가 모두 균일하거나 하나만 존재해야 하는 엄격함 분할 기준으로 인해 결정 기준 경계가 많아지고 복잡해졌다. 이렇게 복잡한 모델은 학습 데이터 세트의 특성과 약간만 다른 형태의 데이터 세트를 예측하면 예측 정확도가 떨어지게 된다.<br>
&nbsp;다음으로 min_samples_leaf=6으로 하이퍼 파라미터를 조정한 후 결정 트리를 학습 시키면 다음과 같은 영역으로 나뉜다.
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700990738451791892/sgYEREZipUuEZGJGLpERCZi6BIRmYihS0RkIoYuEZGJGLpERCb6HSuk1aiIuxhpAAAAAElFTkSu0AQmCC.png" title="min_samples_leaf=6 decision tree boundary" alt="min_samples_leaf=6 decision tree boundary"></img><br>
위의 그림을 살펴보면 이상치에 크게 반응하지 않으면서 좀 더 일반화된 분류 규칙에 따라 분류됐음을 알 수 있다.
