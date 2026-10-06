# project_lifecycle.tex — TikZ figure: the lifecycle of a project under ComplexGitSync

*Source: `docs/figures/project_lifecycle.tex`*

Written by hand rather than by `scripts/tikz2mermaid.py`, whose conversion of
this figure drops the fitted Operating Space box and the edge into it. This is
the same diagram as the root `README.md`'s *The project lifecycle*; keep the
two identical.

```mermaid
flowchart LR
    SRC["<b>1. Describe</b><br/>.cgs specification<br/>or .gts recorded State"]
    SRC ==>|"<b>2. Materialise</b><br/>cgitsync bootstrap<br/>(nested: initialise)"| OS

    subgraph OS["<b>3. Operating Space</b> — the project's local file system (CGSHOME)"]
        direction TB
        Root["my-project/<br/>root repo"] --> Src["src/<br/>repo"]
        Root --> Doc["docs/<br/>repo"]
        Root --> Data["data/<br/>repo"]
        Root --> Agent[".agent/rules/<br/>private repo"]
        Doc --> Tuto["docs/tutorials/<br/>nested repo"]
    end

    OS ==>|"<b>4. Work</b><br/>edit, build, compute,<br/>analyse — any tool"| WORK["modified<br/>project files"]
    WORK ==>|"<b>5. Persist</b><br/>cgitsync add · commit<br/>push · tag"| STATE["new State<br/>.gts snapshot<br/>+ memory ledger"]
    STATE -.->|"restore, here or<br/>on another machine"| SRC
```
