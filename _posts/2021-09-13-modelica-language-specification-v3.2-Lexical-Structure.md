---
title: "Modelica Language Specification V3.2 Rev2 - Lexical Structure" 
excerpt: "Modelica Language Specification V3.2 Rev2 중 2장 Lexical Structure 부분의 번역본 초안입니다." 
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
- Lexical structure
---

## 2. Lexical Structure

이 장에서는 식별자 및 리터럴을 포함한 어휘 단위 및 문자와 같은 Modelica의 몇 가지 기본 빌딩 블록에 대해 설명합니다. 의심의 여지 없이 Modelica의 가장 작은 구성 요소는 문자 집합에 속하는 단일 문자입니다. 문자는 토큰이라고도 하는 어휘 단위를 형성하기 위해 결합됩니다. 이러한 토큰은 Modelica 번역기의 어휘 분석 부분에서 감지됩니다. 토큰의 예로는 리터럴 상수, 식별자 및 연산자가 있습니다. 주석은 결국 폐기되기 때문에 실제로는 어휘 단위가 아닙니다. 반면에 주석은 폐기되기 전에 어휘 분석기에 의해 감지됩니다. 여기에 제공된 정보는 부록 B의 보다 공식적인 사양에서 파생되었습니다.

### 2.1 Character Set

Modelica 언어의 문자 집합은 유니코드이지만 여러 위치에서 7비트 ASCII 문자에 해당하는 유니코드 문자로 제한됩니다. 자세한 내용은 부록 B.1을 참조하십시오.

### 2.2 Comments

Modelica에는 언어의 어휘 단위가 아닌 두 가지 종류의 주석이 있으며, Modelica 번역기에 의해 공백으로 처리됩니다 . 공백 문자는 공백, 표 및 줄 구분 기호(캐리지 리턴 및 줄 바꿈)입니다. 토큰 내부에는 공백이 있을 수 없습니다. 예를 들어 `<=`는 공백이나 주석 없이 두 문자로 작성해야 합니다[주석 구문은 C++과 동일합니다]. 다음과 같이 주석을 사용할 수 있습니다.

```
// comment      //부터 줄 끝까지의 문자는 무시됩니다.
/* comment */   /*와 */ 사이의 문자는 무시됩니다.
```

Modelica 주석은 중첩되지 않습니다. 즉, `/* */`는 `/* */` 안에 포함될 수 없습니다. 다음은 유효하지 않습니다.

```
/* Commented out - erroneous comment, invalid nesting of comments!
/* This is a interesting model */
model interesting
...
end interesting;
*/
```

일종의 "문서 주석"도 있는데, 실제로는 Modelica 언어의 일부인 문서 문자열이므로 Modelica 번역기가 무시하지 않습니다. 이러한 "주석"은 선언, 방정식 또는 명령문의 끝이나 클래스 정의의 시작 부분에 나타날 수 있습니다. 예를 들면,

```
model TempResistor "Temperature dependent resistor"
...
parameter Real R "Resistance for reference temp.";
...
end TempResistor;
```

### 2.3 Identifiers, Names, and Keywords

*식별자*는 언어에서 다양한 항목의 이름을 지정하는 데 사용되는 문자, 숫자 및 밑줄과 같은 기타 문자의 시퀀스입니다. 특정 문자 조합은 Modelica 문법에서 예약어로 표시되는 키워드이므로 식별자로 사용할 수 없습니다.

#### 2.3.1 Identifiers

