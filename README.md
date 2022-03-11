# バンディット問題
複数のアームと呼ばれる候補から最も良いものを逐次的に探す問題である。報酬を最大化するという点で、バンディット問題は強化学習のカテゴリに属する。バンディット問題の予測者は、限られた試行回数において得られる総報酬を最大化したい。 このとき、強化学習の普遍的なテーマである探索と活用のトレードオフが発生する。 短期的には、現時点での経験期待報酬が高いアームを引くのが良い（情報の活用）。 しかし、真の期待報酬が高いアームが、これまでたまたま運悪く少ない期待報酬しか得られていなかったということが低確率で発生する。 これを防ぐためには、すべてのアームを全体的に引く必要がある（情報の探索）。 予測者は、良いアルゴリズムに従って情報の活用と探索をバランスする必要がある。

# 期待値の更新
## 定常環境
## 非定常環境

# 方策
![\begin{align*}
 b  &= \frac{n_i}{\rho_i^z} -  N +\epsilon \\
SRS_i &=  (N + b)\rho_i^z - n_i  \\
\pi_i &=  \frac{SRS_i}{SRS_1 + SRS_2 + \cdots +SRS_k}
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0A+b++%26%3D+%5Cfrac%7Bn_i%7D%7B%5Crho_i%5Ez%7D+-++N+%2B%5Cepsilon+%5C%5C%0ASRS_i+%26%3D++%28N+%2B+b%29%5Crho_i%5Ez+-+n_i++%5C%5C%0A%5Cpi_i+%26%3D++%5Cfrac%7BSRS_i%7D%7BSRS_1+%2B+SRS_2+%2B+%5Ccdots+%2BSRS_k%7D%0A%5Cend%7Balign%2A%7D%0A)

# 実験結果

# 引用文献
https://www.jstage.jst.go.jp/article/pjsai/JSAI2021/0/JSAI2021_1G2GS2a04/_article/-char/ja
https://www.jstage.jst.go.jp/article/pjsai/JSAI2018/0/JSAI2018_1Z304/_article/-char/ja/
https://www.jstage.jst.go.jp/article/pjsai/JSAI2019/0/JSAI2019_2H3J203/_article/-char/ja/
