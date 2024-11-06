---
layout: "layout"
title:  "Documentation"
hide:
  - navigation
  - toc
---

## How to Prepare the Source Code

1. **Download the Source Code:**  
   Click the link below to download the latest version of the source code as a ZIP file:  
   [Download Source Code](https://github.com/cbk2000/mkdocs-os-cbk/archive/refs/heads/master.zip)

2. **Extract the ZIP File:**  
   Once downloaded, unzip the `mkdocs-os-cbk-master.zip` file to access the source code files.

3. **Follow the steps below**

## How to Install Requirements for MkDocs

To set up MkDocs and `mkdocs-material` theme, run these commands:

```bash
pip install mkdocs
pip install mkdocs-material
```

## How to Run MkDocs in a Web Browser

After installation, you can start the MkDocs development server to preview your documentation locally.

The command `mkdocs serve` launches a built-in server for easy preview and development.

```bash
mkdocs serve [OPTIONS]
```

### Common Options for `mkdocs serve`

| Option                          | Type                 | Description                                                                                      | Default            |
|---------------------------------|----------------------|--------------------------------------------------------------------------------------------------|--------------------|
| `-a`, `--dev-addr`              | text                | IP address and port to serve documentation locally (default: `localhost:8000`).                  | None               |
| `--no-livereload`               | boolean             | Disable live reloading in the development server.                                                | False              |
| `--dirty`                       | boolean             | Only rebuild files that have changed.                                                            | False              |
| `-c`, `--clean`                 | boolean             | Build the site without effects of `mkdocs serve`; performs a pure build, then serves it.         | False              |
| `--watch-theme`                 | boolean             | Watch the theme for live reloading. Ignored if live reload is off.                               | False              |
| `-w`, `--watch`                 | path                | Additional directories or files to watch for live reloading (can be specified multiple times).   | `[]`               |
| `-f`, `--config-file`           | filename            | Specify a custom MkDocs config file (filename or `-` to read from stdin).                        | None               |
| `-s`, `--strict / --no-strict`  | boolean             | Enable strict mode, causing MkDocs to abort on warnings.                                         | None               |
| `-t`, `--theme`                 | choice (mkdocs \| readthedocs) | Specify the theme for building documentation.                                               | None               |
| `--use-directory-urls`          | boolean             | Use directory URLs when building pages (enabled by default).                                     | None               |
| `-q`, `--quiet`                 | boolean             | Suppress warnings.                                                                              | False              |
| `-v`, `--verbose`               | boolean             | Enable verbose output.                                                                           | False              |
| `--help`                        | boolean             | Display help information for `mkdocs serve`.                                                     | False              |

---

## How to Set Up GitHub Actions for Automated MkDocs Deployment

### Preparing Your MkDocs Project for GitHub Actions

To automate the deployment of your MkDocs project using GitHub Actions, you'll need to set up a specific directory structure and configuration files within your repository. Here's a step-by-step guide to get you started:

1. **Create the `.github` Directory:**
   - Navigate to the root of your MkDocs project and create a new folder named `.github`. This directory will house the GitHub Actions workflows and other GitHub-specific configurations.

2. **Add a `workflows` Directory:**
   - Inside the `.github` folder, create another folder named `workflows`. This is where all workflow configuration files will be stored.

3. **Create the CI Workflow File:**
    * Within the `workflows` folder, create a file named `ci.yml`. This YAML file will define the Continuous Integration (CI) workflow that GitHub Actions will execute.

### Example CI Workflow Configuration

Below is an example of a `ci.yml` file that sets up a CI workflow for deploying an MkDocs site. This configuration ensures that every push to the `master` or `main` branches triggers the deployment process.

```yaml
name: ci 
on:
  push:
    branches:
      - master 
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com
      - uses: actions/setup-python@v5
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV 
      - uses: actions/cache@v4
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs-material 
      - run: mkdocs gh-deploy --force
```

### Deployment Steps Explained

- **Checkout the Repository:** Initializes the repository content on the runner, allowing further actions to manipulate the project files.
- **Configure Git Credentials:** Sets up Git with credentials used by GitHub Actions, which allows it to commit back to your repository.
- **Setup Python Environment:** Prepares the Python environment with the specified version, ensuring compatibility with MkDocs.
- **Generate Cache ID:** Creates a unique identifier for caching dependencies, which speeds up subsequent workflow runs.
- **Cache Dependencies:** Caches Python dependencies to reduce build time.
- **Install MkDocs Material:** Installs the MkDocs Material theme and other required Python packages.
- **Deploy to GitHub Pages:** Builds and deploys your MkDocs site to GitHub Pages using a force push to overwrite existing content.

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
