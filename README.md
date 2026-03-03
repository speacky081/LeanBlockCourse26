# Formalized Math in LEAN – FUB Block Course 2026

## Announcements

- Uploaded slides for `P01_Introduction` *2025-03-02*

## General notes

This is the second time this course is being held. The structure will largely follow last year’s with some additions and modifications, but is nevertheless subject to (spontaneous) change. Constructive feedback is welcomed throughout the course and afterwards.

### Teaching team

[Christoph Spiegel](https://christophspiegel.berlin) will teach this course. He is a researcher at ZIB in Prof. Pokutta’s IOL group, working on combinatorics, optimization, machine learning, and proof formalization. [Silas Rathke](https://www.mi.fu-berlin.de/en/math/groups/geokomb/People/PhD-Students/Silas_Rathke.html) will serve as the teaching assistant. He is a Ph.D. student at FUB in Prof. Szabo’s group, focusing on extremal combinatorics and related formalization projects.

### Time and venue

The course takes place from **Monday the 2nd of March** to **Friday the 13th of March 2026**, split into two daily sessions (9:30–12:30 and 14:00–17:00). It will be held in **Seminarraum 119 (A3/SR 119) at Arnimallee 3** on the FUB Dahlem Campus.

### Registration and credit

The course is open to everyone, including guest auditors (Gasthörer), not just those who need it for their degree. Priority will be given to FU students who need the course as part of their ABV degree program. The course will also be offered for **Master students at the FUB** as well as as a **BMS Advanced Course** for the first time this year!

For the `aktive Teilnahme`, Master-level participants will be required to solve additional and more advanced problems in the exercise sessions compared to Bachelor-level students. Both Bachelor and Master-level students will sit the same **final exam on the second Friday**. Master-level students will additionally receive a **small formalization project** to complete in the one or two weeks following the course. The exact scope and evaluation format has not yet been determined but may include an in-person presentation.

### Prerequisites

Completion of Analysis I and Linear Algebra I should provide a sufficient mathematical background, though participants should have a strong command of these subjects, as formal proof verification is very "unforgiving". No prior programming experience is required, but a certain technical affinity and interest is needed. Besides formal proof verification, you will be in contact with many other tools such as `git` and `github`, [Patrick Massot’s](https://www.imo.universite-paris-saclay.fr/~patrick.massot/en/) `leanblueprint`, CI/CD in the form of `github Actions`, as well as various ML tools.

Participants need to **bring a laptop** to follow along and work on exercises. The course will be **conducted in English**, but Bachelor students taking the course as part of their ABV requirements may express themselves in German if they prefer.

### Setup

We will walk through the full setup together on the first day, covering [Visual Studio Code](https://code.visualstudio.com), a **[GitHub account](https://github.com/signup)**, and **git**. The process for setting up git varies by platform:

* **macOS** — `xcode-select --install` installs Apple’s developer tools, which include git. [Homebrew](https://brew.sh) is not required but recommended as a general package manager.
* **Linux** — Install git via your package manager, e.g. `sudo apt install git` on Debian/Ubuntu or `sudo pacman -S git` on Arch.
* **Windows** — We recommend installing [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) (Windows Subsystem for Linux) with Ubuntu, which is the officially recommended environment for Lean on Windows. Git is then installed within WSL (`sudo apt install git`). Keep your course files inside the WSL filesystem (e.g. `~/projects/`) rather than your Windows Documents folder, and open VS Code from within WSL using `code .`.

## Course Outline

The course outline is still subject to change, but will roughly be as follows:

1) General introduction, or: why formalize maths?
1) The tech stack, or: how to properly organize a formalization project?
1) Foundations of Logic in LEAN, or: what is a type and what does being classical vs. intuitionistic mean?
1) Set theory in LEAN, or: why you should rarely do set theory in LEAN
1) Natural numbers in LEAN, or: why inductive types are so powerful.
1) **Formalization Example** The infinitude of primes, or: your first real proof in LEAN.
1) **Formalization Example** The handshaking lemma, or: graph theory and combinatorics in LEAN.
1) **Examination** Final exam and distribution of small formalization projects for Master-level students.
1) **Optional** An example on how to contribute to mathlib.

## Unicode Input

