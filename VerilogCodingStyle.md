# lowRISC Verilog 코딩 스타일 가이드

## Basics

### Summary

Verilog는 lowRISC 호환 IP를 위한 주요 논리 설계 언어입니다.

Verilog 및 SystemVerilog(이 문서에서 일반적으로 "Verilog"라고 함)는 매우 다른 스타일로 작성할 수 있으며, 이로 인해 코드 충돌 및 코드 검토 지연이 발생할 수 있습니다. 이 스타일 가이드는 그룹 간에 Verilog 가독성을 높이는 것을 목표로 합니다. [Google C++ 스타일 가이드](https://google.github.io/styleguide/cppguide.html) 를 인용하자면 "일반적이고 필요한 관용구와 패턴을 만들면 코드를 훨씬 더 쉽게 이해할 수 있습니다."

이 가이드는 Verilog의 Comportable 스타일을 정의합니다. 목표는 다음과 같습니다.

- 하드웨어 개발 프로젝트 전반에 걸쳐 일관성 촉진
- 모범 사례 홍보
- 코드 공유 및 재사용 증가

이 스타일 가이드는 Verilog-2001 및 SystemVerilog 호환 코드 모두에 대한 스타일을 정의합니다. 또한 이 스타일 가이드는 합성 가능한 코드와 테스트 벤치 코드 모두에 대한 스타일을 정의합니다.

이 스타일 가이드의 요약된 표 표현은 [부록](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#appendix---condensed-style-guide) 을 참조하십시오.



**Table of Contents**

- lowRISC Verilog Coding Style Guide
  - Basics
    - [Summary](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#summary)
    - [Terminology Conventions](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#terminology-conventions)
    - [Default to C-like Formatting](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#default-to-c-like-formatting)
    - [Style Guide Exceptions](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#style-guide-exceptions)
    - [Which Verilog to Use](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#which-verilog-to-use)
  - Verilog/SystemVerilog Conventions
    - [Summary](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#summary-1)
    - [File Extensions](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#file-extensions)
    - General File Appearance
      - [Characters](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#characters)
      - [POSIX File Endings](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#posix-file-endings)
      - [Line Length](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#line-length)
      - [No Tabs](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#no-tabs)
      - [No Trailing Spaces](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#no-trailing-spaces)
    - [Begin / End](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#begin--end)
    - Indentation
      - [Indented Sections](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#indented-sections)
      - [Line Wrapping](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#line-wrapping)
      - [Preprocessor Directives](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#preprocessor-directives)
    - Spacing
      - [Comma-delimited Lists](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#comma-delimited-lists)
      - [Tabular Alignment](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#tabular-alignment)
      - [Expressions](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#expressions)
      - [Array Dimensions in Declarations](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#array-dimensions-in-declarations)
      - [Parameterized Types](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#parameterized-types)
      - [Labels](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#labels)
      - [Case items](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#case-items)
      - [Function And Task Calls](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#function-and-task-calls)
      - [Macro Calls](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#macro-calls)
      - [Line Continuation](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#line-continuation)
      - [Space Around Keywords](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#space-around-keywords)
    - Parentheses
      - [Ternary Expressions](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#ternary-expressions)
    - [Comments](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#comments)
    - [Declarations](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#declarations)
    - [Basic Template](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#basic-template)
  - Naming
    - [Summary](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#summary-2)
    - Constants
      - [Parameterized Objects (modules, etc.)](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#parameterized-objects-modules-etc)
    - [Macro Definitions](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#macro-definitions)
    - [Suffixes](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#suffixes)
    - [Enumerations](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#enumerations)
    - Signal Naming
      - [Use descriptive names](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#use-descriptive-names)
      - [Prefixes](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#prefixes)
      - [Hierarchical consistency](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#hierarchical-consistency)
    - [Clocks](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#clocks)
    - [Resets](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#resets)
  - Language Features
    - [Preferred SystemVerilog Constructs](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#preferred-systemverilog-constructs)
    - [Package Dependencies](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#package-dependencies)
    - [Module Declaration](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#module-declaration)
    - [Module Instantiation](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#module-instantiation)
    - [Constants](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#constants-1)
    - Signal Widths
      - [Always be explicit about the widths of number literals.](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#always-be-explicit-about-the-widths-of-number-literals)
      - [Port connections on module instances must always match widths correctly.](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#port-connections-on-module-instances-must-always-match-widths-correctly)
      - [Do not use multi-bit signals in a boolean context.](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#do-not-use-multi-bit-signals-in-a-boolean-context)
      - [Bit Slicing](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#bit-slicing)
      - [Handling Width Overflow](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#handling-width-overflow)
    - [Blocking and Non-blocking Assignments](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#blocking-and-non-blocking-assignments)
    - [Delay Modeling](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#delay-modeling)
    - [Sequential Logic (Latches)](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#sequential-logic-latches)
    - [Sequential Logic (Registers)](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#sequential-logic-registers)
    - Don't Cares (`X`'s)
      - [Catching errors where invalid values are consumed](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#catching-errors-where-invalid-values-are-consumed)
      - [Specific Guidance on Case Statements and Ternaries](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#specific-guidance-on-case-statements-and-ternaries)
      - [Dynamic Array Indexing](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#dynamic-array-indexing)
    - [Combinational Logic](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#combinational-logic)
    - Case Statements
      - [Wildcards in case items](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#wildcards-in-case-items)
    - [Generate Constructs](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#generate-constructs)
    - [Signed Arithmetic](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#signed-arithmetic)
    - [Number Formatting](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#number-formatting)
    - [Functions and Tasks](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#functions-and-tasks)
    - Problematic Language Features and Constructs
      - [Floating begin-end blocks](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#floating-begin-end-blocks)
      - [Hierarchical references](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#hierarchical-references)
  - Design Conventions
    - [Summary](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#summary-3)
    - [Declare all signals](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#declare-all-signals)
    - [Use `logic` for synthesis](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#use-logic-for-synthesis)
    - [Logical vs. Bitwise](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#logical-vs-bitwise)
    - [Packed Ordering](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#packed-ordering)
    - [Unpacked Ordering](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#unpacked-ordering)
    - [Finite State Machines](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#finite-state-machines)
    - [Active-Low Signals](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#active-low-signals)
    - [Differential Pairs](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#differential-pairs)
    - [Delays](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#delays)
    - [Wildcard import of packages](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#wildcard-import-of-packages)
    - Assertion Macros
      - [A Note on Security Critical Applications](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#a-note-on-security-critical-applications)
  - Appendix - Condensed Style Guide
    - [Basic Style Elements](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#basic-style-elements)
    - [Construct Naming](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#construct-naming)
    - [Suffixes for signals and types](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#suffixes-for-signals-and-types)
    - [Language features](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#language-features-1)



### Terminology Conventions

달리 명시되지 않는 한 다음 용어 규칙이 이 스타일 가이드에 적용됩니다.

- ***must***는 필수 요구 사항을 나타냅니다. 마찬가지로, ***do not***은 금지를 나타냅니다. 명령 및 선언문은 ***must***에 대응합니다 .
- ***recommended***라는 단어는 특정 작업 과정이 선호되거나 가장 적합함을 나타냅니다. 마찬가지로 ***not recommended*** 는 조치가 부적절하지만 금지되지는 않음을 나타냅니다. 다른 옵션을 사용해야 하는 이유가 있을 수 있지만 그렇게 하는 의미와 이유를 완전히 이해해야 합니다.
- ***may*** 단어는 작업 과정이 허용되고 선택 사항임을 나타냅니다.
- ***can*** 이라는 단어 는 물질적, 물리적 또는 인과적 제약이 주어지면 행동 과정이 가능함을 나타냅니다.

### Default to C-like Formatting

***[https://google.github.io/styleguide/cppguide.html](https://google.github.io/styleguide/cppguide.html) 과 일치하는 형식 코드***

Verilog는 C와 유사한 언어이며 적절한 경우 기본적으로 [Google의 C++ 스타일 가이드](https://google.github.io/styleguide/cppguide.html) 와 일치 합니다.

특히 다음과 같은 특정 형식 지정 지침을 상속합니다.

- 일반적으로 [이름](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#naming)은 설명적이어야 하며 약어는 피해야 합니다.
- ASCII가 아닌 문자는 사용할 수 없습니다.
- 들여쓰기는 탭이 아닌 공백을 사용합니다. 들여쓰기는 중첩을 위한 2칸, 줄 연속을 위한 4칸입니다.
- [조건식](https://google.github.io/styleguide/cppguide.html#Conditionals) `if` 에서 와 괄호 사이에 공백을 둡니다 .
- 연산자 주위에 수평 공백을 사용하고 줄 끝에서 후행 공백을 피하십시오.
- 일관되고 좋은 [구두점, 맞춤법 및 문법](https://google.github.io/styleguide/cppguide.html#Punctuation,_Spelling_and_Grammar) (주석 내)을 유지합니다.
- [TODO](https://google.github.io/styleguide/cppguide.html#TODO_Comments) 및 [사용 중단](https://google.github.io/styleguide/cppguide.html#Deprecation_Comments) 에 대한 C와 같은 형식을 포함하여 [주석](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#comments) 에 표준 형식을 사용 합니다.

### Style Guide Exceptions

***주석으로 모든 예외를 정당화하십시오.***

완벽한 스타일 가이드는 없습니다. 작업 설계로 가는 가장 좋은 방법이나 도구 문제를 해결하기 위한 가장 좋은 방법은 단순히 Gordian Knot을 잘라내고 이 스타일 가이드와 상충하는 코드를 만드는 것입니다. 적절한 경우 Lint waiver pragma뿐만 아니라 간략한 설명으로 그 필요성이 명확하게 정당화되는 한 필요에 따라 스타일 가이드에서 벗어나는 것은 항상 괜찮습니다.

### Which Verilog to Use

***SystemVerilog-2017을 선호합니다.***

모든 RTL 및 테스트는 [금지된 기능](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#problematic-language-features-and-constructs) 을 제외하고 [IEEE 1800-2017(SystemVerilog-2017) 표준](https://ieeexplore.ieee.org/document/8299595)에 따라 SystemVerilog에서 개발되어야 합니다.

표준 문서는 [IEEE GET](https://ieeexplore.ieee.org/browse/standards/get-program/page/series?id=80) 을 통해 무료로 제공됩니다 (등록 필요).

## Verilog/SystemVerilog Conventions

### Summary

이 섹션은 주로 스타일의 미적 측면(줄 길이, 들여쓰기, 간격 등)을 다룹니다.

### File Extensions

*** SystemVerilog 파일(또는 `.svh`전처리기를 통해 포함된 파일)에  `.sv` 확장자를 사용하십시오 .***

파일 확장자의 의미는 다음과 같습니다.

- `.sv`는 모듈 또는 패키지를 정의하는 SystemVerilog 파일을 나타냅니다.
- `.svh`는 전처리기 지시문 ``include`를 사용하여 다른 파일에 포함하려는 SystemVerilog 헤더 파일을 나타냅니다 .
- `.v`는 모듈 또는 패키지를 정의하는 Verilog-2001 파일을 나타냅니다.
- `.vh`는 Verilog-2001 헤더 파일을 나타냅니다.

`.sv` 및  `.v` 파일 만 컴파일 단위로 사용됩니다. `.svh` 및  `.vh`  파일은 파일은 다른 파일 내로만  ``include`-ed 될 수 있습니다.

netlist 파일을 제외하고 각 `.sv` 또는 `.v` 파일에는 하나의 모듈만 포함되어야 하며 이름이 연결되어야 합니다. 예를 들어 파일 `foo.sv`에는 `foo` 모듈만 포함되어야 합니다.

### General File Appearance

#### Characters

***UNIX 스타일의 줄 끝( `"\n"`)이 있는 ASCII 문자만 사용하십시오.***

#### POSIX File Endings

***비어 있지 않은 파일의 모든 줄은 줄 바꿈(`"\n"` )으로 끝나야 합니다.***

#### Line Length

***한 줄에 100자로 코드를 래핑합니다.***

스타일 호환 Verilog 코드의 최대 줄 길이는 줄당 100자입니다.

예외:

- 줄 바꿈이 불가능한 모든 위치(예: 포함 경로가 100자를 초과할 수 있음).

[줄 바꿈](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#line-wrapping) 에는 긴 줄을 줄 바꿈하는 방법에 대한 추가 지침이 포함되어 있습니다.

#### No Tabs

***어디에서나 탭을 사용하지 마십시오.***

공백을 사용하여 텍스트를 들여쓰거나 정렬합니다. [들여](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#indentation) 쓰기 및 줄 바꿈에 대한 규칙은 들여 쓰기를 참조하세요 .

파일에서 탭을 공백으로 변환하려면 [UNIX `확장`](http://linux.die.net/man/1/expand)  유틸리티를 사용할 수 있습니다.

#### No Trailing Spaces

***줄 끝에서 후행 공백을 삭제합니다.***

### Begin / End

***전체 문이 한 줄에 맞지 않으면 `begin`과 `end`를 사용 합니다.***

구문이 블록 경계에서 줄 바꿈되면 `begin`과 `end`를 사용해야 합니다. 전체 세미콜론으로 끝나는 문장이 한 줄에 맞는 경우에만 `begin`과 `end`를 생략할 수 있습니다.

👍

```verilog
// 래핑된 절차 블록에는 begin과 end가 필요합니다.
always_ff @(posedge clk) begin
  q <= d;
end
```

👍

```verilog
// 전체 구조가 한 줄에 맞기 때문에 begin과 end가 생략될 수 있는 예외 경우입니다.
always_ff @(posedge clk) q <= d;
```

👎

```verilog
// 래핑된 문에는 begin과 end가 있어야 하기 때문에 올바르지 않습니다.
always_ff @(posedge clk)
  q <= d;
```

`begin`은 앞의 키워드와 같은 줄에 있어야 하고 줄을 끝냅니다. `end`는 새 줄을 시작해야 합니다. `end else begin`은 한 줄에 함께 있어야 합니다. 유일한 예외는 `end`에 레이블이 있는 경우 `else` 다음이 새 줄에 있어야 한다는 것입니다.

👍

```verilog
// "end else begin"가 같은 줄에 있습니다..
if (condition) begin
  foo = bar;
end else begin
  foo = bum;
end
```

👍

```verilog
// begin/end는 각 세미콜론으로 끝나는 문장이 한 줄에 맞기 때문에 생략됩니다.
if (condition) foo = bar;
else foo = bum;
```

👎

```verilog
// "else"는 "end"와 같은 줄에 있어야 하므로 올바르지 않습니다.
if (condition) begin
  foo = bar;
end
else begin
  foo = bum;
end
```

👍

```verilog
// 레이블이 지정된 블록은 예외입니다.
if (condition) begin : a
  foo = bar;
end : a
else begin : b
  foo = bum;
end : b
```

위의 스타일은 case 문 내의 개별 item에도 적용됩니다. 전체 케이스 항목(케이스 표현식 및 관련 문)이 한 줄에 맞는 경우 `begin` 및 `end`를 생략할 수 있습니다. 그렇지 않으면 case 표현식과 같은 줄에 `begin` 키워드를 사용하십시오.

👍

```verilog
// 각 사례 항목에 대해 begin과 end을 일관되게 사용하는 것이 좋습니다.
unique case (state_q)
  StIdle: begin
    state_d = StA;
  end
  StA: begin
    state_d = StB;
  end
  StB: begin
    state_d = StIdle;
    foo = bar;
  end
  default: begin
    state_d = StIdle;
  end
endcase
```

👍

```verilog
// 한 줄에 맞는 케이스 항목은 begin과 end를 생략할 수 있습니다.
unique case (state_q)
  StIdle: state_d = StA;
  StA: state_d = StB;
  StB: begin
    state_d = StIdle;
    foo = bar;
  end
  default: state_d = StIdle;
endcase
```

👎

```verilog
unique case (state_q)
  StIdle:           // 시작과 끝을 사용하지 않고 블록 경계에서   
    state_d = StA;  // 케이스 항목을 래핑해서는 안 되므로 이 행은 올바르지 않습니다.
  StA:              // 케이스 항목은 한 줄에 맞아야 하며
    state_d = StB;  // 그렇지 않으면 절차 블록에 시작과 끝이 있어야 합니다.
  StB: begin
    foo = bar;
    state_d = StIdle;
  end
  default: begin
    state_d = StIdle;
  end
endcase
```

### Indentation

***들여쓰기는 레벨당 2칸입니다.***

들여쓰기에는 공백을 사용하세요. 탭을 사용하지 마십시오. 탭 키를 눌렀을 때 공백을 내보내도록 편집기를 설정해야 합니다.

#### Indented Sections

항상 짝을 이루는 모든 키워드의 포함된 섹션에 추가 수준의 들여쓰기를 추가하십시오. SystemVerilog 키워드 쌍의 예 : `begin / end`, `module / endmodule`, `package / endpackage`, `class / endclass`. `function / endfunction`

#### Line Wrapping

긴 표현식을 줄 바꿈할 때 표현식의 연속 부분을 다음과 같이 4칸 들여씁니다.

👍

```systemverilog
assign zulu = enabled && (
    alpha < bravo &&
    charlie < delta
);

assign addr = addr_gen_function_with_many_params(
    thing, other_thing, long_parameter_name, x, y,
    extra_param1, extra_param2
);

assign structure = '{
    src: src,
    dest: dest,
    default: '0
};
```

또는 가독성이 향상된다면 표현식의 연속 부분을 다음과 같이 그룹화 여는 괄호나 중괄호로 정렬합니다.

👍

```systemverilog
assign zulu = enabled && (alpha < bravo &&
                          charlie < delta);

assign addr = addr_gen_function(thing, other_thing,
                                long_parameter_name,
                                x, y);

assign structure = '{src: src,
                     dest: dest,
                     default: '0};
```

래핑된 표현식의 연산자는 각 줄의 끝이나 시작에 배치할 수 있지만 이는 파일 내에서 일관되게 수행되어야 합니다.

여러 줄 식의 한 줄을 끝내는 `{` 또는 `(` 같은 열린 구문 문자는 한 줄에 닫는 문자 (`}`, `)`)로 끝나야 합니다. 

예:

👍

```systemverilog
assign bus_concatenation = {
    bus_valid,
    bus_parity[7:0],
    bus_valid[63:0]
};

inst_type inst_name1 (
  .clk_i       (clk),
  .data_valid_i(data_valid),
  .data_value_i(data_value),
  .data_ready_o(data_ready)
);
```

#### Preprocessor Directives

***분기 전처리기 지시문을 왼쪽으로 정렬하고 들여쓰지 않은 상태로 유지합니다.***

중첩된 경우에도 분기 전처리기 지시문 (` 'ifdef` ,  `'ifndef`, `'else`, `'elsif`, `'endif`) 을 왼쪽으로 정렬합니다. `'endif` 전처리기 지시문이 없는 것처럼 텍스트의 조건부 분기를 들여씁니다. 비분기 전처리기 지시문은 일반 코드와 동일한 들여쓰기 규칙을 따라야 합니다.

👍

```systemverilog
package foo;
`ifdef FOO              // good: branching directive left-aligned
  `include "foo.sv";    // normal indentation for non-branching directives
  parameter bit A = 1;  // normal indentation for the regular code
`ifdef BAR              // good: branching directive left-aligned
  parameter bit A = 2;
`else
  parameter bit A = 3;
`endif
`endif
endpackage : foo
```

들여쓰기되지 않은 분기 전처리기 지시문은 읽기 흐름을 방해하여 조건부 텍스트가 있음을 강조합니다. 조건부 분기 텍스트를 들여쓰기하지 않은 상태로 두면 후처리된 텍스트가 제대로 들여쓰기된 것처럼 보입니다.

### Spacing

#### Comma-delimited Lists

***한 줄에 여러 항목이 있는 경우 하나의 공백으로 쉼표와 다음 문자를 구분해야 합니다.***

가독성을 위해 추가 공백이 허용됩니다.

👍

```systemverilog
bus = {addr, parity, data};
a = myfunc(lorem, ipsum, dolor, sit, amet, consectetur, adipiscing, elit,
           rhoncus);
mymodule mymodule(.a(a), .b(b));
```

👎

```systemverilog
{parity,data} = bus;
a = myfunc(a,b,c);
mymodule mymodule(.a(a),.b(b));
```

#### Tabular Alignment

tabular alignment는 두 개 이상의 유사한 선을 그룹화하여 동일한 부분이 서로 바로 위에 오도록 합니다. 이 정렬을 통해 행 간에 동일한 문자와 다른 문자를 쉽게 확인할 수 있습니다.

**일반적으로 tabular alignment를 사용하는 것이 좋습니다.**

**이 가이드의 해당 하위 섹션에 설명된 대로 일부 구성에는 tabular alignment를 사용해야 합니다.**

테이블 정렬이 필요한 구성:

- [모듈 인스턴스화의 포트 표현식](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#module-instantiation)

빈 줄로 구분된 각 코드 블록은 별도의 "테이블"로 처리됩니다.

탭이 아닌 공백을 사용하십시오.

예를 들어:

👍

```systemverilog
logic [7:0]  my_interface_data;
logic [15:0] my_interface_address;
logic        my_interface_enable;

logic       another_signal;
logic [7:0] something_else;
```

👍

```systemverilog
mod u_mod (
  .clk_i,
  .rst_ni,
  .sig_i          (my_signal_in),
  .sig2_i         (my_signal_out),
  // 빈 줄이 없는 주석은 블록을 유지합니다.
  .in_same_block_i(my_signal_in),
  .sig3_i         (something),

  .in_another_block_i(my_signal_in),
  .sig4_i            (something)
);
```

#### Expressions

***모든 이항 연산자의 양쪽에 공백을 포함합니다.***

이항 연산자 주위에 공백을 사용하십시오. 가독성을 돕기 위해 충분한 공백을 추가하십시오.

예를 들어:

👍

```systemverilog
assign a = ((addr & mask) == My_addr) ? b[1] : ~b[0];  // good
```

is better than

👎

```systemverilog
assign a=((addr&mask)==My_addr)?b[1]:~b[0];  // bad
```

**예외:** 비트 벡터를 선언할 때 압축 표기법을 사용할 수 있습니다. 예를 들어:

👍

```systemverilog
wire [WIDTH-1:0] foo;   // this is acceptable
wire [WIDTH - 1 : 0] foo;  // fine also, but not necessary
```

대체 표현식을 여러 줄로 분할할 때 동등한 if-then-else 줄과 유사한 형식을 사용하십시오. 예를 들어:

👍

```systemverilog
assign a = ((addr & mask) == `MY_ADDRESS) ?
           matches_value :
           doesnt_match_value;
```

#### Array Dimensions in Declarations

packed dimensions 주위에 공백을 추가합니다.

공백을 추가하지 마십시오:

- 식별자와 압축을 푼 치수 사이.
- 여러 차원 사이.

packed 및 unpacked 배열은 물론 dynamic arrays, associative arrays 및 queues에 적용됩니다.

👍

```systemverilog
logic [7:0][3:0] data[128][2];
typedef logic [31:0] word_t;
bit bit_array[512];
data_t some_array[];
data_t some_map[addr_t];
data_t some_q[$];
```

👎

```systemverilog
// There must not be a space between dimensions.
logic [7:0] [3:0] data[128] [2];
// There must be a space around packed dimensions.
typedef logic[31:0]word_t;
// There must not be a space between identifier and unpacked dimension.
bit bit_array [512];
// Dynamic, associative, and queue "dimensions" are treated the same as unpacked
// dimensions.  There must not be a space.
data_t some_array [];
data_t some_map [addr_t];
data_t some_q [$];
```

#### Parameterized Types

***유형이 규정된 이름의 일부인 경우를 제외하고 유형 매개변수 앞에 공백 하나를 추가하십시오.***

규정된 이름에는 해당 세그먼트를 연결하는 범위 연산자 `::`가 하나 이상 포함 됩니다. 규정된 이름(qualified name)의 공백은 한 기호에 대한 참조의 연속성을 깨뜨릴 수 있으므로 추가해서는 안 됩니다. 매개변수 목록은 [쉼표 뒤에 공백](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#comma-delimited-lists) 규칙 을 따라야 합니다 .

👍

```systemverilog
my_fifo #(.WIDTH(4), .DEPTH(2)) my_fifo_nibble ...

class foo extends bar #(32, 8);  // unqualified base class
  ...
endclass

foo_h = my_class#(.X(1), .Y(0))::type_id::create("foo_h");  // static method call

my_pkg::x_class#(8, 1) bar;  // package-qualified name
```

👎

```systemverilog
my_fifo#(.WIDTH(4), .DEPTH(2)) my_fifo_2by4 ...

class foo extends bar#(32, 8);  // unqualified base class
  ...
endclass

foo_h = my_class #(.X(1), .Y(0))::type_id::create("foo_h");  // static method call

my_pkg::x_class #(8, 1) bar;  // package-qualified name
```

#### Labels

***코드 블록에 레이블을 지정할 때 콜론 앞뒤에 하나의 공백을 추가하십시오.***

예를 들어:

👍

```systemverilog
begin : foo
end : foo
```

👎

```systemverilog
end:bar            // There must be a space before and after the colon.
endmodule: foobar  // There must be a space before the colon.
```

#### Case items

케이스 항목의 콜론 앞에 공백이 없어야 합니다. 케이스 항목의 콜론 뒤에는 하나 이상의 공백이 있어야 합니다.

`default` 케이스 항목에는 콜론이 포함되어야 합니다 .

예를 들어:

👍

```systemverilog
unique case (my_state)
  StInit:   $display("Shall we begin");
  StError:  $display("Oh boy this is Bad");
  default: begin
    my_state = StInit;
    interrupt = 1;
  end
endcase
```

👎

```systemverilog
unique case (1'b1)
  (my_state == StError)  : interrupt = 1; // Excess whitespace before colon
  default:begin end                       // Missing space after colon
endcase
```

#### Function And Task Calls

***함수 및 작업 호출은 함수 이름 또는 작업 이름과 여는 괄호 사이에 공백이 없어야 합니다.***

예를 들어:

👍

```systemverilog
process_packet(pkt);
```

👎

```systemverilog
process_packet (pkt);  // There must not be a space before "("
```

#### 매크로 호출

***매크로 호출은 매크로 이름과 여는 괄호 사이에 공백이 없어야 합니다.***

예를 들어:

👍

```systemverilog
`uvm_error(ID, "you fail")
`ASSERT(name, a & b, clk, rst)
```

👎

```systemverilog
`uvm_error (ID, "you fail")  // There must not be a space before "("
`ASSERT (name, a & b, clk, rst)
```

#### 라인 연속

***줄 연속을 오른쪽 정렬하는 것은 필수입니다.***

줄 연속(' `\ `' 문자)을 정렬하면 여러 줄 매크로의 끝을 시각적으로 표시하는 데 도움이 됩니다. 정렬 위치는 공백이 토큰을 분할하지 않을 때 다중 행 매크로의 가장 오른쪽 범위를 최소 한 공백 이상 벗어나야 하지만 최대 행 길이를 초과해서는 안 됩니다.

```systemverilog
`define REALLY_LONG_MACRO(arg1, arg2, arg3) \
    do_something(arg1);                     \
    do_something_else(arg2);                \
    final_action(arg3);
```

#### 키워드 주변 공백

***SystemVerilog 키워드 앞뒤에 공백을 포함하십시오.***

공백을 포함하지 마십시오.

- 여는 괄호와 같이 그룹 열기 바로 뒤에 오는 키워드 앞에
- 줄의 시작 부분에 있는 키워드 앞에 있습니다.
- 줄 끝에 있는 키워드 뒤에

예를 들어:

```systemverilog
// Normal indentation before if.  Include a space after if.
if (foo) begin
end
// Include a space after always, but not before posedge.
always_ff @(posedge clk) begin
end
```

### 괄호

***연산을 명확하게 하려면 괄호를 사용하십시오.***

합리적인 사람이 생각을 확장하거나 연산자 우선 순위 차트를 참조해야 하는 경우에는 대신 괄호를 사용하여 작업 순서를 모호하지 않게 만드십시오.

#### 삼항 표현식

***다른 삼항 표현식의 참 조건에 중첩된 삼항 표현식은 괄호로 묶어야 합니다.***

예를 들어:

👍

```systemverilog
assign foo = condition_a ? (condition_a_x ? x : y) : b;
```

다음 중첩 삼항은 컴파일러에게 단 하나의 의미를 갖지만 의미가 불분명하고 사람에게 오류가 발생하기 쉽습니다.

👎

```systemverilog
assign foo = condition_a ? condition_a_x ? x : y : b;
```

***예를 들어 우선 순위 mux를 설명할 때 코드 형식이 동일한 정보를 전달하는 경우 괄호를 생략할 수 있습니다.***

👍

```systemverilog
assign foo = condition_a ? a :
             condition_b ? b : not_a_nor_b;
```

### 코멘트

***C++ 스타일 주석( `// foo`)이 선호됩니다. C 스타일 주석( `/* bar */`)도 사용할 수 있습니다.***

자체 줄의 주석은 다음 코드를 설명합니다. 코드가 있는 줄의 주석은 해당 코드 줄을 설명합니다.

예를 들어:

```systemverilog
// This comment describes the following module.
module foo;
  ...
endmodule : foo

localparam bit ValBaz = 1;  // This comment describes the item to the left.
```

모듈 내에서 서로 다른 기능 부분(FSM, 기본 데이터 경로 또는 레지스터 등)을 분리하기 위해 헤더 스타일 주석을 사용하여 코드를 구조화하는 것이 때때로 유용할 수 있습니다. `//`이 경우 선호되는 스타일은 다음과 같이 C++ 스타일 주석으로 둘러싸인 한 줄 섹션 이름 입니다.

```systemverilog
module foo;

  ////////////////
  // Controller //
  ////////////////
  ...

  ///////////////////////
  // Main ALU Datapath //
  ///////////////////////
  ...

endmodule : foo
```

디자이너가 더 나은 가독성을 위해 특정 섹션의 시작/끝을 표시하기 위해 주석을 사용하려는 경우(예: 중첩 for 루프 블록에서) 선호되는 방법은 다음과 같이 추가 구분자가 없는 한 줄 주석을 사용하는 것입니다. 아래의 예.

👍

```systemverilog
// begin: iterate over foobar
for (...) begin
...
end
// end: iterate over foobar
```

👍

```systemverilog
for (...) begin // iterate over foobar
...
end // iterate over foobar
```

👎

```systemverilog
//-------------------------- iterate over foobar -------------------------------
for (...) begin
...
end
//-------------------------- iterate over foobar -------------------------------
```

👎

```systemverilog
///////////////////////////////
// begin iterate over foobar //
///////////////////////////////
for (...) begin
...
end
///////////////////////////////
// end iterate over foobar   //
///////////////////////////////
```

### 선언

***신호는 사용되기 전에 선언되어야 합니다. 이는 암시적 네트 선언을 사용하지 않아야 함을 의미합니다.***

모듈 내에서 신호, 유형, 열거형 및 localparams를 처음 사용할 때와 가깝게 선언하는 **것이 좋습니다 .** 이렇게 하면 판독기가 선언을 찾고 신호 유형을 더 쉽게 볼 수 있습니다.

### 기본 템플릿

***많은 항목을 보여주는 템플릿이 아래에 나와 있습니다.***

주형:

```systemverilog
// Copyright lowRISC contributors.
// Licensed under the Apache License, Version 2.0, see LICENSE for details.
// SPDX-License-Identifier: Apache-2.0
//
// One line description of the module

module my_module #(
  parameter Width = 80,
  parameter Height = 24
) (
  input              clk_i,
  input              rst_ni,
  input              req_valid_i,
  input  [Width-1:0] req_data_i,
  output             req_ready_o,
  ...
);

  logic [Width-1:0] req_data_masked;

  submodule u_submodule (
    .clk_i,
    .rst_ni,
    .req_valid_i,
    .req_data_i (req_data_masked),
    .req_ready_o(req_ready),
    ...
  );

  always_comb begin
    req_data_masked = req_data_i;
    case (fsm_state_q)
      ST_IDLE: begin
        req_data_masked = req_data_i & MASK_IDLE;
        ...
  end

  ...

endmodule
```

## 네이밍

### 요약

| 건설하다                                                     | 스타일                         |
| ------------------------------------------------------------ | ------------------------------ |
| 선언(모듈, 클래스, 패키지, 인터페이스)                       | `lower_snake_case`             |
| 인스턴스 이름                                                | `lower_snake_case`             |
| 신호(네트 및 포트)                                           | `lower_snake_case`             |
| 변수, 함수, 작업                                             | `lower_snake_case`             |
| 명명된 코드 블록                                             | `lower_snake_case`             |
| `매크로 정의                                                 | `ALL_CAPS`                     |
| 매개변수화된 모듈, 클래스 및 인터페이스에 대한 조정 가능한 매개변수 | `UpperCamelCase`               |
| 상수                                                         | `ALL_CAPS`또는`UpperCamelCase` |
| 열거 유형                                                    | `lower_snake_case_e`           |
| 기타 typedef 유형                                            | `lower_snake_case_t`           |
| 열거된 값 이름                                               | `UpperCamelCase`               |

### 상수

***프로젝트 패키지 파일의 매개변수를 사용하여 전역 상수를 선언합니다.***

이러한 맥락에서 **상수** 는 매개변수화된 모듈, 클래스 등과 같은 개체에 대한 조정 가능한 매개변수와 구별됩니다.

상수 유형을 명시적으로 선언합니다.

상수를 선언할 때:

- 패키지 내에서 사용 `parameter`.
- 모듈 또는 클래스 내에서 `localparam`.

상수를 정의하는 기본 방법은 `package`모든 상수를 `parameter`해당 패키지 내에서 선언하고 선언하는 것입니다. 상수가 하나의 파일에서만 사용되는 경우 별도의 패키지가 아닌 해당 파일 내에서 정의된 상태로 유지하는 것이 좋습니다.

프로젝트의 기본 패키지에서 프로젝트 전체 상수를 정의합니다.

`parameter`다른 패키지는 많은 프로젝트에서 재사용될 수 있는 IP 생성을 용이하게 하기 위해 고유한 상수로 선언될 수도 있습니다 .

모든 불변 상수에 대해 선호되는 명명 규칙은 를 사용하는 `ALL_CAPS`것이지만 의 사용이 `UpperCamelCase`더 자연스러운 것으로 간주되는 경우가 있습니다.

| 상수 유형              | 스타일 기본 설정               | Conversation                                                 |
| ---------------------- | ------------------------------ | ------------------------------------------------------------ |
| `정의하다              | `ALL_CAPS`                     | 정말 일정하다                                                |
| 모듈 매개변수          | `UpperCamelCase`               | 상수가 아닌 인스턴스화에 의해 진정으로 수정 가능             |
| 파생된 로컬 매개변수   | `UpperCamelCase`               | 직접 수정되지 않았지만 여전히 모듈 매개변수를 추적합니다.    |
| 조정 가능한 localparam | `UpperCamelCase`               | 최종 RTL 버전에서는 변경되지 않을 것으로 예상되지만 디자이너가 디자인 공간을 편리하게 탐색하기 위해 사용합니다. |
| 실제 localparam 상수   | `ALL_CAPS`                     | 예시`localparam OP_JALR = 8'hA0;`                            |
| 열거형 멤버 참 상수    | `ALL_CAPS`                     | 예시`typedef enum ... { OP_JALR = 8'hA0;`                    |
| 열거형 집합 멤버       | `ALL_CAPS`또는`UpperCamelCase` | 예 `typedef enum ... { ST_IDLE, ST_FRAME_START, ST_DYN_INSTR_READ ...`, `typedef enum ... { StIdle, StFrameStart, StDynInstrRead...`. 임의 값의 모음은 두 가지 규칙 중 하나일 수 있습니다. |

상수가 단위가 없거나 단위가 "비트"가 아닌 경우 상수의 단위는 기호 이름에 설명되어야 합니다. 예를 들어, `FooLengthBytes`.

예시:

👍

```verilog
// package-scope
package my_pkg;

  parameter int unsigned NUM_CPU_CORES = 64;
  // reference elsewhere as my_pkg::NUM_CPU_CORES

endpackage
```

#### 매개변수화된 객체(모듈 등)

***`parameter `매개변수화하고 `localparam`모듈 범위 상수를 선언하는 데 사용 합니다. 패키지 내에서 를 사용 `parameter`하십시오.***

설계 재사용을 용이하게 하기 위해 매개변수화된 모듈, 클래스 및 인터페이스를 생성할 수 있습니다.

사용자가 인스턴스화 시 조정할 것으로 예상되는 매개변수를 나타내려면 매개변수화된 모듈 선언 `parameter`내에서 키워드를 사용하십시오 . `module`모든 매개변수의 기본 명명 규칙은 입니다 `UpperCamelCase`. 일부 프로젝트는 `ALL_CAPS`조정 가능한 매개변수를 상수와 구별하는 데 사용할 수 있습니다.

선언 내의 파생 매개변수 `module`는 를 사용해야 합니다 `localparam`. 아래에 예가 나와 있습니다.

```verilog
module modname #(
  parameter  int Depth  = 2048,         // 8kB default
  localparam int Aw     = $clog2(Depth) // derived parameter
) (
  ...
);

endmodule
```

``define`모듈 을 `defparam`매개변수화하는 데 사용해서는 안 됩니다.

[패키지 매개변수](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#constants) 를 사용 하여 매개변수 대신 계층 구조를 통해 전역 상수를 전송합니다. 범위가 특정 SystemVerilog 모듈 내부에 있는 상수를 선언하려면 [대신 를 ](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#constants)[사용`localparam`](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#constants) 하십시오.

매개변수화된 모듈을 사용하는 경우의 예:

- 모듈의 여러 인스턴스가 인스턴스화되고 매개변수로 구별해야 하는 경우.
- 특정 버스 폭에 대한 모듈을 전문화하는 수단.
- 모듈 내에서 변경할 수 있는 전역 매개변수를 문서화하는 수단.

매개변수의 유형을 명시적으로 선언합니다.

법적 범위를 제한하는 데 도움이 되도록 매개변수 유형을 사용합니다. 예 를 들어, 부울 값 `int unsigned`의 경우 음이 아닌 일반 정수 값 입니다. `bit`조정 가능한 매개변수 값에 대한 추가 제한 사항은 어설션과 함께 문서화되어야 합니다.

조정 가능한 매개변수 값은 항상 합리적인 기본값을 가져야 합니다.

추가 정보는 [매개변수화된 모델 생성을 위한 새로운 Verilog-2001 기술을](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-884-complex-digital-systems-spring-2005/related-resources/parameter_models.pdf) 참조하십시오 .

### 매크로 정의

***매크로는 밑줄이 있는 ALL_CAPITALS여야 합니다.***

매크로는 밑줄이 있는 모두 대문자여야 합니다.

**전역 정의** 는 프로젝트의 모든 소스 파일이 공유하는 헤더 파일의 틱 정의 매크로입니다 . 네임스페이스 충돌을 줄이려면 전역 정의 앞에 관련 매크로 그룹의 이름이 접두사로 붙고 밑줄 쌍이 따라와야 합니다.

```verilog
// The following two constants are in the FOO namespace of the
// SN chip.
`define SN_FOO__ALPHA_BETA  5
`define SN_FOO__GAMMA_OMEGA 6
```

**로컬 정의** 는 단일 로컬 파일의 범위 내에서만 사용해야 하는 틱 정의 매크로입니다. 전역 매크로 네임스페이스를 오염시키지 않도록 사용 후에는 명시적으로 정의되지 않아야 합니다. 매크로가 로컬 범위에서만 사용됨을 나타내려면 매크로 이름 앞에 단일 밑줄을 붙여야 합니다.

로컬 정의가 로컬로 유지되도록 하려면 ``include`매크로 정의와 ``undef`.

예시:

```verilog
`define _MAKE_THING(_x) \
    thing i_thing_##_x (.clk(clk), .i(i##_x) .o(o##_x));
`_MAKE_THING(a)
`_MAKE_THING(b)
`_MAKE_THING(c)
`undef _MAKE_THING
```

### 접미사

접미사는 의도에 대한 지침을 제공하기 위해 여러 곳에서 사용됩니다. 다음 표에는 특별한 의미가 있는 접미사가 나열되어 있습니다.

| 접미사           | 투기장      | 의지                                                         |
| ---------------- | ----------- | ------------------------------------------------------------ |
| `_e`             | 형식 정의   | 열거형                                                       |
| `_t`             | 형식 정의   | 신호 클러스터를 포함한 기타 typedef                          |
| `_n`             | signal name | 활성 낮은 신호                                               |
| `_n`,`_p`        | 신호 이름   | 차동 쌍, 활성 낮음 및 활성 높음                              |
| `_d`,`_q`        | 신호 이름   | 레지스터의 입출력                                            |
| `_q2`, `_q3`등   | 신호 이름   | 신호의 파이프라인 버전 `_q`1주기의 대기 시간, `_q2`2주기, `_q3`3주기 등 |
| `_i`, `_o`,`_io` | 신호 이름   | 모듈 입력, 출력 및 양방향                                    |

여러 접미사가 필요한 경우 다음 지침을 사용하십시오.

- 안내 접미사는 추가 `_` 문자로 구분되지 않고 함께 추가됩니다( `_ni`not `_n_i`).
- 신호가 활성이면 로우 `_n`가 첫 번째 접미사가 됩니다.
- 신호가 모듈 입력/출력인 경우 문자가 마지막에 옵니다.
- `_d`전파 하고 `_q`모듈 경계에 필수는 아닙니다 .

예시:

👍

```verilog
module simple (
  input        clk_i,
  input        rst_ni,              // Active low reset

  // writer interface
  input [15:0] data_i,
  input        valid_i,
  output       ready_o,

  // bi-directional bus
  inout [7:0]  driver_io,         // Bi directional signal

  // Differential pair output
  output       lvds_po,           // Positive part of the differential signal
  output       lvds_no            // Negative part of the differential signal
);

  logic valid_d, valid_q, valid_q2, valid_q3;
  assign valid_d = valid_i; // next state assignment

  always_ff @(posedge clk or negedge rst_ni) begin
    if (!rst_ni) begin
      valid_q  <= '0;
      valid_q2 <= '0;
      valid_q3 <= '0;
    end else begin
      valid_q  <= valid_d;
      valid_q2 <= valid_q;
      valid_q3 <= valid_q2;
    end
  end

  assign ready_o = valid_q3; // three clock cycles delay

endmodule // simple
```

### 열거

***이름 열거 유형 `snake_case_e`. 이름 열거형 값 `ALL_CAPS`또는 `UpperCamelCase`.***

항상 . `enum`_ `typedef`열거 유형의 스토리지 유형을 지정해야 합니다. 합성 가능한 열거형의 경우 스토리지 유형은 4-상태 데이터 유형이어야 합니다( `logic`보다는 `bit`).

익명 `enum`유형은 프로젝트 전체와 프로젝트 전체에서 다른 위치에서 유형을 사용하기 어렵게 만들기 때문에 허용되지 않습니다.

열거 유형 이름에는 소문자 영숫자 문자와 밑줄만 포함해야 합니다. 열거 유형 이름에 접미사를 붙여야 합니다 `_e`.

열거 값 이름(상수)은 일반적으로 `ALL_CAPS`예를 들어 `READY_TO_SEND`상수 특성을 반영해야 하며, 특히 정의된 opcode 할당과 같이 변경할 수 없는 값의 경우에는 더욱 그렇습니다. `UpperCamelCase` 열거형의 할당된 값이 상태 머신 값과 같이 디자이너에게 실질적으로 신경 쓰지 않는 경우가 선호될 수 있습니다 . 이 권장 사항을 생각하는 방법에 대한 토론은 [상수](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#constants) 에 대한 대화를 참조하십시오 .

👍

```verilog
typedef enum logic [7:0] {  // 8-bit opcodes
  OP_JALR = 8'hA0,
  OP_ADDI = 8'h47,
  OP_LDW  = 8'h0B
} opcode_e;
opcode_e op_val;
```

👍

```verilog
typedef enum logic [1:0] {  // A 2-bit enumerated type
  ACC_WRITE,
  ACC_READ,
  ACC_PAUSE
} access_e; // new named type is created
access_e req_access, resp_access;
```

👍

```verilog
typedef enum logic [1:0] {  // A 2-bit enumerated type
  AccWrite,
  AccRead,
  AccPause
} access_e; // new named type is created
access_e req_access, resp_access;
```

👎

```verilog
enum {  // Typedef is missing, storage type is missing.
  Write,
  Read
} req_access, resp_access; // anonymous enum type
```

### 신호 명명

***`lower_snake_case`신호에 이름을 지정할 때 사용 합니다.***

이 맥락에서 **신호** 는 SystemVerilog 설계 내의 네트, 변수 또는 포트를 의미합니다.

신호 이름에는 소문자 영숫자 문자와 밑줄이 포함될 수 있습니다.

신호 이름은 밑줄 뒤에 숫자가 오는 것으로 끝나지 않아야 합니다(예: `foo_1`, `foo_2`등). 많은 합성 도구는 해당 명명 규칙을 사용하여 버스를 네트에 매핑하므로 유사하게 명명된 네트는 합성 네트리스트를 검사할 때 혼동을 초래할 수 있습니다.

예약 된 [Verilog](http://www.xilinx.com/support/documentation/sw_manuals/xilinx13_1/ite_r_verilog_reserved_words.htm) 또는 SystemVerilog 키워드는 이름으로 사용할 수 없습니다.

다른 언어와 상호 운용할 때 다른 언어의 키워드를 사용하지 않도록 주의하십시오.

#### 설명이 포함된 이름 사용

***이름은 신호의 목적이 무엇인지 설명해야 합니다.***

전체 단어를 사용하십시오. 가장 흔한 장소를 제외하고는 약어와 축약어를 피하십시오. 간결함보다 설명적인 신호 이름을 선호합니다.

#### 접두사

공통 접두사를 사용하여 함께 작동하는 신호 그룹을 식별합니다. 예를 들어, AXI-S 인터페이스의 모든 요소는 접두사를 공유합니다: `foo_valid`, `foo_ready`및 `foo_data`.

또한 다중 클럭이 있는 모듈에 대해 어떤 신호가 어떤 클럭 그룹에 있는지 명확하게 레이블을 지정하려면 접두사를 사용해야 합니다. [자세한 내용은 시계 도메인](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#clocks) 섹션을 참조하세요.

예:

- 블록램 제어와 관련된 신호는 `bram_`접두사를 공유할 수 있습니다.
- 동기식 신호 는 `clk_dram`접두사 `clk`를 공유해야 `dram_`합니다.

코드 예:

👍

```verilog
module fifo_controller (
  input         clk_i,
  input         rst_ni,

  // writer interface
  input [15:0]  wr_data_i,
  input         wr_valid_i,
  output        wr_ready_o,

  // reader interface
  output [15:0] rd_data_o,
  output        rd_valid_o,
  output [7:0]  rd_fullness_o,
  input         rd_ack_i,

  // memory interface:
  output [7:0]  mem_addr_o,
  output [15:0] mem_wdata_o,
  output        mem_we_o,
  input  [15:0] mem_rdata_i
);
```

이 명명 규칙을 사용하면 간단하고 일관된 규칙을 사용하여 포트 이름을 유사한 신호 이름에 쉽게 매핑할 수 있습니다. [자세한 내용은 계층적 일관성](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#hierarchical-consistency) 섹션을 참조 하십시오.

#### 계층적 일관성

***동일한 신호는 계층 구조의 모든 수준에서 동일한 이름을 가져야 합니다.***

인스턴스의 포트에 연결하는 신호는 해당 포트와 이름이 같아야 합니다. 이런 식으로 진행하면 직접 연결된 신호는 계층 구조의 모든 수준에서 동일한 이름을 유지해야 합니다.

이 규칙에는 다음과 같은 예외가 예상됩니다.

- 신호 배열의 요소에 포트를 연결할 때.
- 일반 포트 이름을 디자인에 더 특정한 것으로 매핑할 때. 예를 들어, 두 개의 일반 블록(하나는 `host_bus`포트가 있고 다른 하나는 포트가 있음)은 신호 `device_bus`로 연결될 수 있습니다 .`foo_bar_bus`

각각의 예외적인 경우에 포트 이름과 신호 이름을 가능한 한 명확하고 일관성 있게 매핑하도록 주의해야 합니다.

### 시계

***모든 클럭 신호는 로 시작해야 합니다 `clk`.***

디자인에 대한 기본 시스템 시계의 이름은 `clk`. `clk`모듈의 대부분의 로직이 동기되는 기본 클럭을 참조하는 데 사용할 수 있습니다.

모듈에 여러 클록이 포함된 경우 시스템 클록이 아닌 클록은 고유 식별자로 이름을 지정하고 그 앞에 `clk_`접두사를 붙여야 합니다. 예: `clk_dram`, `clk_axi`, 등. 이 접두사는 해당 클록 도메인의 다른 신호를 식별하는 데 사용됩니다.

### 재설정

***리셋은 액티브 로우 및 비동기식입니다. 기본 이름은 `rst_n`입니다.***

칩 전체의 모든 재설정은 활성 낮음 및 비동기식으로 정의됩니다. 따라서 관련 표준 셀 레지스터의 비동기 리셋 입력에 연결된 것으로 정의됩니다.

기본 이름은 `rst_n`입니다. 시계로 구별해야 하는 경우 시계 이름이 와 같이 재설정 이름에 포함되어야 합니다 `rst_domain_n`.

SystemVerilog는 다음 구문 스타일 중 하나를 허용하지만 스타일 가이드는 전자를 선호합니다.

```verilog
// preferred
always_ff @(posedge clk or negedge rst_n) begin
  if (!rst_n) begin
    q <= 1'b0;
  end else begin
    q <= d;
  end
end

// legal but not preferred
always_ff @(posedge clk, negedge rst_n) begin
  if (!rst_n) begin
    q <= 1'b0;
  end else begin
    q <= d;
  end
end
```

## 언어 기능

### 선호하는 SystemVerilog 구성

Verilog-2001에 해당하는 대신 다음 SystemVerilog 구성을 사용하십시오.

- `always_comb`이상 필요합니다 `always @*`.
- `logic``reg`및 보다 선호 `wire`됩니다.
- 최상위 선언이 전역 `parameter`선언보다 선호 됩니다.` `define`

### 패키지 종속성

***패키지에는 순환 종속성이 없어야 합니다.***

패키지 파일은 다른 패키지 파일의 상수 및 유형에 종속될 수 있지만 순환 종속성이 없어야 합니다. 즉, 패키지 A가 패키지 B의 상수에 의존한다면, 패키지 B는 패키지 A의 어떤 것에도 의존하지 않아야 합니다. 순환 의존성은 SystemVerilog 언어 사양에 의해 허용되지만, 그것들을 사용하면 일부 도구가 손상될 수 있습니다.

예를 들어:

```verilog
package foo;

  // Package "bar" must not depend on anything in "foo":
  parameter int unsigned PageSizeBytes = 16 * bar::Kibi;

endpackage
```

### 모듈 선언

***Verilog-2001 전체 포트 선언 스타일을 사용하고 아래 형식을 사용합니다.***

Verilog-2001 결합된 포트 및 I/O 선언 스타일을 사용합니다. Verilog-95 목록 스타일을 사용하지 마십시오. 모듈 문에서 포트 선언은 포트 이름, 유형 및 방향을 완전히 선언해야 합니다.

여는 괄호는 모듈 선언과 같은 줄에 있어야 하며 첫 번째 포트는 다음 줄에 선언되어야 합니다.

닫는 괄호는 열 0의 자체 줄에 있어야 합니다.

모듈 선언을 위한 들여쓰기는 두 개의 공백 들여쓰기의 표준 들여쓰기 규칙을 따릅니다.

클럭 포트는 포트 목록에서 먼저 선언되어야 하며 그 다음에 모든 리셋 입력이 따라와야 합니다.

매개변수가 없는 예:

👍

```verilog
module foo (
  input              clk_i,
  input              rst_ni,
  input [7:0]        d_i,
  output logic [7:0] q_o
);
```

매개변수가 있는 예:

👍

```verilog
module foo #(
  parameter int unsigned Width = 8,
) (
  input                    clk_i,
  input                    rst_ni,
  input [Width-1:0]        d_i,
  output logic [Width-1:0] q_o
);
```

Verilog-95 스타일을 사용하지 마십시오.

👎

```verilog
// WRONG:
module foo(a, b, c d);
input wire [2:0] a;
output logic b;
...
```

### 모듈 인스턴스화

***명명된 포트를 사용하여 모든 인스턴스화를 완전히 지정합니다.***

인스턴스화를 위해 신호를 포트에 연결할 때 다음과 같이 명명된 포트 스타일을 사용합니다.

```verilog
my_module i_my_instance (
  .clk_i (clk_i),
  .rst_ni(rst_ni),
  .d_i   (from_here),
  .q_o   (to_there)
);
```

포트와 연결 신호의 이름이 같으면 `.port`괄호 없이 구문을 사용하여 연결을 나타낼 수 있습니다. 예를 들어:

```verilog
my_module i_my_instance (
  .clk_i,
  .rst_ni,
  .d_i   (from_here),
  .q_o   (to_there)
);
```

선언된 모든 포트는 인스턴스화 블록에 있어야 합니다. 연결되지 않은 출력은 명시적으로 연결되지 않음으로 작성되어야 하고(예: `.output_port()`) 사용되지 않는 입력은 명시적으로 접지에 연결되어야 합니다(예: `.unused_input_port(8'd0)`) .

`.*`허용되지 않습니다.

신호를 포트에 연결하기 위해 위치 인수를 사용하지 마십시오.

모듈에 정의된 것과 동일한 순서로 포트를 인스턴스화합니다.

[테이블 형식](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#tabular-alignment) 으로 포트 표현식을 정렬 합니다. 가장 긴 포트 이름의 여는 괄호 앞에 공백을 포함하지 마십시오. 여는 괄호 뒤 또는 포트 표현식을 묶는 닫는 괄호 앞에 공백을 포함하지 마십시오.

👎

```verilog
mod u_mod(
  .clk_i,
  .rst_ni,

  // Not allowed: avoid leading/trailing whitespace in expressions.
  .sig_1_i( sig_1 ),
  .sig_2_i( sig_2 )
);

mod u_mod(
  .clk_i,
  .rst_ni,

  .short_sig_i                       (sig_1),
  // Not allowed: avoid whitespace between the longest signal name and the opening parenthesis.
  .a_very_long_signal_name_indeed_i  (sig_2)
);
```

***모든 인스턴스화에 대해 명명된 매개변수를 사용하십시오.***

인스턴스를 매개변수화할 때 명명된 매개변수 스타일을 사용하여 매개변수를 지정하십시오. 예외는 레지스터 너비와 같이 명백한 매개변수가 하나만 있는 경우 인스턴스화가 암시적일 수 있다는 것입니다.

모듈 인스턴스화를 위한 들여쓰기는 두 개의 공백 들여쓰기의 표준 들여쓰기 규칙을 따릅니다.

```verilog
my_module #(
  .Height(5),
  .Width(10)
) my_module (
  // ...
);

my_reg #(16) my_reg0 (
  .clk_i,
  .rst_ni,
  .d_i   (data_in),
  .q_o   (data_out)
);
```

매개변수가 하나만 있고 레지스터 인스턴스의 너비와 같이 해당 매개변수의 의도가 분명한 경우가 아니면 매개변수를 위치적으로 지정하지 마십시오.

사용하지 마십시오 `defparam`.

***재귀적으로 인스턴스화하지 마십시오.***

모듈은 재귀적으로 자신을 인스턴스화할 수 없습니다.

### 상수

***원시 숫자 대신 기호로 명명된 상수를 사용하는 것이 좋습니다.***

반복적으로 원시 숫자를 입력하는 대신 일반적으로 사용되는 상수에 기호 이름을 지정하십시오.

지역 상수는 항상 를 사용하여 선언해야 합니다 `localparam`.

전역 상수는 항상 별도의 `.vh`또는`.svh` include file.

SystemVerilog 코드의 경우 전역 상수는 항상 패키지 매개변수로 선언되어야 합니다. Verilog-2001 호환 코드의 경우 최상위 매개변수가 지원되지 않으며 ``define`대신 매크로를 사용해야 합니다.

상수의 기호 이름에 접미사로 상수의 단위를 포함합니다. 이 규칙의 예외는 본질적으로 단위가 없는 상수이거나 상수가 기본 단위 유형인 "비트"를 설명하는 경우입니다.

예시:

```verilog
localparam int unsigned INTERFACE_WIDTH = 64;  // Bits
localparam int unsigned INTERFACE_WIDTH_BYTES = (INTERFACE_WIDTH + 7) / 8;
localparam int unsigned INTERFACE_WIDTH_64B_WORDS = (INTERFACE_WIDTH + 63) / 64;
localparam int unsigned IMAGE_WIDTH_PIXELS = 640;
localparam int unsigned MEGA = 1000 * 1000;  // Unitless
localparam int unsigned MEBI = 1024 * 1024;  // Unitless
localparam int unsigned SYSTEM_CLOCK_HZ = 200 * MEGA;
```

### 신호 폭

***신호 폭에 주의하십시오.***

#### 항상 숫자 리터럴의 너비를 명시해야 합니다.

예:

👍

```verilog
localparam logic [3:0] bar = 4'd4;

assign foo = 8'd2;
```

👎

```verilog
localparam logic [3:0] bar = 4;

assign foo = 2;
```

예외:

- 매개변수화된 너비를 사용할 `1'b1`때 와 같은 방법보다는 단순히 사용하는 것이 허용됩니다(예: 증가할 때) `{{(Bus_width-1){1'b0}}, 1'b1}`. 또는 다음과 같이 쓸 수 있습니다 `Bus_width'(1)`.
- 자동으로 올바른 크기의 0을 생성하기 위해 '0 구조를 사용하는 것은 허용됩니다.
- 정수 변형(예: byte, shortint, int, integer 및 longint)에 할당된 리터럴에는 명시적 너비가 필요하지 않습니다.

#### 모듈 인스턴스의 포트 연결은 항상 너비와 정확하게 일치해야 합니다.

가능하면 Verilog의 암시적 0 확장 및 자르기 작업에 의존하기보다 명시적 너비를 사용하는 것이 좋습니다.

예:

👍

```verilog
my_module i_module (
  .thirty_two_bit_input({16'd0, sixteen_bit_word})
);
```

👎

```verilog
my_module i_module (
  // Incorrectly implicitly extends from 16 bit to 32 bit
  .thirty_two_bit_input(sixteen_bit_word)
);
```

#### 부울 컨텍스트에서 다중 비트 신호를 사용하지 마십시오.

부울 연산과 if 식이 다중 비트 신호를 단일 비트로 줄이는 대신 다중 비트 신호를 0과 명시적으로 비교합니다. 암시적 변환은 미묘한 논리 버그를 숨길 수 있습니다.

예;

👍

```verilog
logic [3:0] a, b;
logic out;

assign out = (a != '0) && (b == '0);

always_comb begin
  if (a != '0)
    ...
  else
    ...
end
```

👎

```verilog
logic [3:0] a, b;
logic out;

// Incorrect because it implicitly converts 4-bit signals to 1-bit before AND.
// Also, !b is different from ~b and can be hard to catch.
assign out = a && !b;

// Incorrect use of a multi-bit signal in an if expression
always_comb begin
  if (a)
    ...
  else
    ...
end
```

#### 비트 슬라이싱

비트 벡터의 일부를 참조하려는 경우에만 비트 슬라이싱 연산자를 사용하십시오.

예:

👍

```verilog
logic [7:0] a, b;
logic [6:0] c;

assign a = 8'd7;       // good

assign a[7:1] = 7'd5;  // good - it's partial assignment.
assign a = b;          // good - the parser would warn on width mismatch.
```

👎

```verilog
logic [7:0] a, b;

assign a[7:0] = 8'd7;  // BAD - redundant and can mask linter warnings.
assign a = b[7:0];     // BAD - redundant and masks linter warnings.
```

#### 너비 오버플로 처리

피연산자보다 넓은 결과를 생성할 수 있는 시프트 연산에 주의하십시오. 비트 선택 및 연결은 일정한 양만큼 이동하는 것보다 명확할 수 있습니다.

더하기 및 부정 연산은 캐리로 인해 피연산자보다 1비트 더 넓은 결과를 생성합니다. 너비 일치에 대한 규칙에 허용되는 예외는 자동으로 수행 할당을 삭제하는 것입니다.

예시:

```verilog
logic [3:0] cnt_d, cnt_q;
assign cnt_d = cnt_q + 4'h1;
```

또는 사이즈 캐스팅을 사용하여 캐리를 떨어뜨리는 것을 명시적으로 표현할 수 있습니다.

```verilog
assign cnt_d = 4'(cnt_q + 4'h1);
```

### 차단 및 비차단 할당

***순차 논리는 비차단 할당을 사용해야 합니다. 조합 블록은 차단 할당을 사용해야 합니다.***

블록 선언 내에서 할당 유형을 혼합하지 마십시오.

순차 블록(클록 에지에서 상태를 래치하는 블록)은 아래 순차 논리 섹션에 정의된 대로 비블록 할당을 독점적으로 사용해야 합니다.

순수 조합 블록은 차단 할당을 독점적으로 사용해야 합니다.

이것은 Cliff Cumming의 [Verilog의 황금률](http://www.ece.cmu.edu/~ece447/s13/lib/exe/fetch.php?media=synth-verilog-cummins.pdf) 중 하나입니다 .

### 지연 모델링

***`#delay`합성 가능한 디자인 모듈 에는 사용하지 마십시오 .***

합성 가능한 설계 모듈은 지연 없는 시뮬레이션 방법론을 중심으로 설계되어야 합니다. `#delay`를 포함한 모든 형식은 `#0`허용되지 않습니다.

자세한 내용은 Cliff Cumming의 [Verilog Nonblocking Assignments with Delay, Myths & Mysteries](http://www.sunburst-design.com/papers/CummingsSNUG2002Boston_NBAwithDelays.pdf) 를 참조하십시오.

### 순차 논리(래치)

***걸쇠의 사용은 권장되지 않습니다. 가능하면 플립플롭을 사용하십시오.***

절대적으로 필요한 경우가 아니면 래치 대신 플롭/레지스터를 사용하십시오.

래치를 사용해야 하는 경우 `always_latch`over `always`를 사용하고 비차단 할당( `<=`)을 사용합니다. 차단 할당( `=`)을 사용하지 마십시오.

### 순차 논리(레지스터)

***순차 블록을 선언할 때 표준 형식을 사용하십시오.***

순차 Always 블록에서는 비차단 할당( `<=`)만 사용합니다. 차단 할당( `=`)을 사용하지 마십시오.

레지스터에 대한 차단 및 비차단 할당을 혼합하는 설계는 일부 시뮬레이터가 별도의 시뮬레이션 이벤트에서 비차단 할당으로 발생하는 것으로 항상 차단의 일부 차단 할당을 처리하기 때문에 잘못 시뮬레이션합니다. 이 프로세스는 일부 신호가 레지스터를 점프하게 하여 잠재적으로 전체 양성자 반전으로 이어질 수 있습니다. 그 나쁜.

상태 할당을 위한 순차 명령문은 재설정 값과 상태에 대한 다음 상태 할당만 포함해야 하며, 다음 상태 값을 생성하기 위해 별도의 조합 전용 블록을 사용합니다.

초기 값이 "0xAB"인 올바르게 구현된 8비트 레지스터가 구현됩니다.

👍

```verilog
logic foo_en;
logic [7:0] foo_q, foo_d;

always_ff @(posedge clk or negedge rst_ni) begin
  if (!rst_ni) begin
    foo_q <= 8'hab;
  end else if (foo_en) begin
    foo_q <= foo_d;
  end
end
```

동일한 비트에 여러 개의 비차단 할당을 허용하지 마십시오.

예시:

👎

```verilog
if (cond1) begin
  abc <= 4'h1;
end

if (cond2) begin
  abc <= 4'h2;
end
```

cond1과 cond2가 모두 참이면 Verilog 표준에 따르면 두 번째 할당이 적용되지만 이는 스타일 위반입니다.

`cond1`와 `cond2`가 상호 배타적 일지라도 두 번째 `if`를 로 만듭니다 `else if`.

예외: 먼저 기본값을 설정한 다음 특정 값을 설정하는 것이 좋습니다. 그러나 명시적 차단 할당이 있는 별도의 조합 블록에서 이 작업을 수행하는 것이 좋습니다.

예시:

```verilog
always_ff @(posedge clk or negedge rst_ni) begin
  if (!rst_ni) begin
    state_q <= StIdle;
  end else begin
    state_q <= state_d;
  end
end

always_comb begin
  state_d = state_q;    // default assignment next state is present state
  unique case (state_q)
    StIdle: state_d = StInit;       // Idle State move to Init
    StInit: begin                   // Initialize calculation
      if (conditional) begin
        state_d = StIdle;
      end else begin
        state_d = StCalc;
      end
    end
    StCalc: begin                   // Perform calculation
      if (conditional) begin
        state_d = StResult;
      end
    end
    StResult: state_d = Idle;
    default: ;
  endcase
end
```

순차 블록의 작업을 단순하게 유지하십시오. 순차 블록이 충분히 복잡해지면 조합 논리를 별도의 조합( `always_comb`) 블록으로 분할하는 것을 고려하십시오. 이상적으로 순차 블록은 로드 활성화 또는 증분과 함께 레지스터 인스턴스화만 포함해야 합니다.

### 상관하지마( `X`'s)

***RTL 코드에서 리터럴을 사용 `X`하지 않는 것이 좋습니다. RTL은 `X`어떤 경우에도 합성에 "신경 쓰지 않음"을 나타내도록 주장해서는 안 됩니다. 값을 할당하고 전파하는 대신 잘못된 조건에 플래그를 지정하고 감지하려면 `X`설계에서 모든 신호 값을 완전히 정의하고 SVA를 광범위하게 사용하여 잘못된 조건을 표시해야 합니다.***

엄격하게 제어되지 않는 경우 `X`RTL에서 할당을 사용하여 유효하지 않거나 무관한 조건에 플래그를 지정하면 시뮬레이션/합성 불일치가 발생할 수 있습니다.

`X`잘못된 조건에 플래그를 지정하고 감지하기 위해 할당 및 전파하는 대신 **SVA를 광범위하게 사용하는** 것이 좋습니다 . 이 설계 방식의 추가 이점은 다음과 같습니다.

- `X`조건 을 적절하게 전파하기 위해 특별한 코드 스타일이 필요하지 않습니다 .
- 실수로 시뮬레이션/합성 불일치를 도입할 가능성이 체계적으로 감소하고,
- 시뮬레이션이 빠르게 실패하고 버그의 근본 원인에 필요한 신호 역추적이 더 적습니다.
- 여러 경우에 공식 자산 검증(FPV)을 사용하여 이러한 SVA가 항상 충족될 수 있는지 여부를 증명할 수 있습니다.
- 보안 컨텍스트에서는 불법/무효/접근할 수 없는 입력 조합에 대해서도 결정론적/정의된 동작이 필요합니다(때로는 "보안에 중요한 디자인에는 신경쓰지 않아도 됨"으로 더 간략하게 설명됨).

여기에 제시된 솔루션은 Don Mills [의 "Being With Your X" 에 제시된 접근 방식과 유사합니다.](http://www.lcdm-eng.com/papers/snug04_assertiveX.pdf)

합성 도구에 가능한 최적화 기회를 나타내기 위해 don't care를 사용할 수 있지만, 논리 감소의 이득이 `X`리터럴의 사용이 수반할 수 있는 합성 불일치 문제(특히 오늘날의 기술에서 사용할 수 있는 게이트 수).

#### 유효하지 않은 값이 사용되는 오류 포착

유효하지 않을 수 있지만(로 구동되지는 않음) 내부적으로 생성된 신호의 경우 `X`일부 작업(예: 레지스터 쓰기 가능)을 트리거하는 데 사용되는 경우 활성화가 true일 때 확인하기 위해 어설션을 추가하는 것이 좋습니다. 신호가 유효합니다. 이것은 잘못된 값이 실수로 사용되었을 때 진단하기 쉬운 실패를 트리거합니다.

```verilog
logic reg_addr;
logic reg_wr_en;

// internal logic which generates reg_addr/reg_wr_en reg_en_addr will never
// be X but must be ignored if reg_wr_en == 0
assign reg_addr = ...
assign reg_wr_en = ...

...

// trigger some specific action when a certain register is written
logic special_reg_en;

assign special_reg_en = (reg_addr == SPECIAL_REG_ADDR) & reg_wr_en;

// Aim to keep RHS of implication as broad as possible
`ASSERT(NoSpecialRegEnWithoutRegEn, special_reg_en |-> reg_wr_en);
```

값과 유효성 신호가 `X`유효하지 않은 신호 를 구동하는 DV 환경에 의해 생성되는 경우 ``ASSERT_KNOWN`충분합니다.

```verilog
module mymod (
  input [7:0] external_addr_i,
  input       external_wr_en_i
);

  logic special_action_en;

  assign special_action_en =
      (external_addr_i == SPECIAL_ADDR) & external_wr_en_i;

  `ASSERT_KNOWN(special_action_en)

endmodule
```

#### 사례 진술 및 삼항에 대한 특정 지침

이 스타일을 준수하기 위해 RTL은 FIFO, SRAM 또는 레지스터 파일 출력과 같이 ``ASSERT_KNOWN`암시적으로 시뮬레이션 시작 부분에 있을 수 있는 신호를 제외하고 모든 모듈 출력에 어설션을 배치해야 합니다.`X`

```verilog
module mymod (
  input        ina_i,
  input        inb_i,
  output logic out_o
);
  assign out_o = ina_i ^ inb_i;
  `ASSERT_KNOWN(OutKnown_A, out_o, clk_i, !rst_ni)
endmodule : mymod
```

또한 case 문, 삼항 또는 if/else 문의 조건을 형성하는 신호에 주장을 추가하는 것이 좋습니다. ``ASSERT_KNOWN` 어설션 스타일은 디자이너의 재량에 따르며 다음 예와 같이 단순한 것부터 완전한 기능을 갖춘 어설션까지 다양합니다.

```verilog
typedef enum logic [1:0] {mode0, mode1, mode2} state_e;
state_e sel;

// encouraged
`ASSERT_KNOWN(SelKnown_A, sel)
always_comb begin
  out0 = '0;
  out1 = '0;
  unique case (sel)
    mode1: out0 = foo;
    mode2: out1 = bar;
    default: ;
  endcase
end

// optional, but more explicit
// not always applicable
`ASSERT(MainFsmCase_A, sel inside {mode0, mode1, mode2}, clk_i, !rst_ni)
always_comb begin
  out0 = '0;
  out1 = '0;
  unique case (sel)
    mode1: out0 = foo;
    mode2: out1 = bar;
    default: ;
  endcase
end
```

삼항 문장의 맥락에서 다음은 권장되는 예입니다.

```verilog
// encouraged
`ASSERT_KNOWN(ModeKnown_A, mode_i, clk_i, !rst_ni)
`ASSERT_KNOWN(LenKnown_A, len_i, clk_i, !rst_ni)
// assign '0 for all other combinations
assign val = (mode_i == ENC)                    ? 8'h01 :
             (mode_i == DEC && len_i == LEN128) ? 8'h36 :
             (mode_i == DEC && len_i == LEN192) ? 8'h80 :
             (mode_i == DEC && len_i == LEN256) ? 8'h40 : 8'h00;

// optional, but more explicit
`ASSERT(ValSelValid_A, mode_i == ENC || mode_i == DEC &&
    len_i inside {LEN128, LEN192, LEN256}, clk_i, !rst_ni)
// using one of the valid outputs for other combinations (saves logic)
assign val = (mode_i == ENC)                    ? 8'h01 :
             (mode_i == DEC && len_i == LEN128) ? 8'h36 :
             (mode_i == DEC && len_i == LEN192) ? 8'h80 :
             (mode_i == DEC && len_i == LEN256) ? 8'h40 : 8'h01;
```

케이스 또는 삼항에 대한 입력이 있을 수 `X` 있지만 입력을 한정하는 일부 유효한 신호가 설정되지 않아 출력이 무시되므로 중요하지 않은 상황에서만 발생하는 경우가 있습니다. 예를 들어 입력은 메모리 또는 DV 환경이 구동하는 최상위 입력에서 직접 공급될 수 있습니다 `X`. 플레인 ``ASSERT_KNOWN`은 이러한 상황에서 작동하지 않으며 대신 일부 자격이 있는 유효한 어설션을 사용하는 것이 적절합니다.

```verilog
`ASSERT(AddrKnownIfValid, addr_valid |-> !$isunknown(addr))
always_comb begin
  out = '0
  unique case (addr[1:0])
    ConstAddr1: out = foo;
    ConstAddr2: out = bar;
    default:    out = baz;
  endcase
end
```

목적은 요구되는 것보다 더 범위를 좁히기보다는 자격을 갖춘 유효한 신호를 가능한 한 넓게 만드는 것이어야 `X`합니다.

👎

```verilog
`ASSERT(AddrKnownIfValid,
  addr_valid & internal_condition_1 & internal_condition_2 |->
  !$isunknown(addr))
```

#### 동적 배열 인덱싱

동적 배열 인덱싱 작업은 암시적으로 `X`. 인덱싱된 배열을 2의 거듭제곱으로 정렬하거나 인덱싱 작업 주위에 보호 if 문을 추가하여 가능하면 이를 피해야 합니다. 이러한 솔루션은 다음 예에 나와 있습니다.

👎

```verilog
logic selected;
logic [3:0] idx;
logic [11:0] foo; // problematic

assign foo = {12'b1010_1111_0000};
assign selected = foo[idx];
```

👍

```verilog
logic selected;
logic [3:0] idx;
logic [15:0] foo; // aligned to powers of two

assign foo = {4'b0000, 12'b1010_1111_0000};
assign selected = foo[idx];
```

👍

```verilog
logic selected;
logic [3:0] idx;
logic [11:0] foo;

assign foo = {12'b1010_1111_0000};

// guarding if statement
assign selected = (idx < $bits(foo)) ? foo[idx] : 1'b0;
```

### 조합 논리

***민감도 목록을 피하고 일관된 할당 유형을 사용합니다.***

`always_comb`SystemVerilog 조합 블록에 사용 합니다. `always @*`Verilog-2001만 지원하는 경우에 사용 합니다. 조합 논리에 대한 민감도 목록을 명시적으로 선언하지 마십시오.

가능한 한 assign 문을 선호합니다.

예시:

```verilog
assign final_value = xyz ? value_a : value_b;
```

case 문이 필요한 경우 자체 `always_comb`블록으로 묶습니다.

합성 가능한 조합 논리 블록은 차단 할당만 사용해야 합니다.

`Z`muxing과 같은 온칩 로직을 수행하기 위해 3상태 로직(상태)을 사용하지 마십시오 .

시뮬레이션/합성 불일치가 발생할 수 있으므로 함수 내부의 래치를 유추하지 마십시오.

### 사례 진술

***대소문자를 수정하는 프라그마를 피하세요. `unique case`가장 좋은 방법입니다. 항상 기본 케이스를 정의하십시오.***

`full_case`또는 `parallel_case`pragma 를 사용하지 마십시오 . 이러한 pragma는 합성-시뮬레이션 불일치를 쉽게 일으킬 수 있습니다.

다음은 스타일 호환 전체 케이스 문의 예입니다.

```verilog
always_comb begin
  unique casez (select)
    3'b000: operand = accum0 >> 0;
    3'b001: operand = accum0 >> 1;
    3'b010: operand = accum1 >> 0;
    3'b011: operand = accum1 >> 1;
    3'b1??: operand = regfile[select[1:0]];
    default: operand = '0; // assign a default
  endcase
end
```

접두사 는 `unique`특정 실수를 포착할 수 있는 시뮬레이션 어설션을 생성하므로 모든 case 문 앞에 권장됩니다. 어떤 경우에는 `priority` 가 대신 사용될 수 `unique`있지만 이러한 경우에는 계단식 삼항 구조가 우선순위 인코더에 대해 더 읽기 쉬운 표현이므로 우선순위 인코더를 나타내는 데 선호되는 방법이어야 합니다.

반드시 `unique case`올바르게 사용하십시오. 특히 다음을 확인하십시오.

- 모든 경우가 포함되더라도 실수로 래치를 추론하는 것을 방지하기 위해 명령문 `default:`이 **항상 포함됩니다.** 시뮬레이션에서 로 평가되는 케이스 표현식은 `X`어떤 케이스와도 일치하지 않고 래치처럼 작동하여 기본값이 지정되지 않은 경우 합성과 다른 동작을 유발합니다.
- 위의 예와 같이 case 문 앞에 기본 할당이 지정되지 않은 경우 하나의 case 항목에 할당된 모든 변수는 를 포함한 모든 case 항목에 할당되어야 합니다 `default:`. 이렇게 하지 않으면 [Don Mills의 논문](http://www.lcdm-eng.com/papers/snug12_Paper_final.pdf) 에 설명된 대로 시뮬레이션 합성 불일치가 발생할 수 있습니다 .

다음은 유한 상태 머신의 다음 상태 논리를 설명하는 데 자주 사용되는 스타일 호환 case 문 변형을 보여주는 다른 예입니다. 이전 예제와 다른 점은 기본 할당이 `unique case`블록 앞에 놓이기 때문에 더 아래의 개별 사례에서 공통 할당을 생략할 수 있다는 것입니다. case 문 이전에 공통 기본 할당이 아니었다면 모든 변수는 `default:`시뮬레이션 합성 불일치를 방지하기 위해 모든 경우에 값을 할당해야 합니다.

```verilog
always_comb begin
  // common default assignments
  state_d = state_q;
  outa = 1'b0;
  outb = 1'b0;
  outc = 1'b0;

  unique case (state_q)
    Idle: begin
      state_d = Work;
      outa = in0;
    end
    Work: begin
      state_d = Wait;
      outb = in1;
    end
    Wait: begin
      state_d = Idle;
      outc = in2;
    end
    // always include a default case
    // empty default permissible due to defaults before case block
    default: ;
  endcase
end
```

#### 케이스 항목의 와일드카드

`case`와일드카드 연산자 동작이 필요하지 않은 경우 사용 합니다. `case inside`와일드카드 연산자 동작이 필요한 경우 사용 합니다. `casez`와일드카드 연산자 동작이 필요하고 Verilog-2001 호환성이 필요한 경우 사용 합니다.

케이스 항목에 와일드카드를 표현할 때 '?' 의도를 더 명확하게 표현하기 때문입니다.

```
casex`사용해서는 안됩니다. 케이스 표현식이 하나 이상의 케이스 항목과 일치할 수 `casex`있도록 대칭 와일드카드 연산자를 구현 합니다. 고임피던스 상태( 또는 )만 와일드카드로 취급하고 구동되지 않은 입력 에 대해 정확한 일치를 수행합니다 . 이것이 대칭 와일드카드 일치의 문제를 완전히 해결하지는 못하지만 실수로 입력을 생성하는 것이 입력보다 더 어렵 기 때문에 이 형식이 선호됩니다. 은(는) 또는 case 표현식을 와일드카드로 취급하지 않으므로 이 형식이 .`X``casez``Z``?``X``Z``X``case inside``X``Z``casez
```

참조:

- Don Mills, [또 다른 래치 및 Gotchas 종이](http://www.lcdm-eng.com/papers/snug12_Paper_final.pdf)
- Clifford Cummings, [full_case parallel_case, Verilog Synthesis의 사악한 쌍둥이](http://www.sunburst-design.com/papers/CummingsSNUG1999Boston_FullParallelCase_rev1_1.pdf)
- Clifford Cummings, [SystemVerilog의 우선 순위 및 고유](http://www.sunburst-design.com/papers/CummingsSNUG2005Israel_SystemVerilog_UniquePriority.pdf)
- Sutherland, Mills 및 Spear, [Gotcha Again: 모든 엔지니어가 알아야 하는 Verilog 및 SystemVerilog 표준의 더 많은 미묘함](http://www.lcdm-eng.com/papers/snug07_Verilog Gotchas Part2.pdf)

### 구성 생성

***항상 생성된 블록의 이름을 지정하십시오.***

생성 구문을 사용할 때 항상 생성된 코드의 각 블록에 명시적으로 이름을 지정하십시오. 생성하는 if 문의 가능한 각 결과의 이름을 지정하고 생성 for 문의 반복 블록의 이름을 지정하십시오.

이렇게 하면 생성된 계층적 신호 이름이 여러 도구에서 일관성을 유지합니다.

생성하고 모든 명명된 코드 블록은 를 사용해야 합니다 `lower_snake_case`. `begin`와 코드 블록 이름 사이에는 공백이 있어야 합니다 .

조건부 생성 구문의 예:

👍

```verilog
if (TypeIsPosedge) begin : posedge_type
  always_ff @(posedge clk) foo <= bar;
end else begin : negedge_type
  always_ff @(negedge clk) foo <= bar;
end
```

루프 생성 구문의 예:

👍

```verilog
for (genvar ii = 0; ii < NumberOfBuses; ii++) begin : my_buses
  my_bus #(.index(ii)) i_my_bus (.foo(foo), .bar(bar[ii]));
end
```

`begin`추가 블록 으로 생성 구문을 래핑하지 마십시오 .

`generate`영역 생성 { , `endgenerate`} 을 사용하지 마십시오 .

### 부호 있는 산술

***부호 있는 산술이 사용되는 곳마다 사용 가능한 부호 있는 산술 구조를 사용하십시오.***

unsigned에서 signed로 변환해야 하는 경우 `signed'`캐스트 연산자( `$signed`Verilog-2001에서)를 사용합니다.

계산의 피연산자가 부호 없는 경우 Verilog는 암시적으로 모든 피연산자를 unsigned로 변환하고 경고를 생성합니다. 모든 서명되지 않은 변수가 적절하게 캐스트된 경우 시뮬레이션 또는 합성 도구에서 서명된 대 서명되지 않은 경고가 없어야 합니다.

암시적 서명에서 서명되지 않은 캐스팅의 예:

```verilog
logic signed [7:0]  a;
logic               incr;
logic signed [15:0] sum1, sum2, sum3;
initial begin
  a = 8'sh80;                        // a = -128
  incr = 1'b1;
  sum1 = a + incr;                   // bad:  sum1 = 16'h0081 ( 129)
  sum2 = a + signed'({1'b0, incr});  // good: sum2 = 16'hFF81 (-127)
  sum3 = a + 8'sh01;                 // good: sum3 = sum2 (more straightforward)
end
```

위의 예에서 unsigned라는 사실 은 unsigned 로 평가되는 `incr`원인이 됩니다. 평가는 놀랍고 무시해서는 안 되는 경고로 표시됩니다 `a`.`sum1`

### 숫자 서식

***인쇄된 이진수 앞에 `0b`. 인쇄된 16진수 숫자 앞에 `0x`. 십진수에 접두사를 사용하지 마십시오.***

로그 파일에 대한 숫자의 텍스트 표현 형식을 지정할 때 포함하는 데이터를 명확히 하십시오.

인쇄된 숫자의 밑부분을 명확하게 만드십시오. 수정자 없이 십진수만 인쇄합니다. 16진수에는 접두사를 사용하고 2 `0x`진수 에는 접두사를 사용합니다 `0b`.

사용자가 원시 값을 수동으로 디코딩할 것으로 기대하는 대신 대규모 구조의 개별 필드를 개별적으로 디코딩합니다.

👍

```verilog
$display("0x%0x", some_hex_value);
$display("0b%0b", some_binary_value);
$display("%0d",   some_decimal_value);
```

👎

```verilog
$display("%0x",   some_hex_value);
$display("%0b",   some_binary_value);
$display("0d%0d", some_decimal_value);
```

상수 값을 할당할 때 더 나은 가독성을 위해 길이가 8을 초과하는 16진수 또는 2진수 비트 강도에 대해 밑줄 표기법을 사용하는 것이 좋습니다. 가독성이 향상되지 않는 한 0 앞에 추가할 필요가 없습니다. 일반적으로 표시되는 형식(2진수, 16진수, 10진수)으로 상수를 선언합니다.

👍

```verilog
logic [15:0] val0, val1, val2;
logic [39:0] addr0, addr1;

always_comb begin
  val0 = 16'h0;
  if (condition1) begin
    val1  = 16'b0010_0011_0000_1101;
    val2  = 16'b0010_1100_0000_0000;
    addr1 = 40'h00_1fc0_0000;
    addr2 = 40'h00_efc0_0000;
  end else begin
    val0  = 16'hffff;
    val1  = 16'b1010_0011_0110_1001;
    val2  = 16'b1110_1100_1111_0110;
    addr1 = 40'h40_8000_0000;
    addr2 = 40'h41_c000_0000;
  end
end
```

### 기능 및 작업

다음 섹션은 합성 가능한 RTL에만 적용됩니다. DV 사용을 [위한 설계 검증을 위한 코딩 스타일 가이드를](https://github.com/ParkDongho/style-guides/blob/master/DVCodingStyle.md) 참조하십시오 .

***합성 가능한 RTL에서는 선언된 함수의 사용이 허용됩니다 `automatic`. 작업을 사용해서는 안됩니다.***

함수는 패키지 또는 모듈 내부에서 선언해야 합니다. 패키지는 함수가 패키지의 다른 정의와 관련된 경우에 적합하고 여러 모듈에 유용할 수 있습니다(현재 하나에서만 사용되는 경우에도). 기능이 해당 모듈의 내부와 특별히 관련된 경우 모듈이 적합합니다.

함수는 조합 논리의 재사용 가능한 블록을 개념적으로 표현하는 것을 목표로 해야 합니다.

모든 인수와 함수 반환 값에 대해 저장소 유형을 명시적으로 선언해야 합니다. 모든 유형은 4-상태 데이터 유형이거나 `logic`또는 에서 파생된 유형 `logic`(예: 적절한 또는 유형 `struct`) 이어야 합니다 .`enum``typedef`

`output`, `inout`또는 `ref`함수 인수에 사용하지 마십시오 . 모든 함수는 입력을 소비하고 하나의 출력을 생성해야 합니다. `input`기본값이며 함수 인수에는 필요하지 않습니다.

👎

```verilog
// - Doesn't have explicit storage type on `a` or `b` or return type
// - `b` being used as `output` argument
// - `input` not required on `a`
function automatic [2:0] foo(input [2:0] a, [2:0] b);
  b = b + 1;
  return a + b;
endfunction
```

👎

```verilog
// - Doesn't have explicit storage type on `a`, `b` or `c`
// - Uses `output` on `c`
// - `input` not required on `a` and `b`
function automatic logic [2:0] foo(input [2:0] a, input [2:0] b, output [2:0] c);
  c = a - b;
  return a + b;
endfunction
```

👎

```verilog
// - Uses 2-state data type `int` for `a`
function automatic logic [2:0] foo(int a, logic [2:0] b);
  return a + b;
endfunction
```

👍

```verilog
function automatic logic [2:0] foo(logic [2:0] a, logic [2:0] b);
 return a ^ b;
endfunction
```

👍

```verilog
typedef logic [2:0] bar_t;

typedef struct packed {
  logic [2:0] field;
} baz_t;

function automatic logic [2:0] foo(bar_t a, baz_t b);
  return a + b.field;
endfunction
```

`return result`데이터는 명시적 스타일 을 사용하여 함수에서 반환되어야 합니다 . `function_name = result`스타일 을 사용하지 마십시오 .

👎

```verilog
function automatic logic [2:0] foo(logic [2:0] a, logic [2:0] b);
  if (a == 3'd2) begin
    foo = b;
  end else begin
    foo = a ^ b;
  end
endfunction
```

👍

```verilog
function automatic logic [2:0] foo(logic [2:0] a, logic [2:0] b);
  logic [2:0] result;

  if (a == 3'd2) begin
    result = b;
  end else begin
    result = a ^ b;
  end

  return result;
endfunction
```

모든 지역 변수는 초기 할당을 통해 또는 for `else`및 문 을 사용하여 모든 코드 경로에 할당되어야 합니다. `default:``if``case`

👍

```verilog
function automatic logic [2:0] foo(logic [2:0] a, logic [2:0] b);
  logic [2:0] local_var_1;
  logic [2:0] local_var_2;

  local_var_1 = 3'd0;

  if (a == 0) begin
    local_var_1 = 3'd2;
  end

  unique case(b)
    3'd0:    local_var_2 = 3'd1;
    3'd1:    local_var_2 = 3'd3;
    default: local_var_2 = 3'd0;
  endcase

  return local_var_1 + local_var_2;
endfunction
```

👎

```verilog
function automatic logic [2:0] foo(logic [2:0] a, logic [2:0] b);
  logic [2:0] local_var_1;
  logic [2:0] local_var_2;

  if (a == 0) begin
    local_var_1 = 3'd2;
  end

  unique case(b)
    3'd0:    local_var_2 = 3'd1;
    3'd1:    local_var_2 = 3'd3;
  endcase

  return local_var_1 + local_var_2;
endfunction
```

### 문제가 있는 언어 기능 및 구성

이러한 언어 기능은 문제가 있는 것으로 간주되며 달리 명시되지 않는 한 사용을 권장하지 않습니다.

- 인터페이스.
- `alias`성명 .

#### 부동 시작-종료 블록

`for`루프 이외의 생성 블록 `if`또는 `case`생성 구성을 사용하는 것은 LRM을 준수하지 않습니다. 일부 도구에서는 이러한 사용이 허용될 수 있지만 이 가이드에서는 이러한 "베어" 생성 블록을 금지합니다. 유사한 "순차 블록" 구성이 LRM을 준수하고 허용된다는 점에 유의하십시오.

👎

```verilog
module foo (
  input bar,
  output foo
);
  begin // illegal generate block
    assign foo = bar;
  end
endmodule
```

#### 계층적 참조

합성 가능한 RTL 코드에서 계층적 참조를 사용하는 것은 금지됩니다. 특정 합성 도구는 실제로 계층적 참조를 지원하지만 일부 도구는 오류가 발생하고 다른 도구는 자동으로 무시하여 잠재적으로 시뮬레이션/합성 불일치로 이어질 수 있습니다.

이에 대한 면제는 예를 들어 SystemVerilog 주장(SVA)의 일부로 합성을 위해 계층 참조를 제거하기 위해 매크로에 의해 보호되는 경우입니다.

👎

```verilog
module mymod_int (
  input        in0_i,
  input        in1_i,
  input        in2_i,
  output logic out_o
);

  logic int;
  assign int   = in0_i & in1_i;
  assign out_o = in2_i | int;

endmodule

module mymod (
  ...
);

  mymod_int u_mymod_int (
    .in0_i,
    .in1_i,
    .in2_i,
    .out_o
  );

  // Hierarchical references are prohibited in synthesizable RTL code.
  assign int_o = u_mymod_int.int;

endmodule
```

## 디자인 컨벤션

### 요약

이 섹션의 주요 아이디어는 다음과 같습니다.

- 모든 신호를 선언하고 다음을 사용 `logic`하십시오.`logic foo;`
- 패킹된 배열은 리틀 엔디안입니다.`logic [7:0] byte;`
- 압축을 푼 배열은 빅엔디안입니다.`byte_t arr[0:N-1];`
- 모듈 출력을 등록하는 것을 선호합니다.
- FSM을 일관되게 선언합니다.

### 모든 신호 선언

***추론된 그물에 의존하지 마십시오.***

모든 신호 는 사용 전에 명시적으로 선언되어야 합니다 **.** 선언된 모든 신호는 데이터 유형을 지정해야 합니다. 올바른 설계에는 추론된 네트가 포함되어 있지 않습니다.

### `logic`합성에 사용

***`logic`합성에 사용 합니다. `wire`필요한 경우 허용됩니다.***

합성 가능한 RTL의 모든 신호는 4-상태 데이터 유형의 관점에서 구현되어야 합니다. 이는 모든 신호가 궁극적으로 스토리지 유형이 인 네트로 구성되어야 함을 의미합니다 `logic`. SystemVerilog는 4-상태 저장(즉 `integer`, )을 가진 다른 데이터 기본 요소를 제공하지만 이러한 기본 요소는 오해와 오용이 발생하기 쉽습니다.

예를 들어:

👍

```verilog
logic signed [31:0] x_velocity;  // say what you mean: a signed 32-bit integer.
typedef logic [7:0] byte_t;
```

👎

```verilog
bit signed [63:0] stars_in_the_sky;  // 2-state logic doesn't belong in RTL
int grains_of_sand;  // Or wait, did I mean integer?  Easy to confuse!
```

네트를 선언하고 연속 할당을 수행하기 위해 와이어를 약어로 사용할 수 있습니다. 연속 할당과 초기화를 혼동하지 않도록 주의하십시오. 예를 들어:

👍

```verilog
wire [7:0] sum = a + b;  // Continuous assignment
```

👎

```verilog
logic [7:0] sum = a + b; // Initialization (not synthesizable)
```

`sum`와 b의 초기값의 합으로 초기화된다.

👍

```verilog
logic [7:0] acc = '0;    // Initialization (synthesizable on some FPGA tools)
```

`logic`부적절한 장소에 대한 예외가 있습니다 . 예를 들어 양방향( `inout`) 포트에 연결하는 네트는 로 선언해야 합니다 `wire`. 이러한 예외는 짧은 설명으로 정당화되어야 합니다.

DV(Design Verification)가 2-상태 로직을 사용하는 것은 허용되지만 4-상태와 2-상태 신호 사이의 모든 인터페이스는 `X`2-상태 변수로 해석되기 전에 4-상태 네트에 대한 검사를 주장해야 합니다.

### 논리 대 비트 단위

***논리적 비교에는 논리적 구성을 선호하고 데이터에는 비트 단위를 선호합니다.***

논리 연산자( `!`, `||`, `&&`, `==`, `!=`)는 if 절 및 삼항 할당과 같이 논리(true 또는 false) 값을 평가하는 모든 구문에 사용해야 합니다. 스칼라일지라도 모든 데이터 구성에 대해 비트 연산자( `~`, `|`, `&`, )를 선호합니다. `^`평가된 표현식이 논리적 컨텍스트에서 사용되어야 하는 것이 분명한 경우 예외가 만들어질 수 있습니다.

👍

```verilog
always_ff @(posedge clk_i or negedge rst_ni) begin
  if (!rst_ni) begin
    reg_q <= '0;
  end else begin
    reg_q <= reg_d;
  end
end

always_comb begin
  if (bool_a || (bool_b && !bool_c) begin
    x = 1'b1;
  end else begin
    x = 1'b0;
end

assign z = ((bool_a != bool_b) || bool_c) ? a : b;
assign y = (a & ~b) | c;
```

👎

```verilog
always_ff @(posedge clk_i or negedge rst_ni) begin
  if (~rst_ni) begin
    reg_q <= '0;
  end else begin
    reg_q <= reg_d;
  end
end

always_comb begin
  if (bool_a | (bool_b & ~bool_c) begin
    x = 1'b1;
  end else begin
    x = 1'b0;
end

assign z = ((bool_a ^ bool_b) | bool_c) ? a : b;
assign y = (a && !b) || c;
```

👍

```verilog
// allowed logical assignment for boolean test
assign request_valid = !fifo_empty && data_available;

always_comb begin
  if (request_valid) begin
    output_valid = 1'b1;
  end else begin
    output_valid = 1'b0;
  end
end
```

### 포장 주문

***비트 벡터와 묶음 배열은 리틀 엔디안이어야 합니다.***

비트 벡터와 묶음 배열을 선언할 때 최상위 경계(콜론의 왼쪽)의 인덱스는 최하위 경계(콜론의 오른쪽)보다 크거나 같아야 합니다.

이 스타일의 비트 벡터 선언은 패킹된 변수를 리틀 엔디안으로 유지합니다.

예를 들어:

```verilog
typedef logic [7:0] u8_t;
logic [31:0] u32_word;
u8_t [1:0] u16_word;
u8_t byte3, byte2, byte1, byte0;
assign u16_word = {byte1, byte0};
assign u32_word = {byte3, byte2, u16_word};
```

### 포장을 푼 주문

***압축을 푼 배열은 빅엔디안이어야 합니다.***

압축을 푼 배열을 빅엔디안 방식으로 선언합니다(예: `[n:m]`where `n <= m`). 압축을 푼 배열을 리틀 엔디안 순서로 선언하지 마십시오(예: `[size-1:0]`.

더 짧은 표기법을 사용하여 0부터 시작하는 압축되지 않은 배열을 선언합니다 `[size]`. `[size]`빅 엔디안 선언과 동일한 것으로 이해 `[0:size-1]`됩니다.

```verilog
logic [15:0] word_array[3] = '{word0, word1, word2};
```

### 유한 상태 기계

***상태 머신은 열거형을 사용하여 상태를 정의하고 두 가지 프로세스 블록인 조합 블록과 클록 블록으로 구현됩니다.***

모든 상태 머신 설명에는 세 부분이 있습니다.

1. 상태를 선언하고 설명하는 열거형입니다.
2. 상태를 디코딩하여 다음 상태 및 기타 조합 출력을 생성하는 조합 프로세스 블록.
3. 다음 상태에서 상태를 업데이트하는 클럭 프로세스 블록.

*상태 열거*

상태 머신의 enum 문은 상태 머신의 각 상태를 나열해야 합니다. 상태를 설명하는 주석은 아래의 조합 프로세스 블록에서 case 문으로 연기되어야 합니다.

[상태는 다른 열거 상수](https://github.com/ParkDongho/style-guides/blob/master/VerilogCodingStyle.md#enumerations)`UpperCamelCase` 와 마찬가지로 에 이름을 지정해야 합니다 .

특별한 상황을 제외하고 상태 머신의 초기 유휴 상태는 `Idle`또는 로 지정 `StIdle`됩니다. (명확성을 향상시키는 경우 대체 이름을 사용할 수 있습니다.)

이상적으로 각 모듈에는 하나의 상태 머신만 포함되어야 합니다. 모듈에 둘 이상의 상태 머신이 필요한 경우 각 상태 머신의 상태에 고유한 접두사(또는 접미사)를 추가하여 어떤 상태가 어떤 상태 머신과 연결되어 있는지 구별해야 합니다. 예를 들어, "판독기" 기계와 "작성기" 기계가 있는 모듈은 `StRdIdle`상태와 상태를 가질 수 있습니다 `StWrIdle`.

*국가의 조합 해독*

조합 프로세스 블록에는 다음이 포함되어야 합니다.

- 상태를 디코딩하여 다음 상태 및 조합 출력을 생성하는 case 문. 명확성을 위해 출력 값이 기본값에서 벗어나는 경우에만 코딩해야 합니다.
- case 문 앞에 "다음 상태"를 포함하여 모든 조합 출력에 대한 기본값을 정의하는 코드 블록이 있어야 합니다.
- "다음 상태" 변수의 기본값은 현재 상태여야 합니다. 상태를 디코딩하는 case 문은 상태 간 전환 시 "다음 상태"에만 할당합니다.
- case 문 내에서 각 상태 대안 앞에는 상태 시스템 내에서 해당 상태의 기능을 설명하는 주석이 있어야 합니다.

*주정부 등록부*

이 과정에서 리셋을 제외한 어떠한 로직도 수행되어서는 안 된다. 상태 변수는 "다음 상태" 변수의 값을 래치해야 합니다.

*기타 지침*

가능하면 이름 시작 부분에서 다른 상태 이름을 선택하여 파형 추적을 볼 때 읽기 쉽게 만드십시오.

*예시*

👍

```verilog
// Define the states
typedef enum {
  StIdle, StFrameStart, StDynInstrRead, StBandCorr, StAccStoreWrite, StBandEnd
} alcor_state_e;

alcor_state_e alcor_state_d, alcor_state_q;

// Combinational decode of the state
always_comb begin
  alcor_state_d = alcor_state_q;
  foo = 1'b0;
  bar = 1'b0;
  bum = 1'b0;
  unique case (alcor_state_q)
    // StIdle: waiting for frame_start
    StIdle:
      if (frame_start) begin
        foo = 1'b1;
        alcor_state_d = StFrameStart;
      end
    // StFrameStart: Reset accumulators
    StFrameStart: begin
      // ... etc ...
    end
    // may be empty or used to catch parasitic states
    default: alcor_state_d = StIdle;
  endcase
end

// Register the state
always_ff @(posedge clk or negedge rst_n) begin
  if (!rst_n) begin
    alcor_state_q <= StIdle;
  end else begin
    alcor_state_q <= alcor_state_d;
  end
end
```

### 액티브-로우 신호

***접미사 는 `_n`액티브 로우 신호를 나타냅니다.***

`_n`액티브 로우 신호를 사용하는 경우 이름에 접미사가 있어야 합니다 . 그렇지 않으면 모든 신호는 활성-하이로 간주됩니다.

### 차동 쌍

***차동 쌍을 나타내 려면 `_p`및 접미사를 사용합니다.`_n`***

예를 들어, 차동 쌍 세트 `in_p`를 구성합니다.`in_n`

### 지연

***`_q`단일 클록 주기만큼 지연된 신호는 접미사 로 끝나야 합니다 .***

한 신호가 다른 신호의 지연된 버전일 경우 `_q`이 관계를 나타내기 위해 접미사를 사용해야 합니다.

다른 신호가 다른 클록 주기에 의해 지연되면 다음 신호는 `_q2`접미사 로 식별되어야 하는 식으로 `_q3`계속됩니다.

예시:

```verilog
always_ff @(posedge clk) begin
  data_valid_q <= data_valid_d;
  data_valid_q2 <= data_valid_q;
  data_valid_q3 <= data_valid_q2;
end
```

### 패키지의 와일드카드 가져오기

와일드카드 가져오기 구문, 예 `import ip_pkg::*;`를 들어 패키지가 해당 패키지를 사용하는 모듈과 동일한 IP의 일부인 경우에만 허용됩니다. 와일드카드 import 문은 모듈 헤더 또는 모듈 본문에 배치해야 합니다.

👍

```verilog
// mod_a_pkg.sv and mod_a.sv are in the same IP.
// Packages can be imported in the module declaration if access to
// unqualified types is needed in the port list.

// mod_a_pkg.sv
package mod_a_pkg;

  typedef struct packed {
    ...
  } a_req_t;
endpackage

// mod_a.sv
module mod_a
  import mod_a_pkg::*;
(
  ...
  a_req_t a_req,
  ...
);

endmodule
```

👍

```verilog
// mod_a
module mod_a ();

  // mod_a_pkg.sv and mod_a.sv are in the same IP.
  import mod_a_pkg::*;

  ...

  a_req_t a_req;

endmodule
```

위의 경우 외에는 와일드카드 가져오기가 허용되지 않습니다. `mod_a` 예를 들어, 아래 예제 는 소스 목록에 이어지는 모듈에서 이름 충돌을 생성할 수 있습니다 .

👎

```verilog
// mod_a.sv
import mod_a_pkg::*; // not allowed: imported to $root scope.

module mod_a ();

endmodule
```

다른 나쁜 예:

👎

```verilog
// wildcard import for other packages outside of the IP
module mod_a import mod_b_pkg::*; ();
```

👎

```verilog
module mod_a ();

  // not allowed: wildcard import of a package from a different IP
  import mod_b_pkg::*;

endmodule
```

### 어설션 매크로

기능적 정확성을 확인하고 유효하지 않은 조건에 플래그를 지정하기 위해 설계 전반에 걸쳐 SystemVerilog 주장(SVA)을 사용하는 것이 좋습니다. 생산성을 높이고 어설션을 짧고 간결하게 유지하기 위해 다음 어설션 매크로를 사용할 수 있습니다.

```verilog
// immediate assertion, to be placed within a process.
`ASSERT_I(<name>, <property>)
// immediate assertion wrapped within an initial block. can be used for things
// like parameter checking.
`ASSERT_INIT(<name>, <property>)
// concurrent assertion to be used for functional assertions.
`ASSERT(<name>, <property>, <clk>, <reset condition>)
// concurrent assertion that checks that a signal has a known value after reset
// (i.e. that the signal is not `X`).
`ASSERT_KNOWN(<name>, <signal>, <clk>, <reset condition>)
```

이러한 매크로의 구현(다른 유용한 변형 포함)은 [https://github.com/ParkDongho/opentitan/blob/master/hw/ip/prim/rtl/prim_assert.sv 에서 찾을 수 있습니다.](https://github.com/ParkDongho/opentitan/blob/master/hw/ip/prim/rtl/prim_assert.sv)

#### 보안 크리티컬 애플리케이션에 대한 참고 사항

보안에 중요한 응용 프로그램의 경우 케이스 문 및 삼항을 보호하는 것과 관련된 어설션 매크로의 이름은 접미사로 `_SEC`. 이를 통해 설계 프로세스의 나중 단계에서 이러한 명령문의 보안 관련 사후 처리가 가능합니다. 기능 면에서 이러한 매크로는 원래 주장과 동일해야 합니다. 즉,

```verilog
`define ASSERT_SEC `ASSERT
`define ASSERT_I_SEC `ASSERT_I
`define ASSERT_KNOWN_SEC `ASSERT_KNOWN
```

더 많은 보안 주장 및 코딩 스타일 지침은 곧 별도의 문서에서 제공될 예정입니다.

## 부록 - 압축 스타일 가이드

이것은 Comportable 스타일 가이드에 대한 간략한 요약입니다. 설명 예 및 예외는 본문을 참조하십시오.

### 기본 스타일 요소

- SystemVerilog-2012 규칙, module.sv로 명명된 파일, 모듈당 하나의 파일 사용
- ASCII만 가능, 한 줄 에 **100** 자, 탭 **없음 , 모든 쌍을 이루는 키워드에 대해 들여쓰기당** **2개의** 공백.
- C++ 스타일 주석`//`
- 한 줄에 여러 항목이 있는 경우 **한** 공백은 쉼표와 다음 문자를 구분해야 합니다.
- 키워드 및 이항 연산자 주위에 **공백** 포함
- 케이스 항목과 콜론, 함수/태스크/매크로 호출 및 여는 괄호 사이에 공백 **없음**
- **줄 바꿈은 4** 칸 들여쓰기를 해야 합니다.
- `begin`앞의 키워드와 같은 줄에 있어야 하고 줄을 끝내야 합니다.
- `end`새 줄을 시작해야 합니다

### 구성 이름 지정

- 인스턴스 이름, 신호, 선언, 변수, 유형에 **lower_snake_case** 사용
- 조정 가능한 매개변수, 열거된 값 이름에 **UpperCamelCase** 사용
- **상수에 ALL_CAPS** 를 사용 하고 매크로를 정의합니다.
- 메인 클럭 신호의 이름은 `clk`. 모든 클럭 신호는 다음으로 시작해야 합니다.`clk_`
- 재설정 신호는 **활성-낮음** 및 **비동기식** 이며 기본 이름은 다음과 같습니다.`rst_n`
- 신호 이름은 설명적이어야 하며 계층 전체에서 일관되어야 합니다.

### 신호 및 유형에 대한 접미사

- `_i`모듈 입력, `_o`모듈 출력 또는 `_io`양방향 모듈 신호에 추가
- 등록된 신호의 입력(다음 상태)에는 접미사 가 있어야 `_d`하고 출력 은 다음과 같아야 합니다.`_q`
- 신호의 파이프라인 버전은 지연 시간을 반영하도록 , 등 으로 이름 `_q2`을 지정해야 합니다.`_q3`
- 활성 로우 신호는 를 사용해야 합니다 `_n`. 차동 신호를 사용할 때 `_p`활성 하이에 사용
- 열거형은 접미사로 붙여야 합니다.`_e`
- 다중 접미사는 로 구분되지 않습니다 `_`. 먼저 , , 또는 마지막 에 `n`와야 합니다. `i``o``io`

### 언어 기능

- **모듈에 전체 포트 선언 스타일** 을 사용 하고 모든 클럭 및 재설정이 먼저 선언됨
- **인스턴스화를 위해 명명된 매개변수** 를 사용하십시오 . 선언된 모든 포트가 있어야 합니다.`.*`
- 최상위 매개변수가 ``define`전역 매개변수보다 선호됩니다.
- 원시 숫자 대신 기호 **로 명명된 상수 사용**
- `localparam`지역 상수는 별도의 **.svh** 파일 에 전역 으로 선언해야 합니다.
- `logic``reg`및 보다 선호되며 `wire`모든 신호를 명시적으로 선언합니다.
- `always_comb`, `always_ff`및 `always_latch`_`always`
- 인터페이스는 권장되지 않습니다.
- **순차 논리는 비차단** 할당 을 사용해야 합니다.
- **조합 블록은 차단** 할당 을 사용해야 합니다.
- 걸쇠의 사용은 권장되지 않으며 가능하면 플립플롭을 사용하십시오.
- RTL에서 할당을 사용 `X`하지 않는 것이 좋습니다. 대신 SVA를 사용하여 잘못된 동작을 확인하십시오.
- `assign`가능한 한 진술을 선호 합니다.
- 케이스 를 사용 `unique case`하고 항상 정의`default`
- 부호 있는 산술이 사용되는 곳마다 사용 가능한 부호 있는 산술 구조를 사용하십시오.
- 인쇄할 때 이진수와 16진수의 접두사로 `0b`and 를 사용합니다. 명확성을 위해 `0x`사용 `_`
- 논리적 비교에는 논리적 구조(ie `||`)를 사용하고 데이터 비교에는 비트 단위(ie `|`)를 사용합니다.
- 비트 벡터와 패킹된 배열은 리틀 엔디안이어야 하고 압축되지 않은 배열은 빅 엔디안이어야 합니다.
- FSM: 상태 레지스터에 대한 프로세스에서 리셋을 제외한 **어떤 로직 도 수행되어서는 안 됨**
- 조합 프로세스는 먼저 프로세스 의 모든 출력에 대한 **기본값 을 정의해야 합니다.**
- 다음 상태 변수의 기본값은 현재 상태여야 합니다.
