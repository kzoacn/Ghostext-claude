# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains the Ghostext research paper. Ghostext is a text steganography system using large language models and arithmetic coding.

## Dependencies

The Ghostext implementation is in `../Ghostext`. Do not modify the Ghostext code - it already works.

## Main Task

Write a research paper about Ghostext following the specifications in `docs/SPEC.md`.

## Key Points

- Write the paper in English
- Use natural language paragraphs, not bullet points
- Keep vocabulary simple and friendly
- Title: "Ghostext: an almost perfect steganography via large language model and arithmetic coding" (can be modified)
- Only use the llm backend for experiments - toy backend is for testing only
- The paper should claim "almost perfect" steganography because it preserves the LLM's next-token distribution while maximizing entropy usage

## Milestones

See docs/SPEC.md for the detailed plan. After completing each milestone:
- `git add` the changes
- `git commit` with a descriptive message
- `git push` to save progress
