---
title: π0 A Vision-Language-Action Flow Model for General Robot Control
authors: Kevin Black, Noah Brown, Danny Driess, Adnan Esmail, Michael Equi, Chelsea Finn, Niccolo Fusai, Lachy Groom, Karol Hausman, Brian Ichter, Szymon Jakubczak, Tim Jones, Liyiming Ke, Sergey Levine, Adrian Li-Bell, Mohith Mothukuri, Suraj Nair, Karl Pertsch, Lucy Xiaoyang Shi, James Tanner, Quan Vuong, Anna Walling, Haohuan Wang, Ury Zhilinsky
year: 
---
### Architecture
![[스크린샷 2026-01-07 오전 9.24.35.png]]
- [[@zhouTransfusionPredictNext2024|Transfusion]] 구조 참고
- Robot-sepcific token을 처리할 weights를 따로 구성하는게 성능이 더 좋았다. (MoE)
	- Transfusion은 단일 transformer 사용
	- VLM (PaliGemma 3B) + Flow Matching (action expert 300M)
	- Action expert는 full bidirectional attention mask 사용
		![[스크린샷 2026-01-07 오후 12.00.39.png|300]]

---

### Train
- Flow matching loss
- Flow matching timestep sampling
	![[스크린샷 2026-01-08 오후 5.20.42.png|300]]
> predicting the mean action conditioned on a robot observation (i.e., learning $E[A_t|o_t]$) is a much harder problem

---

### Inference
![[스크린샷 2026-01-07 오후 1.53.01.png|400]]
- RTX4090에서 속도 측정, mobile robot에 대해서는 off-board (wifi)로 추론 (+13 ms)
- Temporal ensembling은 성능저하를 일으켜서 사용하지 않음
	- action chunk의 뒷부분은 정확도가 떨어져서 사용하지 않는게 더 좋음

---
### Data
- Pre-training
	- open-source dataset (9.1 %)
		- OXE Magic Soup (curated subset of OXE)
		- Bridge v2
		- DROID
	- Internal dataset
		- 903M timesteps
		- 7 different robot configurations
		- 68 tasks
			- “bussing” task로 정의하여 이전에 정의하던 task보다 복잡하다.
				- prior works: “pick up the cup”, “pick up the plate”
				- this work: putting a wide range of different dishes, cups, and utensils into a bussing bin
- Post-training
	- smaller task-specific dataset
- Pre / Post training data 선별 기준
	> the pre-training dataset should cover as many tasks as possible, and within each of those tasks should cover a diversity of behaviors. The post-training dataset should instead cover behaviors that are conducive to effective task execution, which should exhibit a consistent and fluent strategy.

---

### Discussion
- 입력 image가 단일 time step t 인 점은 RT-1, RT-2 와 다름.
	- RT-1, RT-2: history input → single time action
	- $\pi0$: single time input → action sequence
		- 자율주행이나 object가 움직이는 환경에서는 history가 필요하지 않을까
		- cosmos reason
- Action token
	- joint 값
	- end effector의 state
- Action chunking + Temporal Ensemble
	![[스크린샷 2026-01-06 오후 2.25.04.png|400]]
	- [[Action chunking]]
		- neuroscience 개념
			- individual actions are grouped together and executed as one unit, making them more efficient to store and execute
		- [[@zhaoLearningFineGrainedBimanual2023|ALOHA]] 논문에서 [[Action Chunking with Transformers (ACT)]] 처음 제안
		- Generative model에 action sequence를 학습
	- Temporal Ensemble
		- Action sequence를 생성하면서 동일한 time step에서 action을 2번 이상 생성하는 경우 발생 → ensemble하여 안정성 향상
		- ALOHA 논문에서는 exponential weighting scheme 사용
		- Temporal ensembe이 history input 역할을 해주는게 아닌가
- VLA에서 transfusion 구조의 장점
	- Discrete + continuous modality의 통합
		- Action (joint 값)은 continuous 값이다.
		- bin 필요없음
		- VLM 기반 detection에 적용해보면 좋을듯 (continuous box coordinate)
	- 단일 action을 구성하는 joint value들은 sequence 특징이 없다.
		- 하지만, action sequence는 sequential
	- Diffusion으로 trajectory (action chunk)를 한번에 생성
		- Action chunking에 유리
- 서로 다른 종류의 로봇 데이터를 어떻게 학습에 사용하는가
	- embodiment에 대한 conditioning
- 추론 단계에서 VLA는 현재 환경이 어떤 embodiment인지 어떻게 알 수 있나
	- 명시적인 embodiment token 사용
	- State 입력 값
- Mistakes
> Intuitively, training only on high-quality data does not teach the model how to recover from mistakes, since mistakes are rarely seen in such data. Training on only lower-quality pretraining data does not teach the model to act efficiently and robustly.
	
	- mistake → recovery도 imitation learning으로 커버할 수 있을까? imitation learning이 최적일까?
- $\pi0$ 소스코드
	- JAX 기반
		- 속도 최적화를 위해 jax를 사용하지 않았을까 하는 생각이 들었음
	- 일부 모델에 대해서 PyTorch 지원
		- pytorch 모델 추론에도 jax가 쓰이는데 어떤 용도로 쓰이는지는 아직 파악 못함
		- jit compile 같은걸 하는 것 같음
	- DROID가 학습 데이터셋에 있는데, DROID finetuned 체크포인트를 따로 공개
		- 성능 차이가 궁금
