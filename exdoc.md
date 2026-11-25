exdoc
=====

An expectation-driven framework for human-AI problem-solving

## Abstract

- **Core**: a project should be initiated by human intent
- **Anatomy**: projects are structured as living documents
- **Goal**: humans work with AI to iteratively improve the document
- **Anti-Goal**: the document is not a chat log, but the defining truth

## Specification

### 1. Initial Spec

Name the project as a single token. The name should correspond to a file or
directory name and live within a GitHub repo. For example, this project is
named "exdoc", it lives inside a file called `exdoc.md`, which is part of the
`KorfLab/init` repo.

### 2. Abstract

Write 3-5 bullet points in the Abstract defining your intent. Do not use AI
when first defining your intent.

### 3. Golden Path

Write a few examples of how the product should work.

### 4. Edge Cases

Write a few examples of edge cases that might break the product.

### 5. Constraints

Write a few constraints to help you guide AI and your future interactions.

### 6. Commit

Before you start prompting and iteratively improving the executable document,
`git commit` the original document as its initial version.


## Iterative Refinement

1. Feed the document to AI to create an implementation
2. Test the implementation with as much imagination as you have
3. If the output surprises you, update the specification

