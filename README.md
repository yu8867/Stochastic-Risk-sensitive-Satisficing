# バンディット問題
複数のアームと呼ばれる候補から最も良いものを逐次的に探す問題である。報酬を最大化するという点で、バンディット問題は強化学習のカテゴリに属する。バンディット問題の予測者は、限られた試行回数において得られる総報酬を最大化したい。 このとき、強化学習の普遍的なテーマである探索と活用のトレードオフが発生する。 短期的には、現時点での経験期待報酬が高いアームを引くのが良い（情報の活用）。 しかし、真の期待報酬が高いアームが、これまでたまたま運悪く少ない期待報酬しか得られていなかったということが低確率で発生する。 これを防ぐためには、すべてのアームを全体的に引く必要がある（情報の探索）。 予測者は、良いアルゴリズムに従って情報の活用と探索をバランスする必要がある。

# 期待値の更新
## 定常環境
定常環境では、各腕の報酬期待値は固定である。したがって以下の手法を用いて各腕の期待値を更新する。

![\begin{align*}
a &= \frac{1}{n_i} \\
E &= (1 - a)E + aE
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0Aa+%26%3D+%5Cfrac%7B1%7D%7Bn_i%7D+%5C%5C%0AE+%26%3D+%281+-+a%29E+%2B+aE%0A%5Cend%7Balign%2A%7D%0A)

## 非定常環境
非定常環境では、各腕の報酬期待値がランダムに入れ替わるため今までの期待値の更新ではうまく学習することができない。したがって以下の手法を用いて各腕の期待値を更新する。wはエージェントが報酬を受け取ったか、lはエージェントが報酬を受け取っていない状態で場合分けする。

![w_i = \left\{
\begin{array}{ll}
\gamma w_i + 1 & (a_i = a_s  \quad \& \quad  r=1)\\
 \gamma w_i & (otherwise)
\end{array}
\right.
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+w_i+%3D+%5Cleft%5C%7B%0A%5Cbegin%7Barray%7D%7Bll%7D%0A%5Cgamma+w_i+%2B+1+%26+%28a_i+%3D+a_s++%5Cquad+%5C%26+%5Cquad++r%3D1%29%5C%5C%0A+%5Cgamma+w_i+%26+%28otherwise%29%0A%5Cend%7Barray%7D%0A%5Cright.%0A)

![l_i = \left\{
\begin{array}{ll}
\gamma l_i  + 1 & (a_i = a_s  \quad \& \quad  r=0)\\
 \gamma l_i  & (otherwise)
\end{array}
\right.
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+l_i+%3D+%5Cleft%5C%7B%0A%5Cbegin%7Barray%7D%7Bll%7D%0A%5Cgamma+l_i++%2B+1+%26+%28a_i+%3D+a_s++%5Cquad+%5C%26+%5Cquad++r%3D0%29%5C%5C%0A+%5Cgamma+l_i++%26+%28otherwise%29%0A%5Cend%7Barray%7D%0A%5Cright.%0A)

![\begin{align*}
n_i &= w_i + l_i  \\
E_i  &= \frac{w_i}{w_i + l_i}
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0An_i+%26%3D+w_i+%2B+l_i++%5C%5C%0AE_i++%26%3D+%5Cfrac%7Bw_i%7D%7Bw_i+%2B+l_i%7D%0A%5Cend%7Balign%2A%7D%0A)

# 方策SRS(Stochastic Risk-sensitive Satisficing)
SRSとは既存の方策RSにおいて大きく異なるのが、決定論的な行動選択から確率分布を生成して確率論的な行動選択を行えるように拡張した手法である。
確率論的であることのメリットでは、ある程度環境がわかった状態でも探索を行うことでより良い選択肢を探す行動を行えることである。

![\begin{align*}
 b  &= \frac{n_i}{\rho_i^z} -  N +\epsilon \\
SRS_i &=  (N + b)\rho_i^z - n_i  \\
\pi_i &=  \frac{SRS_i}{SRS_1 + SRS_2 + \cdots +SRS_k}
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0A+b++%26%3D+%5Cfrac%7Bn_i%7D%7B%5Crho_i%5Ez%7D+-++N+%2B%5Cepsilon+%5C%5C%0ASRS_i+%26%3D++%28N+%2B+b%29%5Crho_i%5Ez+-+n_i++%5C%5C%0A%5Cpi_i+%26%3D++%5Cfrac%7BSRS_i%7D%7BSRS_1+%2B+SRS_2+%2B+%5Ccdots+%2BSRS_k%7D%0A%5Cend%7Balign%2A%7D%0A)

# 実験結果
実験結果から提案方策SRSは既存の方策よりもregretが低くなることがわかった。したがって方策SRSは複雑な環境において性能を発揮することがわかった。<br><br>
定常環境の結果

<img width="665" alt="スクリーンショット 2022-03-11 16 34 35" src="https://user-images.githubusercontent.com/95354321/157822848-2eec809d-6698-4d1e-9317-4bdc2471a23f.png">

非定常環境の結果

<img width="643" alt="スクリーンショット 2022-03-11 16 30 40" src="https://user-images.githubusercontent.com/95354321/157822360-847a0cfc-0dd6-42ea-bd4d-932c6470e807.png">

# 引用文献
https://www.jstage.jst.go.jp/article/pjsai/JSAI2021/0/JSAI2021_1G2GS2a04/_article/-char/ja
https://www.jstage.jst.go.jp/article/pjsai/JSAI2018/0/JSAI2018_1Z304/_article/-char/ja/
https://www.jstage.jst.go.jp/article/pjsai/JSAI2019/0/JSAI2019_2H3J203/_article/-char/ja/
