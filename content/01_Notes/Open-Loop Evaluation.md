---
tags:
  - vla
---
Policy의 decision이 env를 변화시킬 수 없는 세팅의 evaluation 방법.
Grount-truth action과 policy action의 차이를 계산하여 evaluation 수행.
전체 trajectory를 비교할 수 없기 때문에 부정확하다.
[[Closed-Loop Evaluation]]에 비해 간단하고 빠르기 때문에 아주 많은 모델 혹은 checkpoint에 대해서 빠르게 평가를 진행해야할 때 사용하면 좋다.