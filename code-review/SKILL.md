---
name: code-review
description: Review code for requirements fulfillment, general and logical correctness, stack-specific good practices, and consistency with codebase specifications, documentation, and patterns. Apply implicitly whenever performing a code review, including pull requests, diffs, proposed patches, and self-review of implementation changes.
---

# Code Review

Evaluate the code against its intended behavior and the repository's actual constraints. Review all five dimensions below; passing tests alone does not establish correctness.

## Establish the Review Context

- Identify the review scope and comparison base when applicable. Read the changed code alongside relevant callers, dependencies, types, and tests to understand its effects.
- Read applicable `AGENTS.md` instructions, requirements, acceptance criteria, specifications, and relevant repository documentation. Inspect nearby implementations for established patterns.
- Identify the stack and dependency versions from manifests, lockfiles, and configuration. Assess practices against the versions and conventions in use; consult authoritative documentation when a consequential API or framework behavior is uncertain.
- Distinguish explicit requirements, documented conventions, and inferred intent. If sources conflict or requirements are missing, state the uncertainty and ask only when it prevents a sound conclusion. Do not invent requirements or silently choose between conflicting specifications.

## Review Dimensions

### Requirements Fulfillment

Trace each applicable requirement and acceptance criterion to observable behavior and supporting evidence. Look for omitted cases, partial implementations, unintended scope changes, and missing integration across affected layers. Explicitly identify requirements that cannot be verified from available evidence.

### General Code Correctness

Check implementation and integration defects: contracts and types, invalid or missing inputs, error propagation, resource cleanup, state changes, compatibility, and regressions in affected consumers. Consider security, data integrity, concurrency, and performance where the code makes them relevant.

### Tech Stack Good Practices

Check correct use of the project's language, framework, libraries, and tools, including lifecycle rules, asynchronous behavior, resource ownership, dependency boundaries, and supported APIs as applicable. Prefer established project tooling and idioms. Tie recommendations to a concrete risk, documented convention, or maintainability cost; do not present personal preferences or optional modernization as defects.

### Logical Correctness

Walk through the behavior independently of syntax and type checks. Trace representative success, failure, boundary, and repeated-operation cases. Check conditions, algorithms, invariants, state transitions, ordering, calculations, and units where relevant. Test whether the implementation can produce a plausible but incorrect result, including when its tests pass.

### Codebase Consistency and Documentation

Compare the change with relevant specifications, architecture decisions, documentation, and established implementations. Check that it follows applicable module boundaries, shared abstractions, naming, validation, error handling, and testing patterns. Identify implementation/documentation drift and missing updates to affected contracts or examples. Do not copy an existing defect merely for consistency, or treat an isolated example as a mandatory convention.

## Verify Findings

- Use focused repository checks, tests, type checking, linting, or builds as appropriate to the affected behavior. Inspect whether tests assert the required outcome and meaningful failure cases, rather than merely reproducing the implementation.
- Substantiate suspected defects with a concrete input, execution path, contract violation, or reproduction. Distinguish confirmed problems from unresolved questions and optional suggestions.
- Keep review scope separate from repair scope: a review request alone does not authorize code edits. When fixes are also requested, verify the resulting changes against the same dimensions.

## Report

Follow any required review format. Otherwise, lead with actionable findings ordered by severity, each with a precise file/line reference, the triggering condition, the impact, and a concise correction direction. Avoid speculative findings and preference-only noise. Distinguish introduced defects from relevant pre-existing issues.

Briefly account for all five dimensions, grouping those with no findings. State which checks actually ran, their results, and any unverified requirements or limitations. If no actionable findings remain, say so without claiming unperformed checks passed or guaranteeing correctness.
