#llm

[[@vaswaniAttentionAllYou2023]] 논문에서 제안되었으며, [[Transformer]] 구조의 핵심 연산이다.

$$\text{Attention}(Q,K,V) = \text{softmax}(\frac{QK^T}{\sqrt{d_k}})V$$
$$Q = W_q \times x$$
$$K = W_k \times x$$
$$V = W_v \times x$$

어떠한 입력 값 $x$에서 서로 다른 linear layer를 통해 $Q, K, V$ 값을 얻은 후 attention 연산을 수행한다.

$Q, K, V$ 는 $[\text{batch\_size} \times \text{sequence\_length} \times D]$와 같은 shape을 가진다.

$Q, K, V$가 모두 동일한 입력 $x$에 대해서 계산되면 self attention, $Q$와 $K,V$가 서로 다른 입력에 대해서 계산되면 cross attention이 된다.

Output은 $Q$의 shape을 가진다.