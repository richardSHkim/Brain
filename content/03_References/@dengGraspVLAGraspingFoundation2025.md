---
title: GraspVLA a Grasping Foundation Model Pre-trained on Billion-scale Synthetic Action Data
authors: Shengliang Deng, Mi Yan, Songlin Wei, Haixin Ma, Yuxin Yang, Jiayi Chen, Zhiqi Zhang, Taoyu Yang, Xuheng Zhang, Wenhao Zhang, Heming Cui, Zhizheng Zhang, He Wang
year: 2025
---
- 3D object asset -> Objaverse
- 객체를 잡는 pose (grasp) 계산 -> BODex
- 현재 pose에서 객체를 잡는 pose까지 trajectory 계산 -> CuRobo
- MuJoCo에서 실제로 계산된 trajectory가 성공/실패인지 판단
- IsaacSim에서 domain randomize, camera randomize 적용하여 렌더링