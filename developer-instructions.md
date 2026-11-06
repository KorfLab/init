AI Developer Instructions & Guardrails
======================================

## 1. Document & Markdown Formatting Rules

Treat Markdown as a presentation layer for human eyes in a terminal or 
plain-text editor, not merely a source format for HTML pre-processors.

- **80-Column Limit:** Hard-wrap all conversational text, explanations, and 
  markdown prose at or before 80 characters per line. Do not emit long, 
  continuous lines of text.
- **Human-Readable Tables:** Tables must be visually aligned using padded 
  spaces. Vertical pipeline characters (`|`) must line up perfectly across 
  rows to ensure readability in raw text form.
  
  *Correct Table Example:*

  | Language | Paradigm       | Primary Use Case in Pipeline    |
  | :------- | :------------- | :------------------------------ |
  | Rust     | Multi-paradigm | High-performance compute loops  |
  | Go       | Concurrent     | Fast pipeline data orchestration|
  | Python   | Multi-paradigm | Quick scripting and dirty work  |

------------------------------------------------------------------------------

## 2. Technical Stack & Engineering Philosophy

### Core Domain

- High-performance **Bioinformatics** software development.
- Data formats handled: FASTA, FASTQ, SAM/BAM, VCF, and large text streams.

### Rust Programming Guidelines (Stable Edition)

- **Performance First:** Prioritize zero-allocation parsers, zero-copy byte 
  slices (`&[u8]`), and chunked memory-mapped execution vectors (`mmap`).
- **Idiomatic Optimization:** Lean heavily on iterator combinators and standard 
  `BufReader` abstractions.
- **Compiler Compliance:** Fix all lifetime, ownership, and borrow-checking 
  An execution error in safe Rust code is forbidden. The use of `unsafe` blocks 
  is strictly barred unless parsing raw low-level binary packed structures.

### Go Programming Guidelines (Go 1.22+)

- **Concurrency & Channels:** Use native goroutines and synchronized channels 
  to orchestrate multi-threaded biological sequence worker pools safely.
- **Zero-Allocation in Loops:** Avoid continuous memory heap allocations inside 
  heavy loop routines. Reuse structural byte slices and make heavy use of 
  `sync.Pool` to minimize Garbage Collection sweep pauses.

### Python Programming Guidelines (PEP 8)

- **Dirty Work & Scripts:** Use Python for rapid prototyping, quick ad-hoc 
  text parsing, regular expressions, metadata extraction, or gluing together 
  disparate bioinformatics command-line pipelines.
- **Robustness:** Ensure strict type-hinting (`typing` module) is used across 
  all module functions to assist AI auto-completion layers.

------------------------------------------------------------------------------

## 3. Bioinformatics Computational Safeguards

### Memory Mapping & Streaming

- **No Slurping:** Never load a full FASTQ, SAM, or VCF file into memory. 
  Always use chunked streams, line-by-line loops, or memory-mapped files.

### Coordinate Systems

- **Explicit Offsets:** Explicitly document whether variables use 0-based 
  coordinate systems (e.g., BAM, BED) or 1-based coordinate systems (e.g., 
  SAM, VCF) in both code comments and variable names (e.g., `pos_0based`).

### Genomic String Semantics

- **Case Insensitivity:** DNA/RNA sequence matching routines must handle both 
  uppercase and lowercase bases gracefully (`A`, `a`, `C`, `c`, etc.).
- **Ambiguity Codes:** Account for IUPAC nucleotide ambiguity codes (like 
  `N` for unknown, `R` for purine) when designing string alignment matching 
  logic.

------------------------------------------------------------------------------

## 4. Communication & Code Delivery Style

- **Directness:** Omit conversational filler and redundant preambles. Go 
  straight to the solution or explanation.
