# OneCX Docs: Guidelines

These guidelines provide a framework for creating clear, consistent and user-friendly documentation for OneCX projects using [Antora](https://docs.antora.org/antora/latest/) and [AsciiDoc](https://docs.asciidoctor.org/asciidoc/latest/).  
They are designed to help authors produce high-quality content that meets the needs of our users and contributors.

## [](#core-guidelines)Core Guidelines

Simplicity

Keep content straightforward and focused on user needs.  
\= No prosaic explanations.  
\= Follow the [KISS](https://en.wikipedia.org/wiki/KISS%5Fprinciple) principle.

Clarity

Write clear, concise instructions with examples, code snippets, and visuals.

Consistency

Use a uniform structure, style, and terminology to make docs easy to navigate.  
\= Check linked resources before publish your docs.

Modularity

Organize content into reusable modules and partials for maintainability.  
\= Leverage includes and partials to avoid duplication

Navigation

Provide intuitive navigation with a well-structured sidebar and cross-references.  
\= Use meaningful link text instead of raw URLs.  
\= Use xref: for internal links.  
\= Ensure all links are valid and up-to-date.  
\= Do not use excessively deep nesting levels – a maximum of 3-4 levels.

Readability

Use formatting, headings, lists, and visuals as used within the reference implementation to enhance comprehension.  
\= Avoid using your own formatting styles that differ from the reference implementation.

Error-free

Proofread content to eliminate typos, grammatical errors, and technical inaccuracies.  
\= Check console output after building the website.

## [](#contribution-workflow)Contribution Workflow

* Start with small, focused PRs; write clear descriptions.
* Reference issues when applicable; include screenshots for UI docs.
* Follow existing repository lint/format rules; keep diffs minimal.
* Review feedback constructively; iterate promptly.
* Prefer evergreen docs that age slowly; call out version specifics.

## [](#anti-patterns-to-avoid)Anti-Patterns to Avoid

* Overly complex explanations that confuse users.
* Inconsistent terminology or formatting that hinders navigation.
* Redundant content that could be modularized.
* Broken links or outdated references.
* Own formatting styles that differ from the reference implementation.
* Nested headings beyond 3-4 levels
* Using whitespaces in directory/file names

## [](#writing-style)Writing Style

For detailed writing style guidelines, see the [OneCX Docs: Writing Style](writing%5Fstyle.html) document.

## [](#reference)Reference

The **reference implementation** is the documentation of [OneCX Local Environment](../onecx-local-env/index.html).  
Follow the idea of structure, used [AsciiDoc](https://docs.asciidoctor.org/asciidoc/latest/) features, navigation and conventions.
