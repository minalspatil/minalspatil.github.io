---
layout: post
title: Can an LLM write verified C code for safety-critical software?
date: 2026-11-27
description: What we found when we asked ten LLMs to generate C code for three real automotive modules and checked the results with formal verification.
tags: llm formal-verification automotive
---

Software in cars has to be correct, and standards such as ISO 26262 spell out how much evidence you need that it is. Large language models are good at producing code that looks right. The question in our NeSy 2025 paper, [Generating Safety-Critical Automotive C-programs using LLMs with Formal Verification](https://proceedings.mlr.press/v284/sevenhuijsen25a.html), was whether they can produce code that is provably right.

## The setup

We took three real, industrial, safety-critical automotive software modules and asked LLMs to generate C programs for them. We tried ten LLMs and four prompting techniques: zero-shot, zero-shot chain-of-thought, one-shot, and one-shot chain-of-thought.

Every generated program was checked in two ways:

- **Functional correctness** was assessed with functional verification, which checks the code against its specification.
- **Non-functional requirements**, such as how variables are accessed and scoped, were checked with an industrial static analyzer, together with human evaluation.

The point of putting formal verification behind the model is that it does not matter how the code was produced. If a program passes verification, it meets its specification. If it does not, it is rejected.

## What we found

It is feasible. LLMs can generate functionally correct code for these modules, but how often depends heavily on the module. Out of 800 attempts per module, the success rates were:

| Module | Functionally correct |
|---|---|
| 1 | 540 / 800 |
| 2 | 59 / 800 |
| 3 | 46 / 800 |

So roughly two thirds of attempts succeeded on the first module and under one in ten on the other two. Averages across a benchmark would have hidden that gap.

The generated programs also frequently met the non-functional requirements. When they did not, the deviations were typically of two kinds: violating a single-read or single-write access pattern, or using a wider variable scope than necessary.

## Takeaway

The results show both the promise and the limits of this approach. Verification gives a clear pass or fail, which is what makes LLM-generated code usable in a setting where correctness matters. At the same time, a success rate that varies from two thirds to a few percent shows how much room is left for better prompting, feedback loops, and models.

The full details are in [the paper](https://proceedings.mlr.press/v284/sevenhuijsen25a.html).
