# AGENTS.md

Instructions for AI coding assistants ("agents") working with this repository. This template is used both to **set up a new project** and to **convert an existing project** into the template's structure. These rules apply during both flows and to any later edits in a project created from this template.

## Rules that always apply

### 1. Keep the README YAML header and its metadata option lists

`README.md` starts with a YAML front-matter block. It is project metadata, not template filler. **Never remove it** — even when a request says to "clean up" or "finalize" the README. The header looks like this:

```yaml
---
title: New project template # Replace with the project name
status: active      # Options: active, waiting, paused, finished, cancelled, archived
category: research  # Options: research, clinical, education, personal, tooling
parent-project: # Name the parent project here
---
```

When adapting it:

- Replace `title` with the project's real name and drop the `# Replace with ...` hint.
- Set `status` and `category` to one of the documented values.
- **Keep the `# Options: ...` comments on `status` and `category`.** They show the valid values and must stay visible so they can be consulted later.
- Fill in `parent-project` or leave it empty when the project has no parent project.

The same rule applies to any other metadata field that documents its options: keep the options visible, do not strip the comment.

### 2. Ask before removing folders

The template ships with `data/`, `results/`, `src/`, and `doc/` (with `approvals/`, `manuscripts/`, `project-planning/`, and `protocols/` subfolders), each kept in version control by a `.gitkeep` file until it has real content.

Not every project needs every folder. Small projects often have no separate `data/`, approvals, or manuscripts. When a folder would end up unused:

1. **Ask the user** whether to keep it or remove it. Do not decide unilaterally, and do not delete a folder the user wants to keep.
2. Delete a folder (including its `.gitkeep`) only after the user agrees.
3. If a folder is removed, remove its row from the "Project layout" table in `README.md` so the table matches the actual structure.
4. Prefer collapsing unused `doc/` subfolders into `doc/` over leaving empty subfolders.

Remove a folder's `.gitkeep` file once the folder has real content.

### 3. Never destroy user content

- When converting an existing project, existing files and content are canonical. Adapt and move them; do not delete or overwrite them.
- Template placeholders and examples are meant to be replaced; the user's own content is not.

### 4. Follow the working practices

Follow the "Working practices" section of `README.md`: keep raw data unchanged in approved storage, never commit sensitive data or credentials, use descriptive filenames, and keep the project tracked in version control.

### 5. Keep the README description focused on purpose and methods

The Description section of `README.md` states the study's purpose and methods — design, participants, data collection, and analysis. It must not report findings, themes, or conclusions. Record those in `doc/notebook.qmd` or the manuscript instead.

### 6. Keep the README and notebook entries very short

- Keep the README Description to a few sentences and avoid detail that belongs in the notebook or manuscript.
- Keep each `doc/notebook.qmd` log entry to at most one sentence per dated item.
- Keep the most recent entry on top. Add each new dated entry above the older ones.
- Favour trimming over expanding. Retain only what a reader needs to get oriented.

### 7. Never use semicolons to split sentences

Do not use semicolons to join or split sentences in any prose written for this project (README, notebook, manuscript, and abstract text). Split them into separate sentences, or restructure the clause, instead.

### 8. Avoid AI tells when writing prose

When writing or revising prose for this project, check the wording against https://claudisms.ai/ and remove phrases and patterns that signal AI authorship.

### 9. Follow the coding conventions

These instructions apply when writing or reviewing code. Keep them in initialized projects even if the README's coding summary is removed. This section is self-contained and does not depend on README headings.

#### Functions, duplication, and names

Follow these Good Enough Practices:

