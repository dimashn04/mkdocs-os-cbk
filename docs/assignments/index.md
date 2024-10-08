---
layout: "layout"
title:  "OSP How to Add Weekly Assignments and Any Other Materials in General"
hide:
  - navigation
  - toc
---

## How to Add Weekly Assignments and Any Other Materials in General

### Adding Weekly Assignments

Create a new markdown file in the `docs/assignments` directory. The file name should be in the format `W00-01.md`, where `W00` is the week number and `01` is the assignment number. For example, `W00-01.md` is the first assignment for week 0.
  
Folder structure:

```txt
  docs/
    assignments/
      W00-01.md
      W00-02.md
      ...
```

Add the following front matter to the markdown file:

```yaml
  ---
  layout: "assignment"
  title:  "Week 00 - Assignment 01"
  hide:
    - navigation
    - toc
  ---
```

After the front matter, add the content of the assignment.

Example:

```markdown
  ---
  layout: "assignment"
  title:  "Week 00 - Assignment 01"
  hide:
    - navigation
    - toc
  ---

  ## Week 00 - Assignment 01
  Please complete the following tasks:
  1. Task 1
  2. Task 2
```

### Adding Other Materials

Create another folder in the `docs` directory for the materials. For example, `docs/materials`. Add the materials in the folder and link to them in the markdown files.

Folder structure:

```txt
  docs/
    materials/
      slides.pdf
      notes.md
      ...
```

### Linkking One Page to Another

To link one page to another, use the following markdown syntax:

```markdown
  [Link Text](path/to/page.md)
```

Note: Do not include `docs` in the path. It may not work.

Example for linking a page from W00-01.md to W00-02.md:
In this example assignment 1 refers a material in Parent Process material. The Parent Process material is located at `docs/material`

```markdown
  ---
  layout: "assignment"
  title:  "Week 00 - Assignment 01"
  hide:
    - navigation
    - toc
  ---

  ## Week 00 - Assignment 01
  Please complete the following tasks:
  1. Task 1
  2. Task 2

  Materials:
  - [Parent Process](materials/parent-process.md)
```
