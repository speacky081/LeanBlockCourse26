# Unicode Input

In Lean files, type `\` followed by an abbreviation and press Space or Tab to insert a Unicode symbol. In VS Code, you can also hover over any symbol to see its abbreviation, or use `Ctrl+Shift+P` → "Lean 4: Show All Abbreviations" to browse the full list.

The tables below list every symbol used in this course. The canonical source for all Lean 4 abbreviations is [`abbreviations.json`](https://github.com/leanprover/vscode-lean4/blob/master/lean4-unicode-input/src/abbreviations.json) in the vscode-lean4 repository.

## Logic (P02)

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

## Sets (P03)

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

## Types (P04)

| Symbol | Input | Alternatives | Name |
|:------:|-------|--------------|------|
| `λ` | `\lam` | `\la`, `\lambda`, `\fun` | lambda |
| `×` | `\x` | `\times` | product type |
| `↦` | `\mapsto` | `\ma` | mapsto |
| `∘` | `\circ` | `\o`, `\comp` | function composition |

## Numbers and Arithmetic (P05+)

| Symbol | Input | Alternatives | Name |
|:------:|-------|--------------|------|
| `ℕ` | `\N` | `\nat` | natural numbers |
| `ℤ` | `\Z` | `\int` | integers |
| `≠` | `\ne` | `\neq` | not equal |
| `≤` | `\le` | `\leq`, `\<=` | less or equal |
| `≥` | `\ge` | `\geq`, `\>=` | greater or equal |
| `∣` | `\mid` | `\|`, `\dvd` | divides |
| `⁻¹` | `\inv` | `\-1`, `\-` | inverse |

## Greek Letters and General

| Symbol | Input | Alternatives | Name |
|:------:|-------|--------------|------|
| `α` | `\a` | `\alpha` | alpha |
| `β` | `\b` | `\beta` | beta |
| `γ` | `\g` | `\gamma` | gamma |
| `·` | `\.` | `\cdot` | middle dot |
| `₁` | `\_1` | `\1` | subscript 1 |
| `₂` | `\_2` | `\2` | subscript 2 |
| `₃` | `\_3` | `\3` | subscript 3 |
