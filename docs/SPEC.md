# Ghostext Paper Specification

## Overview

Write a research paper about Ghostext, an almost perfect steganography system that uses large language models and arithmetic coding to hide secret messages in generated text.

## Paper Style Guidelines

- **Language**: English throughout
- **Format**: LaTeX following CCS 2026 conference format (ACM Master Article Template)
- **Document Class**: Use `acmart` class with `sigconf,review,anonymous` options for double-blind review
- **Tone**: Friendly and accessible. Use simple, clear vocabulary rather than overly complex academic jargon.
- **Goal**: The paper should explain the system clearly while still being academically rigorous.

### CCS 2026 LaTeX Format Requirements

**Document Setup:**
```latex
\documentclass[sigconf,review,anonymous]{acmart}
\usepackage{graphicx}
\usepackage{url}
\usepackage{booktabs}
\usepackage{times}

% For anonymity in double-blind review
\ccsSubmissionID{12345}
\ccsPaperID{1234}
\ccsISBN{978-1-4503-XXXX-X/XX/YY}

\begin{document}
\title{Ghostext: An Almost Perfect Steganography via Large Language Model and Arithmetic Coding}
% Remove author info for anonymous review
\author{}
\maketitle
\begin{abstract}
...
\end{abstract}

\section{Introduction}
...

\section{Related Work}
...

\section{System Description}
...

\section{Security Analysis}
...

\section{Technical Approach}
...

\section{Experiments}
...

\section{Conclusion}
...

\bibliographystyle{acmauthory}
\begin{thebibliography}{references.bib}
...
\end{thebibliography}

\end{document}
```

**Key Requirements:**
- Use 10pt font size
- Double-column format (acmart handles this automatically)
- Page limit: 12 pages total (including references)
- Use PDF/A format for final submission
- Ensure all figures and tables are readable
- Include keywords for indexing
- Use ACM reference style (acmauthory)

**Build Commands:**
- `pdflatex paper.tex` - Generate PDF
- `bibtex paper` - Generate bibliography

**Template Availability:**
- Download from: https://www.acm.org/publications/proceedings-template
- File: `acmart.cls` must be in the same directory

## Title

"Ghostext: an almost perfect steganography via large language model and arithmetic coding"

(This title can be modified if you find a better alternative)

## System Description

Ghostext involves three parties: Alice, Bob, and Censor.

Alice uses a prompt, a password, and a secret message to call the Ghostext system, which produces a cover text. When the censor Censor examines this text, they see nothing unusual - it passes through censorship undetected. Bob, using the same prompt and password, can recover the secret message from the text.

## Security Model

The security is defined against a passive censor who can observe the text itself but does not have knowledge of the prompt or password. The goal is that the censor cannot distinguish between text containing the hidden message and natural language text.

Technically, this is achieved in two ways. First, the large language model produces a distribution that is close to natural language text. Second, the encryption process does not disrupt the model's next-token prediction distribution.

## Technical Approach

The system uses two main tools: encryption and arithmetic coding.

Encryption makes the hidden message indistinguishable from random bits. This ciphertext serves as the source for selecting tokens from the next-token prediction distribution.

Arithmetic coding fully exploits the entropy of the distribution, encoding the message completely into the model's token choices.

The key claim is that this approach is "almost perfect" because it preserves the LLM's next-token prediction distribution without modification while maximizing entropy utilization. This makes the steganography scheme highly effective.

## Related Work

Research and reference:
- LLM steganography papers
- LLM watermarking papers (the underlying techniques are closely related)

## Experiments

Run experiments to demonstrate that the system works:
- Use only the llm backend (the toy backend is purely for testing and should not appear in the paper)
- Report basic data and parameters
- Show round-trip success rates, bits per token, and timing information

The Ghostext code in `../Ghostext` has both a toy backend and an llm backend. Only use the llm backend for the paper experiments.

## Plan and Milestones

After completing each milestone, save progress with:
```bash
git add .
git commit -m "descriptive message"
git push
```

### Milestone 1: Initial Investigation
- Explore the Ghostext codebase to understand its structure
- Run basic encode/decode tests to verify the system works
- Collect initial statistics on capacity and performance

### Milestone 2: Related Work Survey
- Research LLM steganography papers
- Research LLM watermarking papers
- Summarize key techniques and how they relate to Ghostext

### Milestone 3: First Draft
- Write the introduction section
- Write the system description
- Write the security analysis
- Write the technical approach section

### Milestone 4: Experiments and Results
- Run experiments with the llm backend
- Collect and analyze data
- Write the experiments section with results

### Milestone 5: LaTeX Conversion and Final Polish
- Convert paper to CCS 2026 LaTeX format
- Use acmart class with sigconf,review,anonymous options
- Ensure all sections are properly formatted
- Compile with pdflatex to verify PDF generation
