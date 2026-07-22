# 📚 LaTeX Book Writing & AI Collaboration Environment

This guide provides a comprehensive setup for writing LaTeX projects within VS Code, leveraging AI assistance (like VS Code Copilot/Gemini) for authoring, and compiling documents online using [latex.sanad.software](https://latex.sanad.software).

> [!WARNING]
> **Do not push or save directly to the `main` branch!**
> All editing and updates must be done on your own dedicated branch. Create your own branch first, commit your changes there, and submit a pull request/merge request. The `main` branch is reserved strictly for the complete, stable LaTeX project.

---

## 🛠️ Step-by-Step Workspace Setup

### Step 1: Initialize Workspace Directory

Create and open the master directory for the project. If you are already inside `book_sanad`, verify your path:

```bash
mkdir -p book_sanad
cd book_sanad
```

### Step 2: Clone the Book Repository (Repo 1)

Clone the repository containing the actual LaTeX book files:

```bash
git clone https://github.com/sanadChair/grad_book grad_book
```

### Step 3: Clone the Project Context Repository (Repo 2)

Clone the second repository (e.g., source code, assets, or database schemas). This helps the AI agent understand the project's background, code structures, and context when reference is needed.

```bash
git clone https://github.com/sanadChair/sanad_ws project_context
```

### Step 4: Account Setup on latex.sanad.software

1. Navigate to [latex.sanad.software](http://latex.sanad.software).
2. Click **Sign Up** to create your account.
3. Import your LaTeX book repository (`grad_book`) onto the platform.
4. **Configure Compiler**: Set the compiler/engine to **XeLaTeX** (or **LuaLaTeX**). 
   > [!IMPORTANT]
   > The project **must** be compiled using **XeLaTeX** or **LuaLaTeX**. Standard `pdfLaTeX` will fail because the template uses the `fontspec` package to load system fonts (e.g., `Times New Roman`).

---

## ⚙️ VS Code Configuration

To enable autocompletion, spelling, grammar checking, and smooth AI-assisted editing, configure VS Code as follows:

### Recommended Extensions

Install the following extensions through the VS Code Extensions Marketplace (`Ctrl+P` / `Cmd+P` -> paste `ext install <id>`):

| Extension               | Purpose                                                           | Install Command                       |
| :---------------------- | :---------------------------------------------------------------- | :------------------------------------ |
| **LaTeX Workshop**      | Syntax highlights, autocomplete, snippet shortcuts                | `ext install James-Yu.latex-workshop` |
| **LTeX (LanguageTool)** | Grammar and spell checking inside LaTeX docs                      | `ext install valentjn.vscode-ltex`    |
| **GitHub Copilot**      | AI-assisted prose drafting, table generation, and math formatting | `ext install github.copilot`          |

### Workspace Settings Configuration

Add the following JSON properties to your `.vscode/settings.json` to optimize editing without attempting local compiles:

```json
{
  "latex-workshop.latex.autoBuild.run": "never",
  "latex-workshop.view.pdf.viewer": "tab",
  "ltex.language": "en-US",
  "editor.wordWrap": "on",
  "[latex]": {
    "editor.wordWrap": "on",
    "editor.quickSuggestions": {
      "other": true,
      "comments": false,
      "strings": true
    }
  }
}
```

> [!NOTE]
> Setting `"latex-workshop.latex.autoBuild.run": "never"` prevents VS Code from throwing build errors locally since the compilation will be handled on the web interface.

---

## 🤖 AI-Driven LaTeX Workflow

### 📁 Project Structure & Figures Guide

This is a modular collaborative LaTeX template. The repository is organized as follows:

```text
grad_book/
├── README.md
├── main.tex                       # Master style & include index
├── shared_figures/                # Shared figures across multiple chapters
│   └── .gitkeep
├── frontmatter/                   # Frontmatter sections (Acknowledgment, Abstract)
│   ├── acknowledgment.tex
│   └── abstract.tex
└── chapters/
    ├── chapter_01/                # Generic Chapter 1 folder
    │   ├── chapter_01.tex         # Chapter content
    │   └── figures/               # Figures specific to Chapter 1
    │       └── .gitkeep
    ...
    └── chapter_12/
        ├── chapter_12.tex
        └── figures/
            └── .gitkeep
```

#### 🖼️ Adding and Referencing Figures

To avoid conflicts during collaboration, follow these image guidelines:

1. **Chapter-Specific Figures**:
   - Save figures in the chapter's own `figures/` directory, e.g., `chapters/chapter_01/figures/`.
   - Reference the figure in the LaTeX file using its relative path from the root:
     ```latex
     \includegraphics[width=0.8\textwidth]{chapters/chapter_01/figures/my_diagram.png}
     ```
2. **Shared Figures**:
   - Save figures used in multiple chapters in `shared_figures/`.
   - Reference them using:
     ```latex
     \includegraphics[width=0.8\textwidth]{shared_figures/common_chart.png}
     ```

---

### Step 5: Edit in VS Code and Compile Online

#### 1. Editing with AI Assistance

Use VS Code Copilot or any AI chat assistant in VS Code. Since you have cloned the project repository alongside the book repository, the AI can read definitions and context from the project files.

**Example Prompts for your AI Agent:**

- _Drafting prose:_
  > "Draft an introductory paragraph for Chapter 2 explaining the system architecture using the files in `./project_context` as reference."
- _Generating LaTeX Tables:_
  > "Convert the configuration parameters from `./project_context/config.json` into a neat LaTeX table with centering and labels."
- _Math formatting:_
  > "Format the following equation in LaTeX math block and add a brief description of the variables: [equation description]"

#### 2. Compiling and Previewing

copy-paste updated text blocks directly into the editor on [latex.sanad.software](http://latex.sanad.software) to run a quick compilation and verify rendering.
