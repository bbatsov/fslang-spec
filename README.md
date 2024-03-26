# fslang-spec
F# Language Specification

## Overview

This is an initiative to create a more complete and community-maintainable F# spec.

This will be no small task, but we believe it is worthwhile and we count on community contributions.

We foresee three phases:
1. Convert the [latest official spec](https://fsharp.org/specs/language-spec/4.1/FSharpSpec-4.1-latest.pdf) to markdown and create the structure and tools to make it community-maintainable. This is ongoing work, details see below.
2. Add the post-4.1 features as documented in the [RFCs](https://github.com/fsharp/fslang-design/) to the spec. Our goal: a complete F#9 spec.
3. Make spec update part of new feature development so that an up-to-date spec can be released with every new major compiler release.

## Process

The spec is in the end closely coupled to the language design and therefore needs a) strong community contributions and b) a clearly defined final responsibility, which will be similar to the one of the [language design process](https://github.com/fsharp/fslang-design?tab=readme-ov-file#who-is-in-charge).

We foresee the following types of contributions:

- For Phase 1, PRs that add a converted chapter.
- Issues and/or PRs for bug fixes.
- PRs for integration of an accepted and implemented RFC.
- Issues for proposing and discussing smaller or larger improvements to the spec
- PRs for such improvements, once the discussion converges and/or is decided by the team in charge

All PRs need to be accepted by two team reviewers for merging.

## Repository structure

The sources are the markdown files for the chapters (clauses) in the `spec` directory.
Run `build` to create a new complete spec (including ToC and updated reference links) in your `artifacts` directory.

At certain points, releases are created and published in the `releases` directory.

## Guidelines for Phase 1 contributions

- If you want to convert a clause (chapter), announce that by a PR that puts you into the table below.
- Copy the content of that chapter from "2018-spec-autogenerated-from-pdf.md" to a separate .md file. The filename is the standard conversion of the header text to a linkable name (e.g. "Program Structure" => "program-structure").
- Do the necessary manual conversion, specifically
    - Add indentations to code examples and to syntax
    - Add `fsharp` or `fsgrammar` info string to code block fences for code and syntax, resp.
        <br> Add `csharp` for C# code and `fsother` for the few other cases.
    - Note that the auto-converter has turned the syntax blocks into code blocks and thus dropped the italics in the syntax. We keep it that way.
    - Turn all blue items in text paragraphs (blue color in the pdf spec) into code spans (i.e. enclose them in back ticks). Drop the italics also here.
    - Subscripts in the pdf (like in `expr₁`) are typically auto-converted to `expr 1`. We don't support subscripts and just remove the space (`expr1`). An exception is the "opt" suffix, which we convert into ~opt (e.g. `expr~opt`), so that we can later easily deal with it differently by using search-and-replace.
    - Also drop the underlining of "Elaborated Expressions".
    - Reconstruct tables (using GFM (github flavoured markdown)). In code spans inside tables, replace `|` by `∣` (U+2223).
    - Start notes with `> Note: `
    - Check for occasional problems in the auto-converted version (for example missing spaces around dashes), or extra spaces.
    - Add spaces back to table like syntax definitions (like in the operator lists in section 4.1)
    - Revert headings back from all caps to normal capitalization (CONSTANTS -> Constants)
    - Adjust heading levels (# 1. / ## 1.1 / ### 1.1.1)
    - Keep references as they are (like `(see §9.1)`), no space between the `§` and the number, as they will are automatically converted by the CreateLinks script (see below).
- Add the new filename (without the .md suffix) to `Clauses.json`
- In the root directory, run `dotnet fsi CreateLinks.fsx <yourChapter.md>`.
    > This needs to be done only once during baseline creation. It changes your source file. It removes the section numbers in the headings and add links to all §x.x references. The operation, however, is idempotent.
- In the root directory, run `build`, this will update `spec.md` in the `artifacts` directory, complete with ToC and reference links.

### Conversion status

| Clause | Owner | Status | Review | Remarks |
| --- | --- |--------| --- | --- |
| introduction | Martin521 | done   |
| program-structure | Martin521 | done   |
| lexical-analysis | Martin521 | done   |
| basic-grammar-elements | Martin521 | done   |
| types-and-type-constraints | edgarfgp | done  |
| expressions | Martin521 | done    |
| patterns | Martin521 | done   |
| type-definitions | Martin521 | done |
| units-of-measure | Martin521 | done |
| namespaces-and-modules | Martin521 | done |
| namespace-and-module-signatures | Martin521 | wip |
| program-structure-and-executions |
| custom-attributes-and-reflection |
| inference-procedures |
| lexical-filtering |
| provided-types |
| special-attributes-and-types |

