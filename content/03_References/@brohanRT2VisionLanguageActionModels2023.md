---
title: RT-2 Vision-Language-Action Models Transfer Web Knowledge to Robotic Control
authors: Anthony Brohan, Noah Brown, Justice Carbajal, Yevgen Chebotar, Xi Chen, Krzysztof Choromanski, Tianli Ding, Danny Driess, Avinava Dubey, Chelsea Finn, Pete Florence, Chuyuan Fu, Montse Gonzalez Arenas, Keerthana Gopalakrishnan, Kehang Han, Karol Hausman, Alexander Herzog, Jasmine Hsu, Brian Ichter, Alex Irpan, Nikhil Joshi, Ryan Julian, Dmitry Kalashnikov, Yuheng Kuang, Isabel Leal, Lisa Lee, Tsang-Wei Edward Lee, Sergey Levine, Yao Lu, Henryk Michalewski, Igor Mordatch, Karl Pertsch, Kanishka Rao, Krista Reymann, Michael Ryoo, Grecia Salazar, Pannag Sanketi, Pierre Sermanet, Jaspiar Singh, Anikait Singh, Radu Soricut, Huong Tran, Vincent Vanhoucke, Quan Vuong, Ayzaan Wahid, Stefan Welker, Paul Wohlhart, Jialin Wu, Fei Xia, Ted Xiao, Peng Xu, Sichun Xu, Tianhe Yu, Brianna Zitkovich
year: 2023
---

### Contributions
- VLA 명칭을 처음으로 제안
- 이전 방식에도 LLM, VLM을 robotics에 적용한 사례는 있었으나, high-level planning에만 활용하였고 low-level controller로는 활용되지 않았다.
- Tokenizing the actions 를 통해 VLMs을 instruction following robotic polices로 직접적으로 학습한다.

---
### Methods
- PaLI-X, PaLM-E, 최대 55B size
	- multi-TPU cloud server 사용
- Co-finetuning is key

---
### Experiments
- Data
	- [[@brohanRT1RoboticsTransformer2023|RT-1]] data
	- Language Table Benchmark
		- 로봇 팔이 2D 평면 위에서 다양한 물체를 밀어서(pushing) 특정 위치로 옮기거나 특정 물체 근처로 이동시키는 과제를 수행
- Emergent capabilities
	- 로봇 훈련 데이터에는 없었지만, 웹 데이터의 지식이 전이되어 나타나는 새로운 능력
- CoT Reasoning