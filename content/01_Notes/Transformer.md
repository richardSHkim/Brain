---
tags:
  - llm
---
![[스크린샷 2026-01-07 오후 7.14.15.png]]
[[@vaswaniAttentionAllYou2023]] 논문에서 처음 제안.

[[Scaled Dot-Product Attention (SDPA)]] 연산으로만 구성된 네트워크 구조.
Encoder, decoder 구조로 제안되었지만, encoder only, decoder only 구조로도 쓰이며 특히 LLM은 decoder only 구조를 주로 사용함.#

Input과 output의 shape이 동일하게 유지됨.

Input embedding은 [[Embedding Matrix]]에서 lookup table 형식으로 구하며, 해당 matrix는 학습과정에서 유의미한 embedding을 갖도록 최적화 됨.

Attention 연산에는 위치 정보가 없으며, 이를 보완하기 위해 [[Position Encoding]]이 추가됨.