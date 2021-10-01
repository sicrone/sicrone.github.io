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

## 제 1 강 - 개요

[Modelica]([Modelica Language — Modelica Association](https://modelica.org/modelicalanguage.html))는 복잡한 물리 시스템을 모델링하기 위한 언어로, 기본적으로 시뮬레이션을 위해 설계되었지만 최적화 등의 다른 용도로도 사용 가능합니다. Robotics, Automotive, Aircrafts, Satellites, Power plants, System biology 등 다양한 분야에 활용 가능하며, 시간(time)이 포함된 Equation-based dynamic model을 사용합니다.

Modelica 언어의 주요 특징으로는,

- 선언적 언어(Declarative language) : 방정식 및 수학 함수를 통해 인과 관계 모델링, 높은 수준의 사양, 정확성 향상
- 다중 도메인 모델링 : 전기, 기계, 열역학, 유압, 생물학적, 제어, 이벤트, 실시간 등을 결합합니다.
- 모든 것이 클래스 : 일반 클래스 개념, Java 및 MATLAB과 유사한 구문을 사용하는 강력한 형식의 객체 지향 언어
- 비주얼 컴포넌트 프로그래밍 : 계층적 시스템 아키텍처 기능
- 효율적이고 비독점적 : C에 필적하는 효율성; 고급 방정식 편집, 예: 300,000 방정식, 표준 PC에서 ~150,000 라인
- 고급 언어 : MATLAB 스타일의 배열 작업 기능적인 스타일; 반복자, 생성자, 객체 지향, 방정식 등
- MATLAB 유사점 : MATLAB과 유사한 배열 및 스칼라 산술이지만 강력한 형식과 C에 필적하는 효율성.
- 비독점
  - 개방형 언어 표준
  - 오픈 소스 및 상용 구현 모두
- 유연하고 강력한 외부 기능 설비
  - LAPACK 인터페이스 작업 시작

## 제 2 강 - Modelica 환경

Modelica Language를 기반으로 하는 다양한 모델링 및 시뮬레이션 환경을 제공하는 대표적인 도구는 다음과 같습니다. 이 중에서 OpenModelica를 제외한 나머지는 상용 소프트웨어이며, 유일하게 OpenModelica만이 오픈소스 기반으로 개발된 도구입니다. OpenModelica는 Windows, Linux, Mac 등 다양한 플랫폼에서 사용 가능하며, 모든 OpenModelica GUI tool은 Qt4 GUI 라이브러리를 기반으로 만들어졌습니다.

- [Dymola](https://www.3ds.com/ko/products-services/catia/products/dymola/)
- [Simulation X](https://www.esi-group.com/products/system-simulation)
- [MapleSim](https://www.maplesoft.com/products/maplesim/)
- [Wolfram System Modeler](https://www.wolfram.com/system-modeler/) (예전 MathModelica)
- [Amesim](https://www.plm.automation.siemens.com/global/ko/products/simcenter/simcenter-amesim.html)
- [OpenModelica](https://www.openmodelica.org/)

아래의 그림은 OpenModelica Environment Architecture를 나타낸 것입니다.

<img src="{{ site.url }}/assets/img/om_fig01.jpg" />

모델을 시뮬레이션 코드로 변환하는 과정은 다음과 같습니다.

<img src="{{ site.url }}/assets/img/om_fig02.jpg" />

## 제 3 강 - Class

일반적인 시뮬레이션 프로세스

<img src="{{ site.url }}/assets/img/om_fig03.jpg" />

Modelica의 특별한 점

- 다중 도메인 모델링
- 시각적 비인과 관계 계층 구성 요소 모델링
- 형식화된 선언적 방정식 기반 텍스트 언어
- 하이브리드 모델링 및 시뮬레이션

다중 도메인 모델링

<img src="{{ site.url }}/assets/img/om_fig04.jpg" />

시각적 비인과 관계 계층 구성 요소 모델링

<img src="{{ site.url }}/assets/img/om_fig05.jpg" />

형식화된 선언적 방정식 기반 텍스트 언어

<img src="{{ site.url }}/assets/img/om_fig06.jpg" />

하이브리드 모델링 및 시뮬레이션

<img src="{{ site.url }}/assets/img/om_fig07.jpg" />

### Modelica 클래스 및 상속

#### Variables and Constants

내장된 기본 데이터 유형

- **Boolean** : true 혹은 false
- **Integer** : 정수값 예) 42, -3
- **Real** : 부동소수점 실수 예) 2.4e-6
- **String** : 문자열 예) "Hello world"
- **Enumeration** : 열거형 예) ShirtSize.Medium

Modelica에서 지원하는 두가지 유형의 상수

- **constant**
- **parameter** : 시뮬레이션 동안만 일정

```
constant  Real    PI = 3.14159265;
constant  String  redcolor = "red";
constant  Integer one = 1;
parameter Real    mass = 22.5;
```

#### Comments

선언 주석

```
Real x  "state variable";
```

소스코드 주석

```
Real x;  /* This is a C style comment */
Real y;  // Comment to the end of the line
```

#### Restricted Class Keywords

- **class** 키워드는 다음에 제시된 다른 키워드로 교체 가능
  - **model**, **record**, **block**, **connector**, **function** ...
- 상기 키워드로 선언된 클래스에는 제한 사항이 있음
- 제한 사항은 제한된 클래스의 내용에 적용됨
  - **model** : **connector** 클래스로 사용될 수 없는 클래스
  - **record** : 방정식 없이 데이터만 포함하는 클래스
  - **block** : 입/출력의 인과관계가 고정된 클래스

#### Modelica Functions

- Modelica에서 **Function**은 일부 확장 기능이 있는 특수한 종류의 제한된 클래스로 볼 수 있음
- **Function**은 인수를 사용하여 호출할 수 있으며, 호출될 때 동적으로 인스턴스화됨

#### Inheritance

- 여러개의 동일한 정의를 상속하면 하나의 정의만 상속
- 동일한 항목의 여러 다른 정의를 상속할 수 없음

```
record ColorData  // 부모 클래스
  parameter Real red = 0.2;
  parameter Real blue = 0.6;
  Real green;
end ColorData;

class Color  // 자식 클래스
  extends ColorData;  // 상속을 나타내는 키워드
  parameter Real blue = 0.6;  // Legal!
  parameter Real red = 0.3;   // Illegal!
equation
  red + blue + green = 1;
end Color;
```

- 방정식의 상속

```
class Color
  parameter Real blue = 0.2;
  parameter Real red = 0.6;
equation
  red + blue + green = 1;
end Color;

class Color2  // Color is identical to Color2
  extends Color
equation
  red + blue + green = 1;
end Color2;

class Color3  // Color3 is overdetermined. Error!!! 
  extends Color
equation
  red + blue + green = 1;
end Color2;
```

- 다중 상속 가능

```
class Color
  parameter Real blue = 0.2;
  parameter Real red = 0.6;
equation
  red + blue + green = 1;
end Color

class Point
  Real x;
  Real y, z;
end Point;

class ColoredPoint  // Multiple Inheritance
  extends Point;
  extends Color;
end ColoredPoint;

class ColoredPointWithoutInheritance // ColoredPoint 클래스와 동일
  Real x;
  Real y, z;
  parameter Real blue = 0.2;
  parameter Real red = 0.6;
equation
  red + blue + green = 1;
end ColoredPointWithoutInheritance;
```

- 단순 클래스 정의 - 상속의 약칭
  - 아래 두 클래스는 동일함

```
class SameColor = Color;
```

```
class SameColor
  extends Color;
end SameColor;
```

- 수정을 통한 상속
  - 수정은 상속을 클래스 또는 인스턴스 선언과 결합하는 간결한 방법
  - 수정자는 상속된 클래스의 선언 방정식을 수정
- 보호 요소의 상속
  - **extends**절 앞에 **protected** 키워드가 있으면 상위 클래스에서 상속된 모든 요소가 하위 클래스의 보호된 요소가 됨
  - **Point**에서 상속된 필드는 **extends**절 앞에 **public**이 오기 때문에 보호 상태를 유지

```
class Color
  Real red;
  Real blue;
  Real green;
equation
  red + blue + green = 1;
end Color;

class Point
  Real x;
  Real y, z;
end Point;

class ColoredPoint
 protected
  extends Color;
 public
  extends Point;
end ColoredPoint;

class ColoredPointWithoutInheritance // ColoredPoint 클래스와 동일
  Real x;
  Real y, z;
  protected Real red;
  protected Real blue;
  protected Real green;
equation
  red + blue + green = 1;
end ColoredPointWithoutInheritance;
```



계속 업데이트됩니다!!!