클래스, 변수, 상수 및 기타 항목의 이름을 지정하는 데 사용되는 Modelica *식별자*는 두 가지 형식이 있습니다. 첫 번째 형식은 항상 문자 또는 밑줄(_)로 시작하고 그 뒤에 임의의 갯수의 문자, 숫자 또는 밑줄이 오며, 대소문자를 구분합니다. 즉, `Inductor`와 `inductor`의 이름이 다릅니다. 두 번째 형식(`Q-IDENT`)은 작은 따옴표로 시작하고 그 뒤에 인쇄 가능한 ASCII 문자 시퀀스가 옵니다(예를 들면 '`12H`', '`13\'H`', '`+foo`'). 따옴표로 묶인 식별자의 제어 문자는 문자열 이스케이프를 사용해야 합니다. 작은 따옴표는 식별자의 일부입니다. 즉, `'x'`와 `x`는 고유 식별자입니다. 다음 BNF와 유사한 규칙은 Modelica 식별자를 정의합니다. 여기서 중괄호 `{}`는 반복이 0회 이상이고 수직 막대 `|`는 대안을 나타냅니다. Modelica 구문 및 어휘 단위에 대한 전체 BNF 정의는 부록 B에서 확인할 수 있습니다.

```
IDENT    = NONDIGIT { DIGIT | NONDIGIT } | Q-IDENT
Q-IDENT  = "’" { Q-CHAR | S-ESCAPE } "’"
NONDIGIT = "_" | letters "a" to "z" | letters "A" to "Z"
DIGIT    = 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
Q-CHAR   = NONDIGIT | DIGIT | "!" | "#" | "$" | "%" | "&" | "(" | ")" | "*" | "+" | "," |
"-" | "." | "/" | ":" | ";" | "<" | ">" | "=" | "?" | "@" | "[" | "]" | "^" |
"{" | "}" | "|" | "~" | " "_
S-ESCAPE = "\’" | "\"" | "\?" | "\\" | "\a" | "\b" | "\f" | "\n" | "\r" | "\t" | "\v"
```

#### 2.3.2 Names

*이름*은 특정 해석이나 의미를 가진 식별자입니다. 예를 들어, 이름은 `Integer` 변수, `Real` 변수, 함수, 유형 등을 나타낼 수 있습니다. 이름은 코드의 다른 부분, 즉 다른 범위에서 다른 의미를 가질 수 있습니다. 식별자를 이름으로 해석하는 방법은 5장에서 자세히 설명합니다. 패키지 이름의 의미는 13장에서 자세히 설명합니다.

#### 2.3.3 Modelica Keywords

다음 Modelica `키워드`는 예약어이며 부록 B.1에 나열된 경우를 제외하고 식별자로 사용할 수 없습니다.

|               |              |          |           |             |
| ------------- | ------------ | -------- | --------- | ----------- |
| algorithm     | discrete     | false    | model     | redeclare   |
| and           | each         | final    | not       | replaceable |
| annotation    | else         | flow     | operator  | return      |
|               | elseif       | for      | or        | stream      |
| block         | elsewhen     | function | outer     | then        |
| break         | encapsulated | if       | output    | true        |
| class         | end          | import   | package   | type        |
| connect       | enumeration  | in       | parameter | when        |
| connector     | equation     | initial  | partial   | while       |
| constant      | expandable   | inner    | protected | within      |
| constrainedby | extends      | input    | public    |             |
| der           | external     | loop     | record    |             |

### 2.4 Literal Constants

리터럴 상수는 유형에 따라 다른 형식을 갖는 명명되지 않은 상수입니다. Modelica의 사전 정의된 각 유형에는 해당 유형의 명명되지 않은 상수를 표현하는 방법이 있으며, 이는 이어지는 하위 섹션에 표시됩니다. 또한 배열 리터럴 및 레코드 리터럴을 표현할 수 있습니다.

#### 2.4.1 Floating Point Numbers

부동 소수점 숫자는 선택적으로 소수점이 뒤따르고 선택적으로 지수가 뒤따르는 10진수 시퀀스의 형태로 10진수로 표현됩니다. 하나 이상의 숫자가 있어야 합니다. 지수는 E 또는 e로 표시되고 그 뒤에 선택적 기호(+ 또는 -)와 하나 이상의 십진수가 표시됩니다. 최소 권장 범위는 IEEE 배정밀도 부동 소수점 수의 범위로, 표현 가능한 가장 큰 양수는 1.7976931348623157E + 308이고 가장 작은 양수는 2.2250738585072014E - 308입니다. 예를 들어 다음은 부동 소수점 숫자 리터럴 상수입니다.

```
22.5, 3.141592653589793, 1.2E-35
```

