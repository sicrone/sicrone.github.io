---
title: "대류항(Convection term)에 대한 이산화(Discritization) 방법 정리" 
excerpt: "CFD(Computational Fluid Dynamics)에서 대류항의 처리를 위한 이산화 방법 소개"
show_date: true
read_time: true

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "#E4B1FC"

categories: 
- cfd

tags: 
- CFD
- discritization
- convection term
- FVM

---

## 개요
- 유동 해석에서 대류항( ∇⋅(ρ**u**φ) )은 비선형적인 특성 때문에 수치적으로 다루기가 매우 까다롭습니다. 이 항을 어떻게 이산화하는지에 따라 해의 정확성, 안정성, 계산 비용이 크게 달라집니다. 주요 방법들은 정확도와 안정성 사이의 균형을 어떻게 맞추느냐에 따라 구분됩니다.

## 주요 대류항 이산화 기법
### 1차 풍상차분도법 (First-Order Upwind Scheme)
- **원리**: 가장 기본적인 방법으로, 유동의 방향을 고려하여 제어 체적(cell)의 경계면(face)에서의 물리량(φ)을 **상류(upwind)**에 위치한 격자점의 값으로 근사합니다. 즉, 바람이 불어오는 쪽의 값을 그대로 가져와 사용하는 방식입니다.
- **장점**: 매우 견고하고 안정적입니다. 특히 대류가 매우 강한 유동(높은 페클레 수)에서 비물리적인 진동(oscillation) 없이 항상 안정적인 해를 보장합니다.
- **단점**: 정확도가 1차에 불과하여 **수치 확산(numerical diffusion)**이라는 큰 오차를 유발합니다. 이로 인해 실제보다 물리량이 더 넓게 퍼지는 것처럼 계산되어, 급격한 구배(gradient)가 있는 영역을 뭉개버리는 단점이 있습니다.
### 중앙차분도법 (Central Differencing Scheme)
- **원리**: 경계면 양쪽에 있는 두 격자점의 값을 선형 보간(linear interpolation)하여 경계면에서의 값을 계산합니다.
- **장점**: 2차 정확도를 가지므로, 확산이 지배적인 유동(낮은 페클레 수)에서는 매우 정확한 결과를 제공합니다.
- **단점**: 대류가 지배적인 유동(페클레 수가 |Pe| > 2)에서는 안정성이 급격히 떨어져 해가 비현실적으로 진동하거나 발산할 수 있습니다. 이러한 불안정성 때문에 단독으로 사용되는 경우는 드뭅니다.
### 2차 풍상차분도법 (Second-Order Upwind Scheme)
- **원리**: 1차 풍상차분도법의 정확도를 개선한 방법입니다. 경계면의 값을 계산할 때, 상류에 있는 **두 개**의 격자점 값을 이용하여 선형으로 외삽(extrapolation)합니다.
- **장점**: 2차 정확도를 가지므로 1차 풍상차분도법보다 수치 확산이 훨씬 적습니다. 동시에 유동 방향을 고려하여 중앙차분보다 안정적입니다.
- **단점**: 여전히 급격한 변화가 있는 영역에서 약간의 진동(overshoot/undershoot)이 발생할 수 있습니다.
### QUICK 도법 (Quadratic Upwind Interpolation for Convective Kinematics)
- **원리**: 더 높은 정확도를 위해 2차 다항식(포물선)을 이용하는 방법입니다. 경계면의 값을 계산하기 위해 상류 쪽 2개와 하류 쪽 1개의 격자점을 포함한 총 3개의 점을 사용하여 2차 함수로 보간합니다.
- **장점**: 이론적으로 3차 정확도를 가지므로 매우 정밀한 해를 얻을 수 있습니다. 특히 유동 방향이 격자선과 나란하지 않을 때 발생하는 수치 확산을 줄이는 데 효과적입니다.
- **단점**: 중앙차분처럼 진동 문제가 발생할 수 있으며, 경계 조건 처리가 복잡합니다.
### 고해상도 기법 (High-Resolution Schemes): TVD, MUSCL 등
- 이 기법들은 고차 정확도의 장점을 유지하면서 진동을 억제하려는 시도에서 개발되었습니다.
- **TVD (Total Variation Diminishing) 기법**: 해의 총 변동(Total Variation)이 증가하지 않도록, 즉 새로운 극값(진동)이 생기지 않도록 보장하는 조건입니다. 이 조건을 만족하는 기법들은 급격한 구배나 충격파가 있는 영역에서도 안정적으로 고차 정확도를 유지합니다.
- **MUSCL (Monotonic Upstream-centered Scheme for Conservation Laws)**: TVD 조건을 만족시키는 대표적인 기법군입니다.
	- **원리**: 기본적으로 고차 기법(예: 2차 풍상차분)을 사용하되, 해의 변화가 급격한 지역에서는 **경사 제한자(slope limiter)**를 적용하여 구배를 완만하게 만듭니다. 이는 국부적으로 1차 풍상차분도법처럼 작동하여 진동을 억제하는 효과를 낳습니다.
	- **장점**: 해가 완만한 영역에서는 고차 정확도를 유지하고, 충격파나 불연속면 근처에서는 안정성을 확보하는, '똑똑한' 혼합 방식입니다. 정확성과 안정성을 모두 잡기 위한 현대적인 CFD 코드에서 널리 사용됩니다.
	
