# VHMA 3003 — SW Naming Convention (3rd issue, 08/2023)

## BSW — C language

---

### Files

Full file name:

`<modulename><_optional>`

Applies to both `.h` and `.c` (extension excluded).

#### Description of `<modulename>`

Identifies the module. All files in same module share the same `<modulename>`. It must be composed by keywords in **PascalCasing**. Keywords substitution follows Table 5.

#### Description of `<_optional>`

Optional role descriptor. If used, must be composed by keywords in **PascalCasing**. Keywords substitution follows Table 5.

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

Must use keywords listed in Table 5.

#### Description of `<_datatype>`

Indicates data type + dynamic behavior.

Structure: `_<datatype>`. Exception: void / pointer-to-void → N/A.

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

#### Description of `<scope_>` for functions

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

#### Description of `<scope_>` for constructs

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

#### Description of `<_datatype>` for construct fields

Same structure and rules as variables.

Additionally, in case of bitfields, `<type>` must be `ix`, where `x` is the number of bits in the bitfield.

---

### Defines and enumerative cases

Full name:

`<scope_><macroname>`

Exception: function‑like macros may follow this or function naming rules.

#### Description of `<scope_>` for defines and enumerative cases

Two categories (Table 10):

- Global (hfile‑defined) → `<MODULENAME>_` (capital letters)
- Local (cfile‑defined) → N/A

#### Description of `<macroname>`

SNAKE_CASING, with usual keyword substitution.

---

### Tables (BSW)

#### Table 5 — Keywords for C language

| Keyword | Full word |
| --- | --- |
| Ab | Alpha-Beta |
| Abs | Absolute |
| Acq | Acquire, Acquisition |
| Adc | Analog-to-Digital Converter |
| Algn | Align, Aligned, Alignment |
| Alv | Alive |
| Amb | Ambient |
| Amp | Amplitude |
| Ang | Angle |
| Appl | Application |
| Arbt | Arbiter |
| Buf | Buffer |
| Cfg | Configure, Configuration |
| Cl | Closed-Loop |
| Clbk | Callback |
| Clr | Clear |
| Cmpt | Compute, Computation |
| Cnt | Count, Counter |
| Cs | Chip Select |
| Ctrl | Control, Controller |
| Curr | Current |
| Cycl | Cycle, Cyclic |
| Dc | Direct Current |
| Dert | Derate, Derating |
| Diag | Diagnostic |
| Dis | Disable |
| Dly | Delay, Delayed |
| Dq | Direct-Quadrature |
| Ecu | Electronic Control Unit |
| En | Enable |
| Err | Error |
| Estm | Estimate, Estimator, Estimation |
| Ev | Event |
| Exec | Execute, Execution |
| Fctr | Factor |
| Ffw | Feedforward |
| Flux | Flux |
| Folw | Follow, Following |
| Gen | Generate, Generator, Generation |
| If | Interface |
| Ind | Inductance |
| Init | Initialize, Initialization |
| Invt | Inverter |
| Kd | Derivative Gain |
| Ki | Integral Gain |
| Kp | Proportional Gain |
| Lim | Limit |
| Man | Manager |
| Max | Maximum |
| Mcsm | Motor Control State Machine |
| Mcu | Microcontroller Unit |
| Mdul | Module |
| Meas | Measure, Measurement |
| Mgnt | Magnet |
| Min | Minimum |
| Mod | Module, Modulation |
| Mon | Monitor, Monitoring |
| Mot | Motor |
| Motn | Motion |
| Ntwk | Network |
| Obs | Observe, Observer, Observation |
| Ol | Open-Loop |
| Perm | Permanent |
| Phs | Phase |
| Pos | Position |
| Prcs | Process, Processing |
| Prd | Period |
| Pred | Predict, Predictor, Prediction |
| Pwm | Pulse Width Modulation |
| Queu | Queue |
| Rchd | Reached |
| Ref | Reference |
| Reld | Reload |
| Res | Resistance |
| Rglt | Regulate, Regulator, Regulation |
| Rqst | Request |
| Rst | Reset |
| Rtor | Rotor |
| Rx | Receive, Receiver, Reception |
| Schd | Schedule, Scheduler |
| Sens | Sense, Sensor, Sensing |
| Serv | Service |
| Setl | Settle, Settled, Settling |
| Shnt | Shunt |
| Smpl | Sample, Sampling |
| Spd | Speed |
| Spi | Serial Peripheral Interface |
| Sply | Supply |
| Ssc | Spread Spectrum Clocking |
| Stor | Stator |
| Strt | Start |
| Sts | Status |
| Swtc | Switch, Switching |
| Sync | Synchronize, Synchronizer, Synchronization |
| Sys | System |
| Temp | Temperature |
| Tmp | Temporary |
| Trgt | Target |
| Trq | Torque |
| Tsfm | Transform, Transformation |
| Tx | Transmit, Transmitter, Transmission |
| Undr | Under |
| Upd | Update |
| Volt | Voltage |
| Warn | Warning |
| Wd | Watchdog |
| Writ | Write |
| Xyz | X, Y, Z phases |

Words that are shorter than 5 letters are not abbreviated into a keyword.

#### Table 6 — Variable scope categories

| Variable scope category | `<scope_>` | `<variablename>` casing |
| --- | --- | --- |
| Global (extern) | `g_` | PascalCasing |
| Global static (file‑static) | N/A | PascalCasing |
| Local | `l_` | camelCasing |
| Local static (function‑static) | `l_` | PascalCasing |
| Function argument | N/A | camelCasing |

#### Table 7 — Function scope categories

| Function scope category | `<scope_>` | `<functionname>` casing |
| --- | --- | --- |
| Global (extern or hfile‑static) | `<modulename>_` | PascalCasing |
| Local (cfile‑static) | N/A | PascalCasing |

#### Table 8 — Construct scope categories

| Construct scope category | `<scope_>` | `<constructname>` casing |
| --- | --- | --- |
| Global (hfile‑declared) | `<modulename>_` | PascalCasing |
| Local (cfile‑declared) | N/A | PascalCasing |

#### Table 9 — Construct entities

| Construct entity | `<constructtype>` |
| --- | --- |
| Type definition (typedef) | `t` |
| Struct (struct) | `s` |
| Union (union) | `u` |
| Enumerative (enum) | `e` |

#### Table 10 — Macro scope categories

| Macro scope category | `<scope_>` | `<macroname>` casing |
| --- | --- | --- |
| Global (hfile‑defined) | `<MODULENAME>_` | SNAKE_CASING |
| Local (cfile‑defined) | N/A | SNAKE_CASING |

---
