[[@suRoFormerEnhancedTransformer2023]] 논문에서 제안한 방식으로, token 위치에 따라 rotation matrix를 적용하는 방식.

Rotation matrix에서는 absolute position 정보를 encode하고, inner product 연산에서는 relative position 정보를 사용하여 [[Absolute Position Encoding]] 과 [[Relative Position Encoding]] 방식의 특징을 모두 가지고 있다.