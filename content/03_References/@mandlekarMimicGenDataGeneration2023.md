---
title: MimicGen A Data Generation System for Scalable Robot Learning using Human Demonstrations
authors: Ajay Mandlekar, Soroush Nasiriany, Bowen Wen, Iretiayo Akinola, Yashraj Narang, Linxi Fan, Yuke Zhu, Dieter Fox
year: 2023
---
- (Small set of) Real -> Sim -> Real
- Assumption
	- Action space는 delta end effector pose이다.
	- Tasks는 object-centric subtasks로 분해할 수 있다.
		- object-centric subtask는 object 기준의 좌표계로 표현된 trajectory이다.
	- Object의 위치는 각 subtask의 시작 시점에서 파악할 수 있다. (데이터 수집 과정 중에만 해당)
- Method
	- 원본 task를 object-centric subtasks로 분해
	- 새로운 환경 구축 (Sim)
	- 새로운 객체의 위치를 기준으로 reference trajectory를 변환
	- 변환된 subtasks 끼리는 naive linear interpolation으로 연결
	- Post-hoc verification으로 실패 케이스 삭제
- Limitation
	> Naive interpolation scheme and no guarantee on collision-free motion