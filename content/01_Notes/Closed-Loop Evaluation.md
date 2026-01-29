---
tags:
  - vla
---
실제 환경 혹은 가상 환경 (simulation)을 구축하여 그 안에서 policy에 대한 평가를 진행.
Policy의 decision이 env에 변화를 주고 이 변화가 다시 policy의 input으로 사용된다.
[[Open-Loop Evaluation]]에 비해 정확한 평가 방법으로, 사실상 robotics 분야에서의 평가 방법이다.
실제 환경을 사용하는 평가의 경우에는 reproduciblity가 떨어진다.
Simulation 환경은 셋팅만 정확하게 공유된다면 reproducibility가 좋지만, 실제 환경과의 차이 때문에 신용도가 떨어질 수는 있다.