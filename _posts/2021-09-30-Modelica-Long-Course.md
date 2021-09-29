---
title: "Modelica Long Course" 
excerpt: "Peter Fritzson et al.의 Principles of Object-Oriented Modeling and Simulation with Modelica 강의 내용 일부를 발췌하여 번역한 것입니다."
show_date: true
read_time: true

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "#8FBC8F"

categories: 
- modelica
tags: 
- modelica
- openmodelica
- simulation
---
# Principles of Object-Oriented Modeling and Simulation with Modelica

이 문서는 2010년 10월에  Linköping University에서 진행된 Peter Fritzson et al.의 **Principles of Object-Oriented Modeling and Simulation with Modelica** 강의자료의 내용 일부를 발췌하여 번역한 것입니다.

## 제 1 강 - Introduction

[Modelica]([Modelica Language — Modelica Association](https://modelica.org/modelicalanguage.html))는 복잡한 물리 시스템을 모델링하기 위한 언어로, 기본적으로 시뮬레이션을 위해 설계되었지만 최적화 등의 다른 용도로도 사용 가능합니다. Robotics, Automotive, Aircrafts, Satellites, Power plants, System biology 등 다양한 분야에 활용 가능하며, 시간(time)이 포함된 Equation-based dynamic model을 사용합니다.

Modelica 언어의 주요 특징으로는,

- 선언적 언어(Declarative language)
  방정식 및 수학 함수를 통해 인과 관계 모델링, 높은 수준의 사양, 정확성 향상
- 다중 도메인 모델링
  전기, 기계, 열역학, 유압, 생물학적, 제어, 이벤트, 실시간 등을 결합합니다.
- 모든 것이 Class
  일반 클래스 개념, Java 및 MATLAB과 유사한 구문을 사용하는 강력한 형식의 객체 지향 언어
- 비주얼 컴포넌트 프로그래밍
  계층적 시스템 아키텍처 기능
- 효율적이고 비독점적
  C에 필적하는 효율성; 고급 방정식 편집, 예: 300,000 방정식, 표준 PC에서 ~150,000 라인
- 고급 언어
  MATLAB 스타일의 배열 작업 기능적인 스타일; 반복자, 생성자, 객체 지향, 방정식 등
- MATLAB 유사점
  MATLAB과 유사한 배열 및 스칼라 산술이지만 강력한 형식과 C에 필적하는 효율성.
- 비독점
  - 개방형 언어 표준
  - 오픈 소스 및 상용 구현 모두
- 유연하고 강력한 외부 기능 설비
  - LAPACK 인터페이스 작업 시작

## 제 2 강 - Modelica Environments

Modelica Language를 기반으로 하는 다양한 모델링 및 시뮬레이션 환경을 제공하는 대표적인 도구는 다음과 같습니다. 이 중에서 OpenModelica를 제외한 나머지는 상용 소프트웨어이며, 유일하게 OpenModelica만이 오픈소스 기반으로 개발된 도구입니다. OpenModelica는 Windows, Linux, Mac 등 다양한 플랫폼에서 사용 가능하며, 모든 OpenModelica GUI tool은 Qt4 GUI 라이브러리를 기반으로 만들어졌습니다.

- [Dymola](https://www.3ds.com/ko/products-services/catia/products/dymola/)
- [Simulation X](https://www.esi-group.com/products/system-simulation)
- [MapleSim](https://www.maplesoft.com/products/maplesim/)
- [Wolfram System Modeler](https://www.wolfram.com/system-modeler/) (예전 MathModelica)
- [Amesim](https://www.plm.automation.siemens.com/global/ko/products/simcenter/simcenter-amesim.html)
- [OpenModelica](https://www.openmodelica.org/)

아래의 그림은 OpenModelica Environment Architecture를 나타낸 것입니다.

<img src="{{ site.url }}/assets/img/om_fig01.jpg" style="zoom:50%;" />

모델을 시뮬레이션 코드로 변환하는 과정은 다음과 같다.

<img src="{{ site.url }}/assets/img/om_fig02.jpg" style="zoom:50%;" />

계속 업데이트됩니다!!!

