---
layout: "layout"
title:  "OSP How to Add Weekly Assignments and Any Other Materials in General"
hide:
  - navigation
  - toc
---

## How to Add Weekly Assignments and Any Other Materials in General

### Adding Weekly Assignments

* **Create a New Markdown File**:  
   In the `docs/assignments` directory, create a new markdown file named in the format `W00-01.md`, where `W00` represents the week number and `01` is the assignment number.  
   Example: `W00-01.md` is the first assignment for week 0.

   **Folder Structure:**

```txt
  docs/
    assignments/
      W00-01.md
      W00-02.md
      ...
```

* **Add Front Matter**:  
   At the beginning of each markdown file, include the following front matter:

```yaml
  ---
  layout: "assignment"
  title:  "Week 00 - Assignment 01"
  hide:
    - navigation
    - toc
  ---
```

* **Add Assignment Content**:  
   After the front matter, add the details of the assignment.

   **Example:**

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

* **Create a Materials Folder**:  
   In the `docs` directory, create a folder named `materials` and add any relevant files (e.g., `slides.pdf`, `notes.md`).
   
   **Folder Structure:**

```txt
  docs/
    materials/
      slides.pdf
      notes.md
      ...
```

### Linking One Page to Another

To create links between pages, use the following markdown syntax:

```markdown
  [Link Text](path/to/page.md)
```

> **Note**: Do not include `docs` in the path, as it may prevent the link from working.

**Example**: To link from `W00-01.md` to a material called `Memory` in the `docs/materials` folder:

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
  - [Memory](materials/memory.md)
```
