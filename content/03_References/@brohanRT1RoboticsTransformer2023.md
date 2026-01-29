---
title: RT-1 Robotics Transformer for Real-World Control at Scale
authors: Anthony Brohan, Noah Brown, Justice Carbajal, Yevgen Chebotar, Joseph Dabis, Chelsea Finn, Keerthana Gopalakrishnan, Karol Hausman, Alex Herzog, Jasmine Hsu, Julian Ibarz, Brian Ichter, Alex Irpan, Tomas Jackson, Sally Jesmonth, Nikhil J. Joshi, Ryan Julian, Dmitry Kalashnikov, Yuheng Kuang, Isabel Leal, Kuang-Huei Lee, Sergey Levine, Yao Lu, Utsav Malla, Deeksha Manjunath, Igor Mordatch, Ofir Nachum, Carolina Parada, Jodilyn Peralta, Emily Perez, Karl Pertsch, Jornell Quiambao, Kanishka Rao, Michael Ryoo, Grecia Salazar, Pannag Sanketi, Kevin Sayed, Jaspiar Singh, Sumedh Sontakke, Austin Stone, Clayton Tan, Huong Tran, Vincent Vanhoucke, Steve Vega, Quan Vuong, Fei Xia, Ted Xiao, Peng Xu, Sichun Xu, Tianhe Yu, Brianna Zitkovich
year: 2023
---
### Model
- Transformer architecture
- action tokenization
- categorical cross-entropy loss
- token learner

---

### Imitation learning
- Issac sim과 같은 simulation 환경의 활용을 적극적으로 하기 어려움

---

### Inference
- 최소 3Hz, 다른 latency를 고려해서 모델 latency는 less than 100ms 는 되어야한다.
- action마다 280ms 대기

---

### Data collection
- vr controller로 사람이 조작
- 다양한 데이터 수집을 위해 환경, 명령을 randomize함.

---

### Model selection
- real-to-sim: simulation 데이터로 model selection 수행. RetinaGAN으로 domain gap 최소화.