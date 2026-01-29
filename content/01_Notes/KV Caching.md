#llm #inference_optimization

[[Transformer]] 기반의 [[Autoregressive Models]]은 [[Scaled Dot-Product Attention (SDPA)]] 연산 과정에서 동일한 K, V 계산을 여러번 수행하게 된다.

KV caching은 이전에 계산한 K, V를 저장해서 연산량을 줄이는다.