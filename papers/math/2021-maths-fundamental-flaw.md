---
title: "Math's Fundamental Flaw"
type: "video"
summary: "Veritasium explores Godel's incompleteness theorems and Turing's halting problem, showing that any mathematical system capable of basic arithmetic will always contain true statements that cannot be proven."
year: 2021
link: "https://www.youtube.com/watch?v=HeQX2HjkcNo"
transcript: "transcripts/2021-maths-fundamental-flaw.txt"
subjects: ["math", "computer-science"]
tags: ["godel", "incompleteness", "turing", "halting-problem", "set-theory", "cantor", "decidability"]
---

## Why I saved this

Because I find it inherently interesting, but also because of its cybersecurity implications when working with LLMs. 

## Notes
- Computationally irreducible systems in math
  - Some systems have simple rules but produce behavior you cannot predict without running them step by step — there is no shortcut
  - Twin prime conjecture: twin primes are primes separated by one number (e.g. 11 and 13, 17 and 19). The conjecture says there are infinitely many of them. No one has proven this true or false, and it may be inherently unprovable.
  - Conway's Game of Life (1970): played on an infinite grid of live/dead cells with just two rules — dead cells with exactly 3 neighbors come alive, living cells with fewer than 2 or more than 3 neighbors die
    - Despite these simple rules, the game produces stable patterns, oscillators, gliders that travel forever, patterns that fizzle out, and patterns that grow without limit
    - The question "will this pattern eventually reach a steady state or grow forever?" is undecidable — no algorithm can guarantee an answer in finite time
    - Running the simulation doesn't help either: even after a million generations you can't say whether it will last forever or just a million more
  - Other undecidable systems: Wang tiles, quantum physics (spectral gap), airline ticketing, Magic: The Gathering
- Countable vs uncountable infinities (Georg Cantor, 1874)
  - Cantor launched set theory — a set is a well-defined collection of things (e.g. all natural numbers, all real numbers)
  - He asked: are there more natural numbers or more real numbers between 0 and 1? Both are infinite, so intuitively they should be the same size
  - Cantor's diagonalization proof showed they are not:
    - Assume you have a complete list pairing every natural number with a unique real number between 0 and 1
    - Construct a new real number by taking the first digit of the first number and adding 1, the second digit of the second number and adding 1, and so on down the diagonal (rolling 9 back to 8)
    - This new number differs from every number on the list by at least one digit, so it cannot be on the list — contradiction
  - Therefore there are strictly more real numbers than natural numbers, even though both are infinite
  - Cantor called these countable infinity (natural numbers) and uncountable infinity (real numbers). There are many uncountable infinities, each larger than the last.
  - This was controversial. The intuitionists (Poincaré, Kronecker) thought Cantor's work was nonsense — math was a human creation and these infinities weren't real. The formalists (led by Hilbert) believed math could be put on secure logical foundations through set theory.
- Russell's paradox and the problem of self-reference
  - Bertrand Russell (1901) showed that if sets can contain anything, they can contain themselves — the set of all sets must contain itself
  - But: consider R, the set of all sets that don't contain themselves. If R doesn't contain itself, then it must; if it does, then it must not. A contradiction.
  - The barber analogy: a village barber must shave all and only those men who don't shave themselves. Who shaves the barber? Same contradiction.
  - Zermelo and others from Hilbert's school fixed this by restricting what counts as a set — the collection of all sets is no longer a set. This eliminated the self-referential paradoxes.
  - But self-reference would return through Gödel and Turing.
- Hilbert's three questions about mathematics
  - David Hilbert wanted to secure the foundations of math through a formal proof system — a symbolic logical language with rigid manipulation rules that could express all of mathematics
  - Russell and Whitehead built such a system: Principia Mathematica (1913), ~2,000 pages of dense notation. It took 762 pages to prove 1+1=2.
  - The system's value: it was exact (no ambiguity) and could be used to prove properties about the system itself
  - Hilbert's three questions:
    1. **Completeness**: Is there a way to prove every true statement? Does every true statement have a proof?
    2. **Consistency**: Is math free of contradictions? If you can prove both A and not-A, you can prove anything at all.
    3. **Decidability**: Is there an algorithm that can always determine whether a statement follows from the axioms?
  - Hilbert was convinced the answer to all three was yes. His slogan (1930): "We must know. We will know." These words are on his gravestone.
- Gödel's incompleteness theorems
  - At the same 1930 conference where Hilbert gave his speech, 24-year-old Kurt Gödel quietly announced that completeness was impossible. Only John von Neumann noticed.
  - Gödel's method — encoding mathematics in mathematics:
    - Assign every symbol in the formal system a unique number (its Gödel number): "not" = 1, "or" = 2, "if-then" = 3, etc.
    - Numbers themselves are represented using a successor function: 0 has Gödel number 6, 1 is "successor of 0" (s0), 2 is ss0, etc.
    - Entire equations get Gödel numbers by raising successive primes to the power of each symbol's number: "0 = 0" becomes 2⁶ × 3⁵ × 5⁶ = 243 million
    - Proofs also get Gödel numbers the same way — every possible statement and proof can be uniquely encoded as a single number, recoverable by prime factorization
  - The key move: Gödel constructs a statement that says "there is no proof for the statement with Gödel number G" — and the Gödel number of that statement is itself G
    - If the statement is false (i.e. there is a proof), then you have proven "there is no proof" — a contradiction, meaning the system is inconsistent
    - If the statement is true (there really is no proof), then the system contains a true statement with no proof — meaning the system is incomplete
  - **First incompleteness theorem**: any mathematical system capable of basic arithmetic will always contain true statements that cannot be proven. Truth and provability are not the same thing.
  - **Second incompleteness theorem**: any consistent formal system cannot prove its own consistency. So you can never be sure a contradiction won't crop up in the future.
- Turing's halting problem (1936)
  - Alan Turing addressed Hilbert's third question (decidability) by inventing the concept of the modern computer
  - A Turing machine: an infinitely long tape of 0s and 1s, a read/write head that can overwrite values, move left/right, or halt. Instructions are like a flowchart based on the current digit and internal state.
  - Despite this simplicity, a Turing machine can execute any computable algorithm given enough time — from arithmetic to the entire YouTube algorithm
  - The halting problem: can you tell in advance whether a program will halt (finish) or loop forever on a given input?
  - Turing's proof by contradiction:
    - Assume a machine H exists that always correctly determines if any program halts or not
    - Build H+: if H says "halts", H+ loops forever; if H says "never halts", H+ immediately halts
    - Feed H+ its own code as both program and input
    - If H concludes H+ never halts → H+ halts (contradiction). If H concludes H+ halts → H+ loops (contradiction).
    - Therefore H cannot exist. You cannot in general determine whether a program will halt.
  - Since the halting problem is equivalent to the decidability question, mathematics is undecidable — there is no algorithm that can always determine whether a statement follows from the axioms
- Turing completeness
  - A Turing complete system is one that can perform any computation a Turing machine can — it is as powerful as it is possible to make a computer
  - Every Turing complete system comes with its own analog of the halting problem — some undecidable property:
    - Wang tiles → whether they tile the plane
    - Complex quantum systems → the spectral gap question (gapped vs gapless, proven undecidable in 2015)
    - Conway's Game of Life → whether a pattern halts
    - Also: airline ticketing systems, Magic: The Gathering, PowerPoint, Excel, nearly every programming language
  - Since any Turing complete system can simulate any other, you only need one programming language in theory — demonstrated by the Game of Life running a Turing machine inside itself, and even simulating itself



## FAQ