- [Decompose programs into functions](https://carpentries-lab.github.io/good-enough-practices/03-software.html#decompose-programs-into-functions). Give each function one main task and clearly defined inputs and outputs. Pass inputs as arguments rather than relying on global state. Aim for functions that fit on one screen (about 60 lines) and take no more than five or six arguments. Treat these as prompts to consider decomposition, not rigid limits.
- [Eliminate duplication](https://carpentries-lab.github.io/good-enough-practices/03-software.html#be-ruthless-about-eliminating-duplication). Extract repeated logic into reusable functions instead of copying and pasting code. Group related values in vectors, lists, or data frames rather than creating variables such as `score1`, `score2`, and `score3`. Look for well-maintained libraries before reimplementing functionality, and test their relevant behaviour before relying on them.
- [Give functions and variables meaningful names](https://carpentries-lab.github.io/good-enough-practices/03-software.html#give-functions-and-variables-meaningful-names). Choose concise names that describe purpose or content. Avoid vague names such as `process_data` when a more specific name is possible, and avoid cryptic abbreviations. Short loop counters such as `i` are acceptable in a small scope. Objects used widely need more informative names.

#### R

- **Keep dependencies minimal.** Prefer base R when it provides a clear solution. Add a package only when it offers a meaningful benefit over existing tools, rather than loading a broad package collection for a single helper. Declare required packages in `src/DESCRIPTION` when using a local package, or document them in the project's setup instructions otherwise.
- **Use native pipes.** Write `|>` rather than `%>%`. Native pipes require R 4.1 or later. Ensure setup instructions reflect that requirement when pipes are used.
- **Use `gtsummary` for summary and statistical tables.** Do not introduce a competing table-summary package without a project-specific reason.
- **Use `ggplot2` for plots.** Do not introduce a competing plotting framework without a project-specific reason.
- Keep reusable analysis logic in functions with explicit arguments so it can be tested and called from scripts or Quarto documents without duplicating it.

## Setting up a new project

Complete these steps in order:

1. **Copy the template** into a folder named for the project. If the name is not clear from the request, ask.
2. **Adapt `README.md` sections**: replace the example text in each section with real project details and remove guidance that does not apply. Fill in or trim sections (Description, Team and contact, Data and approvals, Setup and workflow) rather than leaving prompt-style placeholders.
3. **Adapt the YAML header** as described in rule 1.
4. **Update `CITATION`**: replace the example with the actual author(s), year, and title. If the repository URL or DOI is unknown, leave `[URL or DOI]` as a placeholder and tell the user what is missing, rather than inventing a value.
5. **Update `LICENSE`**: replace `YEAR` and `AUTHOR OR ORGANISATION` and remove the "Template setup note (remove after initialization)" section. Licensing decisions need a human: if the user has not confirmed the license, flag in your summary that the rights holders must confirm, rather than guessing.
6. **Remove template-only content**: from `README.md`, remove the "Using this template" section and the `TEMPLATE-ONLY` / `PROJECT README` marker comments. **Do not remove the YAML header.** (The `LICENSE` setup note is handled in step 5.)
7. **Start the log in `doc/notebook.qmd`**: replace the placeholder entry with a first dated entry of decisions and next steps. Project details (description, data, methods) live in `README.md`, not the notebook — do not duplicate them. Keep the file.
8. **Resolve folders**: apply rule 2 to every folder that stays empty before finalizing. Update the "Project layout" table accordingly.
9. **Drop `.gitkeep` files** once their folder has content.

Do not run `git init`, create commits, or push unless the user asks.

## Converting an existing project

Treat the existing repository as the source of truth; the template provides structure:

1. **Assess** the existing layout and content before changing anything.
2. **`README.md`**: start from the existing README and merge it into the template's sections. Keep the user's content and drop template headings that do not apply. Add the YAML header per rule 1, deriving the title from the project (ask if it is ambiguous).
3. **Move, don't copy**: relocate existing files into `data/`, `doc/`, `results/`, and `src/` as appropriate. Ask the user before moves that could break references (for example, paths used by scripts, notebooks, or tools), and do not rearrange in a way that risks losing history.
4. **`LICENSE` / `CITATION`**: if the project already has them, keep them unless the user asks to adopt the template's. Never silently replace existing license or citation files.
5. **Template-only content**: if template files were copied in, remove the "Using this template" section and marker comments from `README.md` (keep the YAML header).
6. **Resolve folders**: apply rule 2 to any unused folders; update the "Project layout" table so it reflects the converted project.

## After initialization

- The setup and conversion sections above are one-time steps. Once a project copy is initialized, they may be removed from that copy's `AGENTS.md` to keep it short — but keep the "Rules that always apply" section.
- **Do not edit this file in the template repository itself.** The setup sections exist to be copied into new projects alongside the rest of the template.
- **Never delete `AGENTS.md` itself** during setup or conversion.
- The always-applicable rules (especially keeping the YAML header and asking before deleting folders) stay in force for the life of the project.
