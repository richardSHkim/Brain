---
title: Alpamayo-R1 Bridging Reasoning and Action Prediction for Generalizable Autonomous Driving in the Long Tail
authors:  NVIDIA, Yan Wang, Wenjie Luo, Junjie Bai, Yulong Cao, Tong Che, Ke Chen, Yuxiao Chen, Jenna Diamond, Yifan Ding, Wenhao Ding, Liang Feng, Greg Heinrich, Jack Huang, Peter Karkus, Boyi Li, Pinyi Li, Tsung-Yi Lin, Dongran Liu, Ming-Yu Liu, Langechuan Liu, Zhijian Liu, Jason Lu, Yunxiang Mao, Pavlo Molchanov, Lindsey Pavao, Zhenghao Peng, Mike Ranzinger, Ed Schmerling, Shida Shen, Yunfei Shi, Sarah Tariq, Ran Tian, Tilman Wekel, Xinshuo Weng, Tianjun Xiao, Eric Yang, Xiaodong Yang, Yurong You, Xiaohui Zeng, Wenyuan Zhang, Boris Ivanovic, Marco Pavone
year: 2026
---
### Architecture
![[스크린샷 2026-01-28 오전 10.10.15.png]]
- Input
	- Multi-camera (2초 history, 2 Hz)
	- Ego motion (2초 history, 10 Hz)
		- 속도, 가속도, steering angle, 방향지시등
- Output
	- 6.4초 분량의 future trajectory (10 Hz)
	- Acceleration, curvature 예측
		- Unicycle dynamics
- Cosmos-Reason backbone
	- Efficient vision encoding
		- default: single image tokenization
		- Triplanes (multi-camera에 유리)
		- Flex (multi-camera, history에 유리)
		- future work: SparseVILA (token pruning)
	- Trajectory decoding
		- VLM 학습에는 tokenized trajectory
		- Action expert 학습에는 continuous trajectory

---

### Data
- CoC (Chain of Causation) 데이터셋 구축
	- 라벨러들이 실제로 history만 보고 reason을 작성 후, 전체 영상을 보고 reason 선택하여 결과를 보고 reason을 끼워맞추지 않도록 함
	- 데이터 설계 및 구축 과정은 추후에 참고하면 좋을 것 같음.
- Curation
	- Keyframe detection (rule-base)

---

### Train
- Action modality injection (Imitation Learning)
	- Inject the action modality into the VLM
		- Acceleration, curvature tokenization
		- Cross-entropy loss
	- Train action expert
		- Conditional flow matching loss
		- Gradient stop before VLM (knowledge insulation)
- Reasoning
	- SFT
	- 추론 텍스트 + 궤적 학습
- Post-training
	- GRPO
	- Rewards
		- Reasoning quality
		- CoC-Action consistency
		- Trajectory quality

---

### Experiments
- SFT w/o Reasoning vs. SFT w/ reasoning
	![[스크린샷 2026-01-28 오후 8.46.10.png]]
	- 40 token 정도의 concise reasoning
- SFT vs. RL
	![[스크린샷 2026-01-28 오후 8.46.43.png]]
- Auto-regressive VS. Flow Matching
	![[스크린샷 2026-01-28 오후 9.15.44.png]]
	- Auto-regressive 모델의 속도를 최대한 flow matching과 맞추고 실험.
		- VQGAN으로 decoding해야하는 token 수를 6개로 줄임.
- Vision Encoding
	![[스크린샷 2026-01-28 오후 9.18.04.png]]
	- 획기적인 token 사용량 개선 + 성능 향상. 안 쓸 이유가 없어보임.
	- Open-loop 평가라서 온전히 신뢰하기는 어려움.
- Real-time Performance
	![[스크린샷 2026-01-28 오후 9.25.58.png]]

---

### Future Work
- Meta-action -> motion primitives로 분해하는 hierarchical 구조
	- PTZ camera
- Reasoning on demand
- Auxiliary task integration
	- Depth estimation, scene flow, 3D gaussian splatting
- World model integration