## 요약 비교
| 기법 | 정확도 차수 | 안정성 | 주요 특징 및 단점 |
| --- | --- | --- | --- |
| 1st-Order Upwind | 1차 | 매우 높음 | 안정적이지만, 수치 확산(오차)이 매우 큼 (비정확) |
| Central Differencing | 2차 | 낮음 | 정확하지만, 대류가 강할 때 비물리적 진동 발생 (불안정) |
| 2nd-Order Upwind | 2차 | 보통 | 정확도와 안정성의 절충안. 범용적으로 사용됨 |
| QUICK | 3차 | 보통 | 고정밀 해석에 유리하나, 진동이 발생할 수 있음 |
| MUSCL/TVD | 고차 | 높음 | 고차 정확도를 유지하면서 진동을 억제함. 충격파 등 불연속 문제에 강함 |

## References
- [https://www.youtube.com/watch?v=zFwtF-WkBoU](https://www.youtube.com/watch?v=zFwtF-WkBoU)
- [https://en.wikipedia.org/wiki/Upwind_differencing_scheme_for_convection](https://en.wikipedia.org/wiki/Upwind_differencing_scheme_for_convection)
- [https://en.wikipedia.org/wiki/Central_differencing_scheme](https://en.wikipedia.org/wiki/Central_differencing_scheme)
- [https://adamdjellouli.com/articles/numerical_methods/3_differentiation/central_difference](https://adamdjellouli.com/articles/numerical_methods/3_differentiation/central_difference)
- [https://en.wikipedia.org/wiki/QUICK_scheme](https://en.wikipedia.org/wiki/QUICK_scheme)
- [https://arxiv.org/pdf/2006.15143.pdf](https://arxiv.org/pdf/2006.15143.pdf)
- [https://www.sciencedirect.com/science/article/abs/pii/002199919290177Z](https://www.sciencedirect.com/science/article/abs/pii/002199919290177Z)
- [https://en.wikipedia.org/wiki/MUSCL_scheme](https://en.wikipedia.org/wiki/MUSCL_scheme)
- [https://arxiv.org/pdf/2301.02087.pdf](https://arxiv.org/pdf/2301.02087.pdf)
- [https://www.reddit.com/r/CFD/comments/cjppb3/what_is_a_muscl_scheme/](https://www.reddit.com/r/CFD/comments/cjppb3/what_is_a_muscl_scheme/)
- [https://www.aub.edu.lb/msfea/research/Documents/CFD-Chapter11TheConvectionTerm.pdf](https://www.aub.edu.lb/msfea/research/Documents/CFD-Chapter11TheConvectionTerm.pdf)
- [https://www.sciencedirect.com/science/article/pii/0045782585900659](https://www.sciencedirect.com/science/article/pii/0045782585900659)
- [https://www.youtube.com/watch?v=t9v5JevUSaM](https://www.youtube.com/watch?v=t9v5JevUSaM)
- [https://www.tandfonline.com/doi/abs/10.1080/00207160701870852](https://www.tandfonline.com/doi/abs/10.1080/00207160701870852)
- [https://onlinelibrary.wiley.com/doi/10.1002/num.22064](https://onlinelibrary.wiley.com/doi/10.1002/num.22064)
- [https://en.wikipedia.org/wiki/Numerical_solution_of_the_convection%E2%80%93diffusion_equation](https://en.wikipedia.org/wiki/Numerical_solution_of_the_convection%E2%80%93diffusion_equation)
- [https://research.tue.nl/files/1436139/458484.pdf](https://research.tue.nl/files/1436139/458484.pdf)
- [https://en.wikipedia.org/wiki/Upwind_scheme](https://en.wikipedia.org/wiki/Upwind_scheme)
- [https://www.afs.enea.it/project/neptunius/docs/fluent/html/th/node366.htm](https://www.afs.enea.it/project/neptunius/docs/fluent/html/th/node366.htm)
- [https://www.openfoam.com/documentation/user-guide/6-solving/6.2-numerical-schemes](https://www.openfoam.com/documentation/user-guide/6-solving/6.2-numerical-schemes)
- [https://www.cfd-online.com/Wiki/Approximation_Schemes_for_convective_term_-_structured_grids_-_Common](https://www.cfd-online.com/Wiki/Approximation_Schemes_for_convective_term_-_structured_grids_-_Common)
- [https://www.sciencedirect.com/science/article/pii/S1877050913005255](https://www.sciencedirect.com/science/article/pii/S1877050913005255)
- [https://www.cfd-online.com/Forums/openfoam-solving/60566-quick-discretizaion-scheme.html](https://www.cfd-online.com/Forums/openfoam-solving/60566-quick-discretizaion-scheme.html)
- [https://www.akademiabaru.com/doc/ARFMTSV58_N1_P100_117.pdf](https://www.akademiabaru.com/doc/ARFMTSV58_N1_P100_117.pdf)
- [https://www.cfd.at/sites/default/files/tutorialsV4/4-ExampleFour.pdf](https://www.cfd.at/sites/default/files/tutorialsV4/4-ExampleFour.pdf)
- [https://www.youtube.com/watch?v=q9hShZweRTE](https://www.youtube.com/watch?v=q9hShZweRTE)
- [https://www.sciencedirect.com/science/article/abs/pii/S0021999121005350](https://www.sciencedirect.com/science/article/abs/pii/S0021999121005350)
- [https://su2code.github.io/docs_v7/Convective-Schemes/](https://su2code.github.io/docs_v7/Convective-Schemes/)
- [https://help.sim-flow.com/documentation/panels/discretization](https://help.sim-flow.com/documentation/panels/discretization)
- [https://onlinelibrary.wiley.com/doi/10.1002/fld.5399](https://onlinelibrary.wiley.com/doi/10.1002/fld.5399)