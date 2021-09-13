---
title: "Modelica Language Specification V3.2 Rev2 - Introduction" 
excerpt: "Modelica Language Specification V3.2 Rev2 중 1장 Introduction 부분의 번역본 초안입니다." 
show_date: true
read_time: true

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "#8e9b63"

categories: 
- modelica
tags: 
- modelica
- language
- specification
- introduction
---

## 1. Introduction

### 1.1 Overview of Modelica

Modelica는 효과적인 라이브러리 개발 및 모델 교환을 지원하도록 설계된 물리적 시스템 모델링을 위한 언어입니다. 모델링 지식의 재사용을 용이하게 하기 위해 수학 방정식과 객체 지향 구조를 사용한 인과적 모델링을 기반으로 하는 현대적인 언어입니다.

### 1.2 Scope of the Specification

Modelica 언어의 의미는 Modelica 언어에 설명된 클래스를 평면 Modelica 구조로 변환하기 위한 일련의 규칙을 통해 지정됩니다. 클래스는 평면 Modelica 구조가 일련의 미분, 대수 및 이산 방정식(= Flat hybrid differential-algebraic equation(DAE))으로 추가 변환될 수 있도록 추가 속성을 가져야 합니다. 이러한 클래스를 시뮬레이션 모델이라고 합니다.

평면 Modelica 구조는 시뮬레이션 모델 이외의 다른 경우에도 정의됩니다. 기능(알고리즘 컨텐츠 제공에 사용 가능), 패키지(구조화 메커니즘으로 사용) 및 부분 모델(기본 모델로 사용)을 포함합니다. 이를 통해 시뮬레이션 모델을 구축하기 전에 정확성을 검증할 수 있습니다.

Modelica는 특히 기본적으로 모든 Modelica 언어 구성을 평면 Modelica 구조의 연속 또는 순간 방정식에 매핑하여 모델의 기호 변환을 용이하게 하도록 설계되었습니다. 특히 관련 Modelica 표준 라이브러리의 많은 Modelica 모델은 더 높은 지수 시스템이며 기호 지수 축소가 수행되는 경우에만 합리적으로 시뮬레이션할 수 있습니다. 즉, 방정식을 미분하고 적절한 변수를 상태로 선택하여 결과 방정식 시스템 상태 공간 형태(적어도 국부적으로 수치적으로), 즉 인덱스 0의 하이브리드 DAE로 변환될 수 있습니다. Modelica 사양은 모델을 시뮬레이션하는 방법을 정의하지 않습니다. 그러나 시뮬레이션 결과가 가능한 한 만족해야 하는 일련의 방정식을 정의합니다.

번역(또는 병합)의 주요 문제는 다음과 같습니다.

- 상속된 기본 클래스의 확장
- 기본 클래스, 로컬 클래스 및 구성 요소의 매개변수화 
- Connect-equation으로부터 connection equation 생성

Flat hybrid DAE의 형식은 다음과 같습니다.

- `parameter Real v=5`와 같은 적절한 기본 유형, 접두사 및 속성이 있는 변수 선언
- 방정식 섹션의 방정식
- 호출이 모든 입력 및 모든 결과 변수를 포함하는 방정식 세트로 취급되는 함수 호출(방정식의 갯수 = 변수의 갯수)
- 모든 섹션이 알고리즘 섹션에서 발생하는 변수를 포함하는 방정식 세트로 취급되는 알고리즘 섹션(방정식의 수 = 다른 할당된 변수의 수)
- 모든 when-절이 조건부로 평가된 방정식 세트로 취급되는 when-절, 순시 방정식이라고도 하는 이 방정식은 절에서 발생하는 변수의 함수입니다(방정식의 수 = 다른 할당된 변수의 수)

따라서 Flat hybrid DAE는 일부 방정식이 조건부로만 평가되는 방정식 세트로 간주됩니다(예: 순시 방정식은 해당 when-condition이 참이 될 때만 평가됨). 모델의 초기 설정은 초기 시간에만 유지되는 시작 값 및 순간 방정식을 사용하여 지정됩니다.

Modelica 클래스에는 클래스의 그래픽 표현(아이콘 및 다이어그램), 클래스에 대한 문서 텍스트 및 버전 정보를 지정하는 형식 주석과 같은 주석이 포함될 수도 있습니다.

### 1.3 Some Definitions

시맨틱 사양은 Modelica 문법과 함께 읽어야 합니다. 비규범적인 텍스트, 즉 예 및 주석은 [ ]로 묶습니다. 주석은 기울임꼴로 설정됩니다. 추가 용어는 부록 A의 용어집에 설명되어 있습니다. 몇 가지 중요한 용어는 다음과 같습니다.

| Term       | Definition                                                   |
| ---------- | ------------------------------------------------------------ |
| Component  | Modelica 문법에서 생산 `component_clause`에 의해 정의된 요소(기본적으로 클래스의 변수 또는 인스턴스) |
| Element    | 클래스에 선언된 클래스 정의, `extends-clause` 및 `component-clauses`(기본적으로 클래스 참조 또는 선언의 구성 요소) |
| Flattening | Modelica에 설명된 모델을 상속된 기본 클래스의 확장, 기본 클래스, 로컬 클래스 및 구성 요소의 매개 변수화, 연결 방정식에서 연결 방정식 생성(기본적으로 계층적 매핑 모델의 구조를 모델의 해당 변수 선언 및 함수 정의와 함께 미분, 대수 및 이산 방정식 세트로 변환). |

### 1.4 Notation and Grammar

다음 구문 메타 기호가 사용됩니다(확장 BNF).

```
[ ] optional
{ } repeat zero or more times
```

볼드체는 Modelica 언어의 키워드를 나타냅니다. 키워드는 예약어이며 식별자로 사용할 수 없습니다. 단, 섹션 제목의 키워드인 `initial`과 선언 함수의 키워드인 `der`를 제외하고는 `initial()` 및 `der(...)`함수를 호출하는 것도 가능합니다. 전체 어휘 사양 및 문법은 부록 B를 참조하십시오.