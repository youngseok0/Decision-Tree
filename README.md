# Decision-Tree
여기에 적혀 있는 내용들은 모두 파이썬 머신러닝 완벽 가이드 책에서 가져온 내용들임
### Decision Tree 란?
&nbsp;결정트리(Decision Tree)란 데이터에 있는 규칙을 학습을 통해 자동으로 찾아내 트리 기반의 분류 규칙을 만드는 것이다.
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700926574383464488/Decision_Tree.png" title="Decision Tree structure" alt="Decision Tree structure"></img><br>
&nbsp;위의 그림은 결정 트리의 구조를 간략하게 나타낸 것이다. 규칙 노드(Decision Node)로 표시된 노드는 규칙 조건이 되는 것이고, 리프 노드(Leaf Node)로 표시된 노드는 결정된 클래스 값이다. 그리고 새로운 규칙 조건마다 서브 트리(Sub Tree)가 생성된다. 데이터 세트에 피처가 있고 이러한 피처가 결합해 규칙 조건을 만들 때마다 규칙 노드가 만들어진다. 하지만 규칙이 많을수록, 즉 트리의 깊이가 깊어질수록 트리가 복잡해져 과적합으로 이어지기 쉽다. 가능한 한 적은 규칙 노드로 높은 예측 정확도를 가지려면 데이터를 분류할 때 최대한 많은 데이터 세트가 해당 분류에 속할 수 있도록 규칙 노드의 규칙이 정해져야 한다.
<img src="https://cdn.discordapp.com/attachments/700926550945693846/700932957514367067/Uniformity.png" title="Data Uniformity" alt="Data Uniformity"></img> <br>
&nbsp;위 그림에서 데이터가 균일한 순서로 나타내면 C, B, A 순이다. 아까 말했듯 최대한 많은 데이터 세트가 해당 분류