동일한 부동 소수점 수를 다른 리터럴로 나타낼 수 있습니다. 예를 들어 다음 리터럴은 모두 동일한 숫자를 나타냅니다.

```
13., 13E0, 1.3e1, 0.13E2
```

#### 2.4.2 Integer Literals

`Integer` 유형의 리터럴은 10진수 시퀀스입니다. 정수 `33, 0, 100, 30030044`와 같습니다. [*음수는 단항 빼기로 구성되며 정수 리터럴이 뒤따릅니다.*] 최소 권장 숫자 범위는 2의 보수 32비트 정수 구현의 경우 -2147483648에서 +2147483647입니다.

#### 2.4.3 Boolean Literals

두 개의 `Boolean` 리터럴 값은 `true`와 `false`입니다.

#### 2.4.4 Strings

문자열 리터럴은 큰따옴표 사이에 나타납니다. 새 줄을 포함하여 큰따옴표(") 및 백슬래시(\\)를 제외한 Modelica 언어 문자 집합의 모든 문자(허용되는 문자는 부록 B.1 참조)는 이스케이프 코드를 사용하지 않고 문자열에 *직접*  포함될 수 있습니다. 문자열 리터럴의 문자는 이스케이프 코드를 사용하여 나타낼 수 있습니다. 즉, 문자열 내에서 문자 앞에 백슬래시(\\)가 있습니다. 이러한 문자는 다음과 같습니다.

```
\'    single quote--may also appear without backslash in string constants.
\"    double quote
\?    question-mark--may also appear without backslash in string constants.
\\    backslash itself
\a    alert (bell, code 7, ctrl-G)
\b    backspace (code 8, ctrl-H)
\f    form feed (code 12, ctrl-L)
\n    new-line (code 10, ctrl-J)
\r    return (code 13, ctrl-M)
\t    horizontal tab (code 9, ctrl-I)
\v    vertical tab (code 11, ctrl-K)
```

예를 들어, 탭을 포함하는 문자열 리터럴, `This is`, 큰따옴표, 공백, `between`, 큰따옴표, 공백, `us` 및 개행은 다음과 같이 나타납니다.

```
"\tThis is\" between\" us\n"
```

특정 상황에서 문자열 리터럴의 연결(Modelica 문법 참조)은 Modelica에서 + 연산자로 표시됩니다. "a" + "b"는 "ab"가 됩니다. 여러 줄에 작성해야 하는 긴 문자열 리터럴을 표현하는 데 유용합니다.

[파일 내용이 Modelica 문자열로 읽혀지면 읽기 기능이 파일의 다른 줄 끝 기호를 처리하는 역할을 한다고 가정합니다(예: Linux 시스템에서 끝에 "개행" 문자가 있어야 함). 줄 및 Windows 시스템에서는 "개행" 및 "캐리지 리턴" 문자를 갖습니다. 프로그래밍 언어에서 평소와 같이 Modelica 문자열의 파일 내용에는 "개행" 문자만 포함됩니다.
모델 문서를 저장하기 위한 "info" 주석과 같은 긴 문자열 주석의 경우 문서의 모든 라인에 문자열 연결 연산자를 사용해야 한다면 매우 불편할 것입니다. Modelica 도구는 문자열 리터럴을 검색하거나 편집할 때 인쇄할 수 없는 "개행" 문자를 지원한다고 가정합니다. 예를 들어 다음 명령문은 (인쇄할 수 없는) 개행 문자를 포함하는 하나의 문자열을 정의합니다.]

```
assert(noEvent(length > s_small), "
The distance between the origin of frame_a and the origin of frame_b
of a LineForceWithMass component became smaller as parameter s_small
(= a small number, defined in the \"Advanced\" menu). The distance is
set to s_small, although it is smaller, to avoid a division by zero
when computing the direction of the line force.", level = AssertionLevel.warning);
```

### 2.5 Operator Symbols

사전 정의된 연산자 기호는 부록 B에 공식적으로 정의되어 있으며 섹션 3.2의 연산자 표에 요약되어 있습니다.