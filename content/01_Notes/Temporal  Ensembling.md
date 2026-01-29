#robotics #vla

[[Action Chunking with Transformers (ACT)]] 방법으로 매 time step마다 action sequence를 생성하면 같은 time step에 중복되는 action이 발생하는데, 이 action들을 merge해서 보다 안정적인 결과를 얻는 방법.

[[@zhaoLearningFineGrainedBimanual2023]] 논문에서는 exponential weighting scheme을 적용했다.