# VHMA 3003 — SW Naming Convention (3rd issue, 08/2023)

# Content

## BSW — C language

---

### Files

Full file name:

`<modulename><_optional>`

Applies to both `.h` and `.c` (extension excluded).

#### Description of `<modulename>`

Identifies the module. All files in same module share the same `<modulename>`. It is composed by keywords in **PascalCasing**.

#### Description of `<_optional>`

Optional role descriptor. If used, must be composed by keywords listed in Table 5 in **PascalCasing**.

---

### Variables

Full variable name:

`<scope_><variablename><_datatype>`

#### Description of `<scope_>`

Indicates accessibility region, depending on:

- static storage class usage
- declaration region

Five valid categories are listed in Table 6 with corresponding prefixes.

#### Description of `<variablename>`

Meaning‑specific name; duplicates allowed if other parts differ.

Casing depends on storage class (Table 6):

- **PascalCasing** → static variables
- **camelCasing** → non‑static variables

Keywords substitution follows Table 5.

#### Description of `<_datatype>`

Indicates data type + dynamic behavior.

Structure:

`_<datatype>`

Recursive definition:

```text
<datatype> ::= <pointerqualifier><pointer><datatype>
             | <typequalifier><type>
```

Apply the rule starting from the variable's declared type:

- If the current type is a pointer, append `<pointerqualifier>` and `p`, then apply the rule again to the pointed-to type.
- If the current type is an array, append `a`, then apply the rule again to the element type.
- Otherwise, append `<typequalifier><type>` and stop.

Each qualifier applies only to the type at the current recursion level. Append `_` only once, before the complete sequence.

Exception: void / pointer-to-void → N/A.

- `<pointerqualifier>`: `v` volatile pointer, `c` const pointer, `r` restrict pointer, else N/A
- `<pointer>`: `p` if pointer, `a` if array, else N/A
- `<typequalifier>`: `v` volatile, `c` const, else N/A
- `<type>`:
  - `b`, `u8`, `u16`, `u32`, `s8`, `s16`, `s32`, `f`, `d`
  - N/A for user‑defined types

---

### Functions

Full function name:

`<scope_><functionname><_returntype>`

#### Description of `<scope_>`

Indicates scope + defining file.

Two categories (Table 7):

- Global (extern or hfile‑static)
- Local (cfile‑static)

Global prefix is `<modulename>_`.

#### Description of `<functionname>`

Meaning‑specific, PascalCasing.

Keyword substitution as usual.

#### Description of `<_returntype>`

Indicates the data type + dynamic behavior of the returned object.

Structure: same as `_<datatype>`.

---

### Constructs

Full construct name:

`<scope_><constructname>_<constructtype>`

#### Description of `<scope_>`

Two categories (Table 8):

- Global (hfile‑declared) → `<modulename>_`
- Local (cfile‑declared) → N/A

#### Description of `<constructname>`

PascalCasing, with usual keyword substitution.

#### Description of `<constructtype>`

Entity kind (Table 9).

---

### Construct fields

Full field name:

`<fieldname><_datatype>`

#### Description of `<fieldname>`

camelCasing, with usual keyword substitution.

#### Description of `<_datatype>`

Same structure and rules as variables.

---

### Defines and enumerative cases

Full name:

`<scope_><macroname>`

Exception: function‑like macros may follow this or function naming rules.

#### Description of `<scope_>`

Two categories (Table 10):

- Global (hfile‑defined) → `<MODULENAME>_` (capital letters)
- Local (cfile‑defined) → N/A

#### Description of `<macroname>`

SNAKE_CASING, with usual keyword substitution.

---

### Tables (BSW)

#### Table 5 — Keywords for C language

| Keyword | Full word |
|---|---|
| Alv | Alive |
| Appl | Application |
| Buf | Buffer |
| Cfg | Configure, Configuration |
| Clr | Clear |
| Ctrl | Control, Controller |
| Diag | Diagnostic |
| Err | Error |
| If | Interface |
| Man | Manager |
| Mcu | Microcontroller |
| Mdl | Module |
| Meas | Measure, Measurement |
| Mon | Monitor, Monitoring |
| Rqst | Request |
| Rx | Receive, Reception |
| Schd | Schedule, Scheduler |
| Sts | Status |
| Tx | Transmit, Transmission |
| Upd | Update |
| Warn | Warning |
| Writ | Write |

Words that are shorter than 5 letters are not abbreviated.

#### Table 6 — Variable scope categories

| Variable scope category | `<scope_>` | `<variablename>` casing |
|---|---|---|
| Global (extern) | `g_` | PascalCasing |
| Global static (file‑static) | N/A | PascalCasing |
| Local | `l_` | camelCasing |
| Local static (function‑static) | `l_` | PascalCasing |
| Function argument | N/A | camelCasing |

#### Table 7 — Function scope categories

| Function scope category | `<scope_>` | `<functionname>` casing |
|---|---|---|
| Global (extern or hfile‑static) | `<modulename>_` | PascalCasing |
| Local (cfile‑static) | N/A | PascalCasing |

#### Table 8 — Construct scope categories

| Construct scope category | `<scope_>` | `<constructname>` casing |
|---|---|---|
| Global (hfile‑declared) | `<modulename>_` | PascalCasing |
| Local (cfile‑declared) | N/A | PascalCasing |

#### Table 9 — Construct entities

| Construct entity | `<constructtype>` |
|---|---|
| Type definition (typedef) | `t` |
| Struct (struct) | `s` |
| Union (union) | `u` |
| Enumerative (enum) | `e` |

#### Table 10 — Macro scope categories

| Macro scope category | `<scope_>` | `<macroname>` casing |
|---|---|---|
| Global (hfile‑defined) | `<MODULENAME>_` | SNAKE_CASING |
| Local (cfile‑defined) | N/A | SNAKE_CASING |

---