In Lean files, type `\` followed by an abbreviation and press Space or Tab to insert a Unicode symbol. In VS Code, you can also hover over any symbol to see its abbreviation, or use `Ctrl+Shift+P` → "Lean 4: Show All Abbreviations" to browse the full list.

The table below lists every symbol used in this course. The canonical source for all Lean 4 abbreviations is [`abbreviations.json`](https://github.com/leanprover/vscode-lean4/blob/master/lean4-unicode-input/src/abbreviations.json) in the vscode-lean4 repository.

### Logic (P02)

| Symbol | Input | Alternatives | Name |
|:------:|-------|--------------|------|
| `→` | `\to` | `\r`, `\->` | implication / function type |
| `←` | `\l` | `\<-`, `\gets` | reverse arrow |
| `↔` | `\iff` | `\lr`, `\<->` | biconditional |
| `∧` | `\and` | `\an` | conjunction |
| `∨` | `\or` | `\v` | disjunction |
| `¬` | `\not` | `\neg`, `\!` | negation |
| `∀` | `\all` | `\forall` | universal quantifier |
| `∃` | `\ex` | `\exists` | existential quantifier |
| `⟨` | `\<` | `\langle` | anonymous constructor (open) |
| `⟩` | `\>` | `\rangle` | anonymous constructor (close) |
| `▸` | `\t` | `\rw` | substitution / rewrite |

### Sets (P03)

| Symbol | Input | Alternatives | Name |
|:------:|-------|--------------|------|
| `∈` | `\in` | `\mem` | membership |
| `∉` | `\notin` | `\nin` | non-membership |
| `⊆` | `\sub` | `\ss`, `\subseteq` | subset |
| `⊂` | `\ssub` | `\ssubset` | strict subset |
| `∩` | `\cap` | `\i`, `\inter` | intersection |
| `∪` | `\cup` | `\un`, `\union` | union |
| `⋂₀` | `\I0` | `\sInter` | family intersection |
| `⋃₀` | `\U0` | `\sUnion` | family union |
| `∅` | `\empty` | `\emptyset` | empty set |
| `ᶜ` | `\^c` | `\compl` | complement |

### Types (P04)

| Symbol | Input | Alternatives | Name |
|:------:|-------|--------------|------|
| `λ` | `\lam` | `\la`, `\lambda`, `\fun` | lambda |
| `×` | `\x` | `\times` | product type |
| `↦` | `\mapsto` | `\ma` | mapsto |
| `∘` | `\circ` | `\o`, `\comp` | function composition |

### Numbers and Arithmetic (P05+)

| Symbol | Input | Alternatives | Name |
|:------:|-------|--------------|------|
| `ℕ` | `\N` | `\nat` | natural numbers |
| `ℤ` | `\Z` | `\int` | integers |
| `≠` | `\ne` | `\neq` | not equal |
| `≤` | `\le` | `\leq`, `\<=` | less or equal |
| `≥` | `\ge` | `\geq`, `\>=` | greater or equal |
| `∣` | `\mid` | `\|`, `\dvd` | divides |
| `⁻¹` | `\inv` | `\-1`, `\-` | inverse |

### Greek Letters and General

| Symbol | Input | Alternatives | Name |
|:------:|-------|--------------|------|
| `α` | `\a` | `\alpha` | alpha |
| `β` | `\b` | `\beta` | beta |
| `γ` | `\g` | `\gamma` | gamma |
| `·` | `\.` | `\cdot` | middle dot |
| `₁` | `\_1` | `\1` | subscript 1 |
| `₂` | `\_2` | `\2` | subscript 2 |
| `₃` | `\_3` | `\3` | subscript 3 |


## Technical difficulties

### `git` and `github`

*No information yet.*

### Wrangling `lean` and `lake`

* `lake init ProjectName math` sets up a project with mathlib as a dependency in the current folder.
* `lake build` builds the project.
* If your info view shows that it is compiling a lot of files from mathlib, then (1) run `pkill -f lean` (MacOS / Linux) or `Stop-Process -Name *lean* -Force` (Windows) to kill the running Lean processes, (2) remove the `.lake` folder, e.g., by running `rm -rf .lake` in a POSIX compliant OS, and run `lake clean`, (3) run `lake exe cache get` to download the mathlib binaries again, and finally (4) restart the Lean server by clicking on the `∀` button in VS Code and choosing `Server: Restart Server`.

### `leanblueprint`

*No information yet.*

### Containerization with `docker` and CI/CD through `git Actions`

*No information yet.*

### `claude`, `codex`, and other LLM tools

*No information yet.*

## Resources

### Documentation and search
* The [mathlib documentation](https://leanprover-community.github.io/mathlib4_docs/index.html) is the official documentation of the [mathlib library](https://github.com/leanprover-community/mathlib4)
* [LeanSearch](https://leansearch.net) is a helpful resource for finding results in mathlib

### Text books
* [Theorem Proving in Lean 4](https://leanprover.github.io/theorem_proving_in_lean4/) by Jeremy Avigad, Leonardo de Moura, Soonho Kong, Sebastian Ullrich
* [Mathematics in Lean](https://leanprover-community.github.io/mathematics_in_lean/) by Jeremy Avigad and Patrick Massot
* [The Hitchhiker’s Guide to Logical Verification](https://cs.brown.edu/courses/cs1951x/static_files/main.pdf) by Anne Baanen, Alexander Bentkamp, Jasmin Blanchette, Johannes Hölzl, Jannis Limperg
* [The Mechanics of Proof](https://hrmacbeth.github.io/math2001/) by Heather Macbeth
* [Functional Programming in Lean](https://lean-lang.org/functional_programming_in_lean/) by David Thrane Christiansen

### Talks

* Kevin Buzzard's talk on [The rise of formalism in mathematics](https://www.youtube.com/watch?v=SEID4XYFN7o) at ICM22

### A more playful approach
* The [Lean Game Server](https://adam.math.hhu.de) inspired many of the smaller exercises
