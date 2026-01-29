---
title: $π_{0.5}$ a Vision-Language-Action Model with Open-World Generalization
authors: Physical Intelligence, Kevin Black, Noah Brown, James Darpinian, Karan Dhabalia, Danny Driess, Adnan Esmail, Michael Equi, Chelsea Finn, Niccolo Fusai, Manuel Y. Galliker, Dibya Ghosh, Lachy Groom, Karol Hausman, Brian Ichter, Szymon Jakubczak, Tim Jones, Liyiming Ke, Devin LeBlanc, Sergey Levine, Adrian Li-Bell, Mohith Mothukuri, Suraj Nair, Karl Pertsch, Allen Z. Ren, Lucy Xiaoyang Shi, Laura Smith, Jost Tobias Springenberg, Kyle Stachowicz, James Tanner, Quan Vuong, Homer Walke, Anna Walling, Haohuan Wang, Lili Yu, Ury Zhilinsky
year: 2025
---

Related: [[@blackP0VisionLanguageActionFlow]]

### Architecture
![[스크린샷 2026-01-21 오전 10.46.53.png]]

---
### Train
- [[@pertschFASTEfficientAction2025|FAST]] tokenization for pre-training
- LM Loss + FM Loss

---

### Inference
- High-level instruction -> low-level instructions -> actions

---

### Data
- Pre-training
	- Diverse Mobile Manipulator data (MM)
	- Diverse Multi-Environment non-mobile robot data (ME)
	- Cross-Embodiment laboratory data (CE)
	- High-Level subtask prediction (HL)
	- Multi-modal Web Data (WD)
		- image captioning
		- question answering
		- object localization
- Post-training
	- Filtered MM
	- Filtered ME
	- WD
	- slice of HL
	- Verbal Instruction (VI)