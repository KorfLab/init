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

When data is presented in Markdown, use code blocks with the file type on the
first line. For example, a fasta file follows:

```fasta
>seq
GAATTC
```

------------------------------------------------------------------------------

## 2. Bioinformatics Computational Safeguards

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

## 3. Distribution & Reliable Compilation Guardrails

### Source-Build Guardrails

- **No Absolute Paths:** Never hardcode absolute system paths (like `/usr/`
  or `/home/`) during build orchestration. Always use relative variables
  and respect the standard UNIX environment variable `PREFIX`.

### Cross-Platform Architecture Safeties

- **No Hardcoded SSE/AVX:** Do not allow the AI to hardcode architecture-
  specific vector compiler flags (like `-march=native`). Doing so breaks
  the automated Bioconda cloud build matrix for ARM64 and generic x86 target
  platforms.

------------------------------------------------------------------------------