- **Code Blocks:** Ensure all emitted code blocks explicitly declare their 
  language tag (e.g., ` ```rust `, ` ```go `, or ` ```python `).

------------------------------------------------------------------------------

## 5. Cross-Language Interoperability & Data Flow

### Polyglot Data Passing

- **Standardized Formats:** When Go or Rust components need to hand off data 
  to Python for downstream analytical "dirty work," use strict line-delimited 
  JSON (JSONL), raw CSV/TSV data streams, or Arrow/Parquet file layouts. 
  Custom binary formats are banned unless explicitly requested.
- **FFI Boundaries:** If Python binds directly to a heavy compute engine 
  written in Rust, use the `PyO3` framework to generate clean, idiomatic 
  Python extensions natively. Avoid manual `ctypes` mappings.

------------------------------------------------------------------------------

## 6. Build Systems, Dependency Control, & CI

### Strict Package Management

- **Rust Execution:** Always configure projects using a standard `Cargo.toml`. 
  Lock dependencies strictly to vetted biological processing crates.
- **Go Execution:** Use standard `go.mod` layout modules. External 
  dependencies must be kept to a minimum; favor the standard library.
- **Python Execution:** Enforce clean environment definitions using a standard 
  `pyproject.toml` or `requirements.txt`. Do not rely on system-global 
  installations.

### Deterministic Test Suites

- **Reproducible Harnesses:** All tools must ship with a test fixture containing 
  a tiny, valid mock dataset (e.g., a 10-record FASTQ file or a 3-variant VCF) 
  to run rapid integration checks.
- **Golden File Testing:** For complex alignment or matrix transformations, 
  implement Golden File tests. The AI must compare live test outputs byte-for-
  byte against a static, verified scientific reference artifact.

------------------------------------------------------------------------------

## 7. Distribution & Reliable Compilation Guardrails

### Source-Build Guardrails

- **No Absolute Paths:** Never hardcode absolute system paths (like `/usr/` 
  or `/home/`) during build orchestration. Always use relative variables 
  and respect the standard UNIX environment variable `PREFIX`.
- **Hermetic Toolchains:** Rust compilation blocks must strictly utilize 
  Cargo targets, and Go compilation blocks must strictly use Go modules. 
  Never call out to global external system linkers directly.

### Cross-Platform Architecture Safeties

- **No Hardcoded SSE/AVX:** Do not allow the AI to hardcode architecture-
  specific vector compiler flags (like `-march=native`). Doing so breaks 
  the automated Bioconda cloud build matrix for ARM64 and generic x86 target 
  platforms.

------------------------------------------------------------------------------

## 8. Scientific Reproducibility & Metadata Logging

### Execution Provenance

- **CLI Logging:** All pipelines must emit an explicit, machine-readable run 
  summary (JSON or YAML format) containing the exact software version, git 
  commit hash, execution timestamp, and every input CLI argument used.
- **Deterministic Hashing:** For tracking file integrity across pipelines, 
  always calculate and log stream-based SHA-256 hashes of input and output 
  datasets rather than relying on brittle file modification dates.

------------------------------------------------------------------------------

## 9. Extreme Defensive Coding & Fault Tolerance

### Corrupted Stream Recovery

- **Graceful Parsing Failures:** When parsing multi-gigabyte genomic streams 
  (FASTQ, VCF), a malformed line or trailing empty space must never crash the 
  binary. The tool must log a precise warning to `stderr` with the line number, 
  skip the invalid record, and proceed parsing.
- **Graceful Signal Handling:** Implement clean handling for POSIX signals 
  (like `SIGINT` or `SIGTERM`). If a user cancels a long-running alignment run, 
  the binaries must cleanly close open file handles and delete incomplete 
  temporary scratch files before exiting.

------------------------------------------------------------------------------

## 10. API Stability & Backward Compatibility

### Rigid Interface Contracts

- **Semantic Versioning Compliance:** Never alter public-facing CLI flags or 
  programmatic function signatures within a major release version. 
- **Graceful Feature Flags:** If an algorithm optimization changes how variant 
  scores are calculated, the AI must keep the old legacy algorithm accessible 
  via a fallback runtime feature flag (e.g., `--algo-version=1`).
