# 🎓 Scala Programming Assignments Collection

A comprehensive collection of Scala programming assignments covering algorithms, compilers, data structures, and computational problems. This repository showcases functional programming techniques, recursive algorithms, and advanced Scala features.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Project Modules](#project-modules)
- [Installation](#installation)
- [Compilation & Execution](#compilation--execution)
- [Module Documentation](#module-documentation)
- [Technical Highlights](#technical-highlights)
- [Project Structure](#project-structure)

---

## 🎯 Overview

This repository contains **10+ programming assignments** implemented in Scala, covering diverse computer science topics:

- 🧠 **Compiler Design** - Brainf*** interpreter with optimizations
- 🔢 **Mathematical Computing** - Collatz conjecture analysis
- 📄 **Text Processing** - Document similarity algorithms
- 💹 **Financial Computing** - Stock portfolio analysis
- ♟️ **Graph Algorithms** - Knight's tour solver with heuristics
- 📐 **Expression Parsing** - Shunting yard algorithm with operator precedence
- 🔤 **Regular Expressions** - Pattern matching with derivatives
- 🎮 **Game Theory** - Wordle solver with adversarial strategy

---

## 📦 Project Modules

### 1. Brainf*** Interpreter (`bf.scala`, `bfs.scala`)

**Description**: Complete interpreter for the Brainf*** esoteric programming language with multiple optimization levels.

**Features**:
- ✅ Full BF instruction set (8 commands: `><+-.,[]`)
- ✅ Memory management with sparse array (Map-based)
- ✅ Jump table optimization for bracket matching
- ✅ Code simplification (removes comments, optimizes `[-]` loops)
- ✅ Instruction combining for performance
- ✅ Benchmark programs included (Mandelbrot set, Sierpinski triangle)

**Key Functions**:
```scala
def compute(prog: String, pc: Int, mp: Int, mem: Mem): Mem
def run(prog: String, m: Mem = Map()): Mem
def jtable(pg: String): Map[Int, Int]  // Pre-compute jump table
def optimise(s: String): String         // Code optimization
```

**Example Usage**:
```scala
// Hello World
M5a.run("""++++++++[>++++[>++>+++>+++>+<<<<-]>+>+>->>+[<]<-]>>.>---.+++++++..+++.>>.<-.<.+++.------.--------.>>+.>++.""")

// Fibonacci numbers
M5a.run(load_bff("fibonacci.bf"))

// Benchmark performance
time_needed(1, run3(load_bff("benchmark.bf")))
```

---

### 2. Collatz Conjecture (`collatz.scala`)

**Description**: Analysis of the Collatz sequence (3n+1 problem).

**Features**:
- ✅ Generate Collatz sequences
- ✅ Count steps to reach 1
- ✅ Find maximum steps for range of numbers
- ✅ Detect "hard" numbers (where 3n+1 is power of 2)
- ✅ Calculate last odd number in sequence

**Key Functions**:
```scala
def collatz(num: Long): Long                    // Steps to reach 1
def collatz_max(bnd: Int): (Long, Long)         // Max steps in range
def is_pow_of_two(n: Long): Boolean             // Check power of 2
def is_hard(n: Long): Boolean                   // Detect hard numbers
def last_odd(n: Long): Long                     // Last odd in sequence
```

**Example**:
```scala
C1.collatz(27)           // => 111 steps
C1.collatz_max(100000)   // => (350, 77031)
C1.is_hard(5)            // => true (3*5+1 = 16 = 2^4)
```

---

### 3. Document Similarity (`docdiff.scala`)

**Description**: Calculate similarity between text documents using word frequency analysis.

**Features**:
- ✅ Text tokenization with regex
- ✅ Word frequency counting
- ✅ Dot product similarity metric
- ✅ Overlap coefficient calculation

**Key Functions**:
```scala
def clean(s: String): List[String]                      // Extract words
def occurrences(xs: List[String]): Map[String, Int]     // Count frequencies
def prod(lst1: List[String], lst2: List[String]): Int   // Dot product
def overlap(lst1: List[String], lst2: List[String]): Double
def similarity(s1: String, s2: String): Double          // Overall similarity
```

**Example**:
```scala
val doc1 = "The quick brown fox jumps over the lazy dog"
val doc2 = "The lazy dog sleeps under the brown table"
C2.similarity(doc1, doc2)  // => 0.555... (55.5% similarity)
```

---

### 4. Stock Portfolio Analysis (`drumb.scala`)

**Description**: Analyze historical stock data and calculate investment returns.

**Features**:
- ✅ Load CSV stock price data
- ✅ Calculate yearly returns (deltas)
- ✅ Compound interest calculations
- ✅ Portfolio diversification analysis
- ✅ Multi-year investment simulation

**Portfolios**:
- **Blue Chip**: GOOG, AAPL, MSFT, IBM, FB, AMZN, BIDU
- **Real Estate**: PLD, PSA, AMT, AIV, AVB, BXP, CCI, DLR, etc.

**Key Functions**:
```scala
def get_first_price(symbol: String, year: Int): Option[Double]
def get_prices(portfolio: List[String], years: Range): List[List[Option[Double]]]
def get_delta(price_old: Option[Double], price_new: Option[Double]): Option[Double]
def yearly_yield(data: List[List[Option[Double]]], balance: Long, index: Int): Long
def investment(portfolios: List[String], years: Range, start_balance: Long): Long
```

**Example**:
```scala
// $100 invested in 1978, value in 2019:
M1.investment(blchip_portfolio, 1978 to 2019, 100)   // => $8,932
M1.investment(rstate_portfolio, 1978 to 2019, 100)   // => $12,456
```

---

### 5. Knight's Tour Problem (`knight1.scala`, `knight2.scala`)

**Description**: Find Hamilton paths for a knight on a chessboard.

**Features**:
- ✅ Validate legal knight moves (L-shaped)
- ✅ Generate all legal moves from position
- ✅ Count all possible tours
- ✅ Enumerate complete tours
- ✅ Find first tour (backtracking)
- ✅ **Warnsdorff's heuristic** for efficient solving
- ✅ Closed tour detection (returns to start)

**Key Functions**:
```scala
def is_legal(dim: Int, path: Path, x: Pos): Boolean
def legal_moves(dim: Int, path: Path, x: Pos): List[Pos]
def count_tours(dim: Int, path: Path): Int
def enum_tours(dim: Int, path: Path): List[Path]
def first_tour(dim: Int, path: Path): Option[Path]
def ordered_moves(dim: Int, path: Path, x: Pos): List[Pos]  // Warnsdorff
def first_closed_tour_heuristics(dim: Int, path: Path): Option[Path]
```

**Example**:
```scala
// Find a knight's tour on 8x8 board starting at (0,0)
M4a.first_tour(8, List((0,0)))

// Use heuristic for faster solving on larger boards
M4b.first_tour_heuristics(30, List((0,0)))

// Find closed tour (returns to start)
M4b.first_closed_tour_heuristics(6, List((0,0)))
```

**Visualization**:
```
  0  59  38  33  30  17   8  63
 37  34  31  60   9  62  29  16
 58   1  36  39  32  27  18   7
 35  48  41  26  61  10  15  28
 42  57   2  49  40  23   6  19
 47  50  45  54  25  20  11  14
 56  43  52   3  22  13  24   5
 51  46  55  44  53   4  21  12
```

---

### 6. Expression Parser (`postfix.scala`, `postfix2.scala`)

**Description**: Implementation of the Shunting Yard algorithm for converting infix expressions to postfix and evaluating them.

**Features**:
- ✅ Infix to postfix conversion
- ✅ Operator precedence handling
- ✅ Parentheses support
- ✅ Left/right associativity (for exponentiation)
- ✅ Expression evaluation
- ✅ Power operator with fast exponentiation

**Operators**:
- `+`, `-` (precedence 1, left-associative)
- `*`, `/` (precedence 2, left-associative)
- `^` (precedence 4, right-associative)

**Key Functions**:
```scala
def syard(toks: List[String], st: List[String], out: List[String]): List[String]
def compute(toks: List[String], st: List[Int]): Int
def pow(x: Int, n: Int): Int  // Fast exponentiation
```

**Example**:
```scala
// Infix to postfix
C3a.syard(C3a.split("3 + 4 * ( 2 - 1 )"))  
// => List("3", "4", "2", "1", "-", "*", "+")

// Evaluate expression
C3a.compute(C3a.syard(C3a.split("3 + 4 * ( 2 - 1 )")))  // => 7

// Power with associativity
C3b.compute(C3b.syard(C3b.split("4 ^ 3 ^ 2")))          // => 262144 (right-assoc)
C3b.compute(C3b.syard(C3b.split("( 4 ^ 3 ) ^ 2")))      // => 4096
```

---

### 7. Regular Expression Matcher (`re.scala`)

**Description**: Regular expression matching using Brzozowski derivatives (formal language theory approach).

**Regular Expression Syntax**:
- `ZERO` - Empty language (matches nothing)
- `ONE` - Empty string (ε)
- `CHAR(c)` - Single character
- `ALT(r1, r2)` - Alternation (r1 | r2)
- `SEQ(r1, r2)` - Sequence (r1 ~ r2)
- `STAR(r)` - Kleene star (r*)

**Features**:
- ✅ Nullable check (does regex accept empty string?)
- ✅ Derivative computation (partial matching)
- ✅ Simplification to prevent exponential blowup
- ✅ Efficient matching algorithm
- ✅ Handles complex patterns like `(a*)*b`

**Key Functions**:
```scala
def nullable(r: Rexp): Boolean
def der(c: Char, r: Rexp): Rexp         // Derivative w.r.t. character
def simp(r: Rexp): Rexp                 // Simplify regex
def ders(s: List[Char], r: Rexp): Rexp // Derivative w.r.t. string
def matcher(r: Rexp, s: String): Boolean
```

**Example**:
```scala
// Simple matching
M3.matcher(("a" ~ "b") ~ "c", "abc")  // => true
M3.matcher(("a" ~ "b") ~ "c", "ab")   // => false

// The "evil" regex (a*)* b
val EVIL = SEQ(STAR(STAR(CHAR('a'))), CHAR('b'))
M3.matcher(EVIL, "a" * 1000)          // => false (efficient!)
M3.matcher(EVIL, "a" * 1000 ++ "b")   // => true

// Size comparison (with simplification)
M3.size(M3.der('a', M3.der('a', EVIL)))           // => 36 (without simp)
M3.size(M3.simp(M3.der('a', M3.der('a', EVIL))))  // => 7 (with simp)
```

---

### 8. Wordle Solver (`wordle.scala`)

**Description**: Adversarial Wordle solver that finds the hardest-to-guess words using evil strategy.

**Tip Types**:
- `Correct` - Letter in correct position (10 points)
- `Present` - Letter in word but wrong position (1 point)
- `Absent` - Letter not in word (0 points)

**Features**:
- ✅ Load word list from URL
- ✅ Score guesses against secret words
- ✅ Evil strategy (minimize information given)
- ✅ Character frequency analysis
- ✅ Ranked evil words (hardest to guess)

**Key Functions**:
```scala
def get_wordle_list(url: String): List[String]
def score(secret: String, word: String): List[Tip]
def iscore(secret: String, word: String): Int
def evil(secrets: List[String], word: String): List[String]
def frequencies(secrets: List[String]): Map[Char, Double]
def ranked_evil(secrets: List[String], word: String): List[String]
```

**Example**:
```scala
// Load word list
val secrets = M2.get_wordle_list("https://nms.kcl.ac.uk/christian.urban/wordle.txt")
// => 12,972 five-letter words

// Score a guess
M2.score("chess", "caves")  // => [Correct, Absent, Absent, Present, Correct]
M2.iscore("chess", "caves") // => 21

// Find evil words (minimize information)
M2.evil(secrets, "stent").length    // => 1907
M2.evil(secrets, "horse").length    // => 1203

// Ranked by difficulty
M2.ranked_evil(secrets, "stent")    // => List("robot", "vigor", ...)
```

**Strategy**:
The "evil" strategy keeps the player guessing longest by:
1. Choosing responses that minimize information given
2. Selecting words with uncommon letter patterns
3. Maximizing the remaining possible secret words

---

## 🚀 Installation

### Prerequisites

- **Scala**: Version 2.12+ or 2.13+
- **Java JDK**: Version 8 or higher
- **scalac**: Scala compiler

### Install Scala

**macOS (via Homebrew)**:
```bash
brew install scala
```

**Linux (via SDKMAN)**:
```bash
curl -s "https://get.sdkman.io" | bash
sdk install scala
```

**Windows**:
Download from [scala-lang.org](https://www.scala-lang.org/download/)

### Verify Installation

```bash
scala -version    # Scala compiler version
java -version     # Java version
```

---

## ⚙️ Compilation & Execution

### Basic Compilation

```bash
# Compile single file
scalac filename.scala

# Compile to JAR
scalac filename.scala -d output.jar
```

### Run Compiled Code

```bash
# Run from JAR
scala -cp output.jar

# Interactive REPL
scala
> :load filename.scala
> ObjectName.functionName(args)
```

### Module-Specific Commands

**Brainf*** Interpreter**:
```bash
scalac bf.scala -d bf.jar
scala -cp bf.jar
> M5a.run(M5a.load_bff("mandelbrot.bf"))
```

**Collatz Conjecture**:
```bash
scalac collatz.scala
scala
> :load collatz.scala
> C1.collatz(27)
> C1.collatz_max(100000)
```

**Knight's Tour**:
```bash
scalac knight1.scala knight2.scala
scala
> :load knight2.scala
> M4b.first_tour_heuristics(8, List((0,0)))
```

**Expression Parser**:
```bash
scalac postfix2.scala
scala
> :load postfix2.scala
> C3b.compute(C3b.syard(C3b.split("4 ^ 3 ^ 2")))
```

**Regular Expressions**:
```bash
scalac re.scala
scala
> :load re.scala
> M3.matcher(("a" ~ "b") ~ "c", "abc")
```

**Wordle Solver**:
```bash
scalac wordle.scala
scala
> :load wordle.scala
> val secrets = M2.get_wordle_list("https://nms.kcl.ac.uk/christian.urban/wordle.txt")
> M2.evil(secrets, "stent")
```

---

## 🏗️ Technical Highlights

### Functional Programming Patterns

**Immutability**:
```scala
// Memory represented as immutable Map
type Mem = Map[Int, Int]
def write(mem: Mem, mp: Int, v: Int): Mem = mem + (mp -> v)
```

**Pattern Matching**:
```scala
def compute(prog: String, pc: Int, mp: Int, mem: Mem): Mem = {
  if (pc >= 0 && pc < prog.size) {
    prog(pc) match {
      case '>' => compute(prog, pc+1, mp+1, mem)
      case '<' => compute(prog, pc+1, mp-1, mem)
      case '+' => compute(prog, pc+1, mp, write(mem, mp, sread(mem, mp)+1))
      // ...
    }
  }
}
```

**Higher-Order Functions**:
```scala
def first(xs: List[Pos], f: Pos => Option[Path]): Option[Path]

// Usage
first(legal_moves(dim, path, pos), nxt => first_tour(dim, List(nxt) ++ path))
```

**Tail Recursion**:
```scala
@tailrec
def factorial(n: Int, acc: Int = 1): Int = {
  if (n <= 1) acc
  else factorial(n - 1, n * acc)
}
```

### Algorithm Optimizations

**Jump Table (Brainf***):**
```scala
// Pre-compute bracket matching: O(n) instead of O(n²)
def jtable(pg: String): Map[Int, Int] = {
  (0 to pg.size-1).toList
    .filter(i => pg(i) == '[')
    .map(x => x -> jumpRight(pg, x+1, 0))
    .flatMap(e => List(e, (e._2-1) -> (e._1+1)))
    .toMap
}
```

**Warnsdorff's Heuristic (Knight's Tour)**:
```scala
// Visit squares with fewest onward moves first
def ordered_moves(dim: Int, path: Path, x: Pos): List[Pos] = {
  legal_moves(dim, path, x)
    .sortBy(p => legal_moves(dim, path, p).size)
}
```

**Regular Expression Simplification**:
```scala
// Prevent exponential blowup in regex size
def simp(r: Rexp): Rexp = r match {
  case ALTs(orig) => ALTs_smart(denest(orig.map(simp).toList).distinct)
  case SEQs(orig) => SEQs_smart(flts(orig.map(simp).toList))
  case _ => r
}
```

---

## 📁 Project Structure

```
scala-assignments/
├── bf.scala                    # Brainf*** interpreter (basic)
├── bfs.scala                   # Brainf*** interpreter (optimized)
├── collatz.scala               # Collatz conjecture analysis
├── docdiff.scala               # Document similarity calculator
├── drumb.scala                 # Stock portfolio analyzer
├── knight1.scala               # Knight's tour (brute force)
├── knight2.scala               # Knight's tour (heuristics)
├── postfix.scala               # Shunting yard (basic)
├── postfix2.scala              # Shunting yard (with power)
├── re.scala                    # Regular expression matcher
├── wordle.scala                # Wordle evil solver
├── .gitignore                  # Git ignore patterns
└── README.md                   # This file

Optional data files:
├── mandelbrot.bf               # BF program: Mandelbrot set
├── sierpinski.bf               # BF program: Sierpinski triangle
├── benchmark.bf                # BF program: Performance test
├── collatz.bf                  # BF program: Collatz sequence
└── *.csv                       # Stock price data (for drumb.scala)
```

---

## 🧪 Testing Examples

### Run All Tests

```scala
// Collatz
assert(C1.collatz(27) == 111)
assert(C1.collatz_max(100)._1 == 119)

// Document Similarity
assert(C2.clean("Hello, World!") == List("Hello", "World"))

// Knight's Tour
assert(M4a.legal_moves(8, Nil, (2,2)).length == 8)
assert(M4a.legal_moves(8, Nil, (7,7)).length == 2)

// Expression Parser
assert(C3a.compute(C3a.syard(C3a.split("3 + 4 * ( 2 - 1 )"))) == 7)
assert(C3b.compute(C3b.syard(C3b.split("4 ^ 3 ^ 2"))) == 262144)

// Regular Expressions
assert(M3.matcher(("a" ~ "b") ~ "c", "abc") == true)
assert(M3.matcher(("a" ~ "b") ~ "c", "ab") == false)

// Wordle
assert(M2.iscore("chess", "caves") == 21)
assert(M2.iscore("chess", "swiss") == 20)
```

---

## 📚 Learning Outcomes

### Concepts Demonstrated

✅ **Functional Programming**
- Immutable data structures
- Higher-order functions
- Pattern matching
- Recursion and tail recursion

✅ **Algorithm Design**
- Backtracking (Knight's tour)
- Dynamic programming (memoization)
- Heuristic search (Warnsdorff's rule)
- Formal language theory (regex derivatives)

✅ **Data Structures**
- Maps and sets
- Trees (implicit in recursion)
- Stacks (in expression parsing)
- Graphs (chessboard as graph)

✅ **Optimization Techniques**
- Jump tables for O(1) lookup
- Code simplification
- Lazy evaluation
- Space-time tradeoffs

---

## 🎓 Academic Context

**Institution**: King's College London  
**Subject**: Advanced Functional Programming / Algorithms  
**Language**: Scala 2.x

**Copyright Notice**: This code is subject to copyright by King's College London. It is provided for educational reference and should not be redistributed or used for academic submissions.

---

## 📄 License

This project contains coursework assignments from King's College London. All rights reserved. This code is provided for educational and reference purposes only.

**Usage Restrictions**:
- ❌ Do not submit as your own coursework
- ❌ Do not redistribute without permission
- ✅ Use for learning functional programming
- ✅ Study algorithm implementations
- ✅ Reference for Scala syntax

---

## 🔗 Additional Resources

### Scala Documentation
- [Scala Language Specification](https://scala-lang.org/files/archive/spec/2.13/)
- [Scala API Documentation](https://www.scala-lang.org/api/current/)
- [Scala Style Guide](https://docs.scala-lang.org/style/)

### Algorithm Resources
- **Brainf*****: [esolangs.org/wiki/Brainfuck](https://esolangs.org/wiki/Brainfuck)
- **Knight's Tour**: [Warnsdorff's Rule](https://en.wikipedia.org/wiki/Knight%27s_tour#Warnsdorff's_rule)
- **Shunting Yard**: [Dijkstra's Algorithm](https://en.wikipedia.org/wiki/Shunting-yard_algorithm)
- **Regex Derivatives**: [Brzozowski's Method](https://en.wikipedia.org/wiki/Brzozowski_derivative)

---

**💡 Built with Scala | Functional Programming Excellence | Academic Excellence**
