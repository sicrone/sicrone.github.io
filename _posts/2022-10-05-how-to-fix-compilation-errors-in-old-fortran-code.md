---
title: "예전 Fortran 코드 컴파일 시 발생하는 오류 해결 방법" 
excerpt: "이전에 작성되어 아무런 문제 없이 돌아가던 Fortran 코드를 Intel Fortran Compiler에서 컴파일할 경우 발생하는 구문 오류를 해결하는 방법을 설명합니다."
show_date: true
read_time: true

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "##93F7F2"

categories: 
- coding

tags: 
- fortran
- compile error
- intel fortran compiler
- error 6633
- error 6634
- error 7983
- error 7836

---

오래전에 작성되어 아무런 문제없이 잘 돌아가던 Fortran 소스를 다시 사용하려고 최신 버전의 [Intel® Fortran Compiler](https://software.intel.com/content/www/us/en/develop/tools/oneapi/components/fortran-compiler.html#gs.av5o7k)를 이용하여 컴파일할 경우 여러가지 구문 관련 에러가 발생하는 경우가 많습니다. 대개는 과거의 Fortran 구문과 현재 사용하는 Fortran 구문과의 차이로 인해 발생하는 문법 검사 과정에서 발생하는 경우가 많습니다. 이와 관련하여 대표적으로 발생하는 에러들은 아래와 같습니다.

> **error #6633**: The type of the actual argument differs from the type of the dummy argument.
> 
> **error #6634**: The shape matching rules of actual arguments and dummy arguments have been violated.
> 
> **error #7983**: The storage extent of the dummy argument exceeds that of the actual argument.
> 
> **error #7836**: If the actual argument is scalar, the corresponding dummy argument shall be scalar unless the actual argument is an element of an array that is not an assumed shape or pointer array, or a substring of such an element.

Intel Fortran Compiler를 설치할 경우 기본적으로 [Visual Studio Shell](https://docs.microsoft.com/ko-kr/visualstudio/extensibility/internals/visual-studio-shell?view=vs-2019)이 함께 설치되며, 이러한 경우 대부분은 Visual Studio 내 Project 설정을 변경함으로써 해결이 가능합니다.

> **Project -> Properties -> Configuration Properties -> Fortran ->Diagnostics -> Check routine interfaces** : **No**로 변경!!!

위와 같이 설정을 변경했음에도 실행 시 아래와 같은 에러가 발생한다면 다음과 같이 Project 설정을 추가로 변경하면 해결이 가능합니다.

> forrtl: severe <408>: fort: <2>: Subscript #1 of the array C1 has value 18 which is greater than the upper bound of 9

> **Project -> Properties -> Configuration Properties -> Fortran ->Run-time -> Check Array and String Bounds** : **No**로 변경!!!
