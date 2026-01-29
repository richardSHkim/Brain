---
title: GR00T N1 An Open Foundation Model for Generalist Humanoid Robots
authors:  NVIDIA, Johan Bjorck, Fernando Castañeda, Nikita Cherniadev, Xingye Da, Runyu Ding, Linxi "Jim" Fan, Yu Fang, Dieter Fox, Fengyuan Hu, Spencer Huang, Joel Jang, Zhenyu Jiang, Jan Kautz, Kaushil Kundalia, Lawrence Lao, Zhiqi Li, Zongyu Lin, Kevin Lin, Guilin Liu, Edith Llontop, Loic Magne, Ajay Mandlekar, Avnish Narayan, Soroush Nasiriany, Scott Reed, You Liang Tan, Guanzhi Wang, Zu Wang, Jing Wang, Qi Wang, Jiannan Xiang, Yuqi Xie, Yinzhen Xu, Zhenjia Xu, Seonghyeon Ye, Zhiding Yu, Ao Zhang, Hao Zhang, Yizhou Zhao, Ruijie Zheng, Yuke Zhu
year: 2025
---
### Architecture
![[스크린샷 2026-01-14 오후 2.00.08.png]]
- Cross-attention 구조 사용
	- LLM의 12th layer embedding 사용
- Embodiment마다 state encoder, action encoder, action decoder를 따로 사용
- VLM에서는 vision encoder만 unfrozen, text tokenizer, LLM은 frozen.

---

### Data
![[스크린샷 2026-01-14 오후 2.45.24.png|350]]
- Real-world
	- Internal
	- Open X-Embodiment
	- AgiBot-Alpha
- Synthetic
	- Simulation trajectories
	- Neural trajectories
- Human videos
	![[스크린샷 2026-01-14 오후 3.44.05.png]]

---

### Data Generation
![[스크린샷 2026-01-14 오후 2.40.37.png]]
- Latent actions
	- [[@yeLatentActionPretraining2025|LAPA]]
	- Action 정보가 없는 데이터에 대해서 latent actions 값을 제공
- Neural trajectories
	- WAN2.1-I2V-14B, 480P, LoRA
	- VLM 기반 prompt augmentation
	- VLM as judge
		- Filter에 걸린 영상에 대해서 re-caption 진행
	- 기존 데이터 10배 수량 생성
- Simulation Trajectories
	- [[@jiangDexMimicGenAutomatedData2025a|DexMimicGen]]
		> we have generated 780,000 simulation trajectories — equivalent to 6,500 hours, or nine continuous months, of human demonstration data — in just 11 hours.
- Predicted Actions
	- IDM (Inverse Dynamics Model)
		- First frame + Last frame → Action chunk
	- System 1 architecture + SigLIP-2 vision embeddings, Flow matching

---
### Train

- Flow Matching
	- Auxiliary object detection loss on human videos
		> for each frame in a trajectory segment, we annotate the bounding box of the target object using the OWL-v2 object detector
- Pre-training
	
	||Latent Actions|Ground-truth Actions|Predicted Actions|
	|---|---|---|---|
	|Real-Robot Trajectories|O|O||
	|Simulated Trajectories|O|O||
	|Neural Trajectories|O||O|
	|Human videos|O|||
	
	- Robot datasets + Neural trajectories + Human videos
- Post-training
	
	||Ground-truth Actions|Predicted Actions|
	|---|---|---|
	|Real-Robot Trajectories|O||
	|Neural Trajectories||O|
	
	- Real-world trajectories + Neural trajectories (1:1 sampling ratio)
	- Neural trajectories에 대해서는 latent actions vs. predicted actions 실험해봤는데
		- IDM을 잘 학습시킬 충분한 real-world 데이터가 있다면, predicted actions가 성능이 더 좋았다.
- Standardized Action Spaces
	![[스크린샷 2026-01-14 오후 3.54.56.png]]
---

### Limitations
> Currently, our GR00T N1 model focuses primarily on short-horizon tabletop manipulation tasks.

> However, existing methods still face challenges in generating diverse and counterfactual data, while adhering to the laws of physics, limiting the quality and variability of synthetic datasets.

---

### Discussion

- Middle-layer embeddings
> 	We found that using middle-layer instead of final-layer LLM embeddings resulted in both faster inference speed and higher downstream policy success rate.

	- LLM 부분을 freeze 했기 때문에 꼭 마지막 layer가 최선일 필요는 없어보임.
- LLM frozen
	- [[@blackP0VisionLanguageActionFlow|Pi0]] 에서는 unfreeze
	- GR00T N1.6 에서는 unfreeze top 4 layers during pre-training
	- [[@yeLatentActionPretraining2025|LAPA]]는 vision encoder만 freeze, LLM은 unfreeze
- Embodiment Specific Modules
	- 새로운 embodiment에 대해 finetuning 필수
	- 예상하기로는, embodiment만 일치하면 어느정도 행동은 나올 것 같음
- Dual system architecture ([[System 1]] & [[System 2]])
	- Long horizon task를 planning과 함께 수행하는걸 기대했는데 아니었음.