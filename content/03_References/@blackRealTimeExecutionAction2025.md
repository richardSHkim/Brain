---
title: Real-Time Execution of Action Chunking Flow Policies
authors: Kevin Black, Manuel Y. Galliker, Sergey Levine
year: 2025
---
### Algorithm
- [[Action chunking]] with naive async, temporal ensemble
	![[스크린샷 2026-01-20 오후 5.41.24.png|300]]
- RTC (Real-Time Chunking) with soft masking
	![[스크린샷 2026-01-20 오후 5.41.53.png]]

---

### Simulated Benchmark Dataset
> Most simulated imitation learning benchmarks are quasi-static

> To simulate imperfect actuation, we add Gaussian noise to the actions, making closed-loop corrections crucial for success.

- 공개는 안한 것 같음.

---
### Discussion

- Increased denoising latency
	![[스크린샷 2026-01-20 오후 5.50.19.png]]
	- Training-free 말고 학습 단계에서부터 inpainting을 학습하면 어떨지
