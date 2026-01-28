General requirements

* The code shall be MISRA C:2012 compliant. Compliance with Advisory rules is not mandatory, but recommended.
* The code shall respect the HIS metrics defined in Annex 1.
* The code shall be documented so it can be parsed by Doxygen (used by VHIT/EAD).

SDCM_0002 — Comments in C source code

* Allowed comment styles are: /* ... */ and //.
* Code sections that are not self-explanatory shall be extended with meaningful comments.
* Source code comments shall be written in English.
* Comments shall be aligned with the code they refer to.
* Nesting of comments is not allowed (tools may interpret nested comments differently).
* Meaningful comments shall follow Doxygen style.

Programming guide

Preprocessor directives
SDCM_0003 — Numeric constants

* Use macros for symbolic numeric constants.

SDCM_0004 — Function-like macros

* Avoid function-like macros unless they provide a significant performance improvement.
* If possible, use inline functions instead of function-like macros.
* Note: function remapping is not affected (it may improve reusability and configurability).

SDCM_0005 — Macros usage

* Macros may be used to: access structures, generate bit masks, or perform small and easy logical or mathematical operations.
* Macros shall not replace C language keywords or constructs (readability and maintainability).
* If the macro is not only a symbolic numeric constant, enclose both macro body and macro parameters in parentheses.
* Macro calls shall not end with a semicolon; semicolons must be placed outside the macro.

Function prototypes
SDCM_0006 — Interface visibility

* Separate interfaces into public and private header files and make visibility explicit through file naming.
* Example: define private interfaces in *_priv.h.

Const
SDCM_0009 — Constant variables

* Variables and parameters that will not change shall be declared with the const qualifier.

SDCM_0010 — Function inputs

* Function inputs are constant within the function scope, so they shall be declared with the const qualifier.

Local variables
General rule

* Use different local variables for different use cases within a function; re-use is error-prone and shall be avoided.
* Using multiple locals should not significantly impact resources because compilers can optimize and often place locals in registers.

SDCM_0011 — Local variables name

* Local variable names shall start with the prefix l_ followed by a meaningful name.

SDCM_0012 — Local variables usage

* Do not re-use variables for different purposes.

SDCM_0013 — Local variables type

* Local variables type shall always be 32-bit; avoid smaller types.
* Arm compilers produce more efficient code using 32-bit variables.
* Avoid stack growth by reducing call hierarchy depth and considering that Arm compilers use registers (if available) for locals.

Data types
SDCM_0014 — Data type for persistent variables

* For storage-using variables (global, static, parameters), use the smallest integer type that covers the required value range.

SDCM_0016 — Positive types

* If the variable can only take positive values, choose an unsigned type.

SDCM_0017 — Floating point

* Use floating point types only if strictly necessary.
* This rule does not apply to microcontrollers equipped with an FPU.

SDCM_0018 — Bit masks

* For bit masks or bit strings, use an unsigned type.

SDCM_0019 — Bit fields type

* Bitfields shall be declared as int (or equivalent) type.
* Note from compiler vendors: using int-sized variables can improve runtime and code size (~5% better code density and similar runtime improvement). Consider this primarily for highly efficient code (e.g., centrally called services). For normal application software, follow size/signedness rules to save RAM (often the critical resource).

User-defined data types (typedefs)
SDCM_0020 — Project specific typedefs

* Do not create project-specific typedefs that redefine existing standard types.

SDCM_0021 — Bit fields

* For portability, avoid C bit fields unless strictly necessary.

SDCM_0022 — Unions

* For portability, avoid unions when possible.
* Hint: if unions are needed (e.g., register access), encapsulate them in an abstraction layer.

Compiler independency / Constructs
SDCM_0024 — Constructs

* The code shall be compiler independent for portability across microcontrollers and compilers.

SDCM_0023 — Compiler independency

* Same requirement: for portability reasons, the code shall be compiler independent and reusable on different uCs/compilers.

Statements
SDCM_0025 — Likely-first ordering in selections

* In selection statements (e.g., if-else), place the most likely condition first, then others in decreasing likelihood.

SDCM_0028 — Bounded iterations

* Loops (for/while/do-while) shall have a predetermined maximum number of iterations.
* Exceptions are allowed only with proper justification.

SDCM_0030 — Timeouts in event-waiting loops

* Event-waiting loops shall include a timeout that breaks the loop.
* If the timeout occurs, the resulting behavior shall be handled.

SDCM_0031 — Inequalities for loop termination

* Loop termination conditions shall use inequalities (<, <=, >, >=).
* Include a plausibility check for the range.

Additional commenting requirements
SDCM_0026 — Comment complex computations

* Comment computations that involve at least five variables/parameters, explaining meaning or logic.

SDCM_0027 — Comment each variable definition

* Each variable definition must be commented with its meaning and usage.

SW behavior
SDCM_0029 — Reset vector jumps

* Jumps to the Reset Vector shall not be used.
* Exceptions are allowed only if properly justified.

Global interrupt disable handling
SDCM_ISR_008 — Ensure re-enable

* Ensure no exception, error, or unexpected control flow can prevent re-enabling interrupts after a critical section.

SDCM_ISR_009 — Keep critical sections simple

* When global interrupts are disabled, the protected code block shall not contain conditional branches, loops, or function calls that could delay or prevent timely re-enabling.

SDCM_ISR_010 — Minimize disable duration

* Minimize the interrupt-disable duration and do not exceed the maximum allowed blocking time defined by system timing constraints.

SDCM_ISR_011 — Mark critical sections

* Clearly mark each interrupt-disabled code block with start and end comments.

SDCM_ISR_012 — Review/justify uses

* All uses of global interrupt disable shall be reviewed and explicitly justified.

Annex 1 — HIS source code metrics (C; apply analogously to other languages)
General

* If metric deviations/boundary violations are required for project-specific reasons, evaluate them at unit level and document clear justifications.
* If deviations/violations occur, apply appropriate measures to ensure software quality.

Metrics and limits

* COMF: comment-to-statement ratio (outside and inside functions) must be > 0.2. Applies to manually written code; not applied to automatically generated code.
* PATH: number of non-cyclic execution paths must be <= 80. Tools may overestimate; if violated, demonstrate the real result.
* GOTO: number of unconditional jumps must be 0.
* v(G): cyclomatic complexity must be <= 10.
* PARAM: number of function parameters must be <= 5.
* STMT: number of statements per function must be <= 50 and > 0. Some violations may be justified by design choices; provide justification if needed.
* LEVEL: maximum nesting level inside a function must be <= 4.
* RETURN: number of return statements per function must be 0 or 1.
* Recursions: number of recursions must be 0.
* VOCF: vocabulary frequency must be <= 4. May be violated due to specific design choice; provide proper justification.

Purpose for LLM-based unit generation

