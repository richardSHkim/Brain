[[Transformer]], 즉, [[Scaled Dot-Product Attention (SDPA)]] 연산에는 입력 token의 위치 정보를 처리하는 과정이 없다. 
하지만, text와 같은 sequential한 정보는 위치 정보가 중요하다. 
Position encoding은 이를 보완하기 위해 제안된 방법이다.

구현에는 여러 방법이 있다.
큰 틀에서는 token의 절대적인 위치 index를 사용하는 [[Absolute Position Encoding]], 두 토큰 사이의 상대적인 위치 index를 사용하는 [[Relative Position Encoding]] 이 있다. 둘을 같이 사용하는 방법도 있으며, 자세한 내용은 [[@suRoFormerEnhancedTransformer2023]] 논문의 섹션 2. Background and Related Work 참조.

대표적으로 많이 사용되는 방법은 [[RoPE]] 방식이며, [[@wangQwen2VLEnhancingVisionLanguage2024]] 에서는 [[MRoPE]] 방식을 제안했다. 그 후에는 [[@baiQwen3VLTechnicalReport2025]]에서 [[Interleaved MRoPE]] 방식을 제안했다.