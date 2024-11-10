---
layout: "layout"
title:  "Documentation"
hide:
  - navigation
  - toc
---

## Table of Contents

1. [How to Prepare the Source Code](#how-to-prepare-the-source-code) 

2. [How to Install Requirements for MkDocs](#how-to-install-requirements-for-mkdocs)

3. [How to Run MkDocs in a Web Browser](#how-to-run-mkdocs-in-a-web-browser)  
   3.1 [Common Options for `mkdocs serve`](#common-options-for-mkdocs-serve)  

4. [How to Set Up GitHub Actions for Automated MkDocs Deployment](#how-to-set-up-github-actions-for-automated-mkdocs-deployment)  
   4.1 [Preparing Your MkDocs Project for GitHub Actions](#preparing-your-mkdocs-project-for-github-actions)  
   4.2 [Example CI Workflow Configuration](#example-ci-workflow-configuration)  
   4.3 [Deployment Steps Explained](#deployment-steps-explained)  

5. [How to Change Header Color and Theme Using MkDocs Material](#how-to-change-header-color-and-theme-using-mkdocs-material)

6. [How to Add Weekly Assignments and Any Other Materials in General](#how-to-add-weekly-assignments-and-any-other-materials-in-general)  
   6.1 [Adding Weekly Assignments](#adding-weekly-assignments)  
   6.2 [Adding Other Materials](#adding-other-materials)  
   6.3 [Linking One Page to Another](#linking-one-page-to-another)

## How to Prepare the Source Code

1. **Download the Source Code:**  
   Click the link below to download the latest version of the source code as a ZIP file:  
   [Download Source Code](https://github.com/cbk2000/mkdocs-os-cbk/archive/refs/heads/master.zip)

2. **Extract the ZIP File:**  
   Once downloaded, unzip the `mkdocs-os-cbk-master.zip` file to access the source code files.

3. **Follow the steps below**

## How to Install Requirements for MkDocs

To set up MkDocs and the `mkdocs-material` theme, run the following commands in your CLI:

```bash
pip install mkdocs
pip install mkdocs-material
```

![Install Libraries](../assets/images/template/install_libraries.png)

## How to Set Up GitHub Actions for Automated MkDocs Deployment

### Preparing Your MkDocs Project for GitHub Actions

<span style="color:red; font-weight:bold; font-size:larger;">SKIP STEP 2-4 BECAUSE IT IS ALREADY GIVEN IN THE SOURCE CODE</span>

1. **Create Your GitHub Repository**  
   Start by creating a GitHub repository to host your MkDocs project if you haven’t already.  
   [Create New Repository on GitHub](https://github.com/new)

2. **Create the `.github` Directory:**
    - Navigate to the root of your MkDocs project and create a new folder named `.github`. This directory will house the GitHub Actions workflows and other GitHub-specific configurations.

3. **Add a `workflows` Directory:**
    - Inside the `.github` folder, create another folder named `workflows`. This is where all workflow configuration files will be stored.

4. **Create the CI Workflow File:**
    - Within the `workflows` folder, create a file named `ci.yml`. This YAML file will define the Continuous Integration (CI) workflow that GitHub Actions will execute.

5. **Configure the CI Workflow:**
    - Open the `ci.yml` file and add the necessary steps to install MkDocs, build the site, and deploy it to GitHub Pages. See Example CI Workflow Configuration below.
   [Example CI Workflow Configuration](#example-ci-workflow-configuration)

6. **Commit and Push Changes:**  
    - Once your CI workflow is configured, commit your changes and push them to GitHub.

7. **Set Up GitHub Pages Deployment:**  
    - Go to your repository’s settings, open the **Pages** section, and set the source to **Deploy from a branch**.  
     <img src="../assets/images/template/deployment_source.jpg" alt="Deployment Source" width="800"/>
    - Set the deployment branch to `gh-pages`.  
     <img src="../assets/images/template/deployment_branch.jpg" alt="Deployment Branch" width="800"/>
    - Save your changes.  
     <img src="../assets/images/template/deployment_save.jpg" alt="Save Deployment Settings" width="800"/>

8. **Access Your Deployed Site:**  
    - After the workflow completes successfully, refresh the GitHub Pages section and visit the GitHub Pages URL to access your MkDocs site.  
   <img src="../assets/images/template/deployment_link.jpg" alt="Deployment Link" width="800"/>

9. **Add the Deployed Site Link to Repository Details:**  
    - To make it easy for visitors to find your site, add the GitHub Pages URL to the repository details or the README file.  
     <img src="../assets/images/template/repository_about.jpg" alt="Repository About Section" width="800"/>
    - In the "About" section, click the gear icon to add the URL under "Website" and save your changes.  
     <img src="../assets/images/template/about_website.jpg" alt="About Website" width="800"/>
    - Save your changes.

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

### How to Change Header Color and Theme Using MkDocs Material

* **Open Your `mkdocs.yml` Configuration File:**
    - In your MkDocs project folder, locate and open the `mkdocs.yml` file.

* **Set the Color Palette:**
    - Under the `theme` section, add or modify the `palette` configuration to specify your desired primary and accent colors. For example:

```yaml
theme:
  name: 'material'
  palette:
    scheme: default
    primary: 'blue'
    accent: 'amber'
```


   - **Primary Color**: Sets the main color theme for your header and other primary elements.
   - **Accent Color**: Sets the accent color for links, buttons, and interactive elements.
   - Replace `'blue'` and `'amber'` with the colors that best suit your style. MkDocs Material supports a variety of colors, such as `'red'`, `'green'`, `'purple'`, `'indigo'`, `'teal'`, etc.

* **Available Color Schemes:**
    - MkDocs Material offers several built-in color schemes you can choose from. Each scheme changes the background, text contrast, and tone for the entire site, including the header and sidebar. Here’s a breakdown of each scheme:
   
     - **`default`**: The standard light scheme, with a white background and dark text. It provides a clean and bright look, ideal for general readability.
     - **`slate`**: A subtle, slightly darker scheme than `default`, featuring a muted background and softer contrast. This scheme is a great choice for a more subdued appearance while still remaining light.
     - **`dark`**: A full dark mode theme with a dark background and light text, suitable for users who prefer a low-light setting. This scheme is especially useful for nighttime reading.
     - **`black`**: The darkest scheme available, with a true black background and high-contrast light text. It’s designed to offer the most contrast and is perfect for OLED screens or users seeking maximum readability in dark mode.

4. **Preview Your Changes:**
      - Run the following command to preview the changes locally:

      ```bash
      mkdocs serve
      ```

      - This command starts a local development server where you can view the updated header color and palette changes.

5. **Deploy Your Site:**
    - Once you’re satisfied with the color scheme, deploy your MkDocs site to apply the changes to your live documentation.

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
  [Link Text](path/to/pageNameWithoutDotmd)
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
