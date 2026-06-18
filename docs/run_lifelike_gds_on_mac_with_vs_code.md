# Set Up and Run `lifelike-gds` on a Mac

This guide is for someone starting with a new Mac that does not already have development tools installed.

We will install:

* Homebrew
* Git
* uv
* just
* Python 3.11
* JupyterLab

Then we will download the `lifelike-gds` project from GitHub and run notebooks locally.

## 1. Open Terminal

Open the **Terminal** app.

You can find it by pressing:

```text
Command + Space
```

Then type:

```text
Terminal
```

Press **Enter**.

## 2. Install Homebrew

Homebrew is a tool that helps install developer software on a Mac.

First, check whether Homebrew is already installed:

```bash
brew --version
```

If you see a version number, Homebrew is already installed.

If you see an error like `command not found: brew`, install Homebrew with this command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

During installation, it may ask for your Mac password. Type your password and press **Enter**.

After Homebrew finishes installing, follow any instructions printed in the Terminal.

Then check again:

```bash
brew --version
```

## 3. Install Git, uv, and just

Install the tools needed for this project:

```bash
brew install git uv just
```

Check that they installed correctly:

```bash
git --version
uv --version
just --version
```

## 4. Install Python 3.11 with uv

This project uses Python 3.11.

Run:

```bash
uv python install 3.11
```

Check Python:

```bash
uv python list
```

## 5. Choose a Folder for the Project

For example, create a `projects` folder in your home directory:

```bash
mkdir -p ~/projects
cd ~/projects
```

## 6. Download the Code from GitHub

Use Git to clone the project with HTTPS:

```bash
git clone https://github.com/cair2015/lifelike-gds.git
```

Go into the project folder:

```bash
cd lifelike-gds
```

You should now be inside the project folder.

Check the files:

```bash
ls
```

You should see files such as:

```text
README.md
pyproject.toml
uv.lock
justfile
src
examples
tests
```

## 7. Set Up the Python Project

Run:

```bash
just setup
```

This will create a local Python environment and install the packages needed by the project.

If `just setup` does not work, run the equivalent command directly:

```bash
uv sync
```

## 8. Check That the Project Works

Run the project tests:

```bash
just test
```

If that does not work, run:

```bash
uv run pytest
```

Some tests may require extra setup, such as a local database. If a test mentions Neo4j or connection settings, that part may need additional configuration.

## 9. Install JupyterLab in the Project Environment

Run this command from inside the `lifelike-gds` folder:

```bash
uv pip install jupyterlab
```

Then register the project environment as a Jupyter kernel:

```bash
uv run python -m ipykernel install --user --name lifelike-gds --display-name "Python (lifelike-gds)"
```

## 10. Start JupyterLab

Run:

```bash
uv run jupyter lab
```

This should open JupyterLab in your browser.

If it does not open automatically, Terminal will show a local URL that starts with something like:

```text
http://localhost:8888/lab
```

Copy that URL and paste it into your browser.

## 11. Open a Notebook

In JupyterLab, open a notebook file if the project has one.

If you create a new notebook, choose this kernel:

```text
Python (lifelike-gds)
```

This tells Jupyter to use the Python environment for this project.

## 12. Run Example Python Scripts

The project also has example Python scripts in the `examples` folder.

To see them:

```bash
ls examples
```

To run one example, use:

```bash
uv run python examples/shortest_path_example.py
```

Or replace the filename with another file from the `examples` folder.

## 13. Later: Get the Latest Code Updates

If the project code changes on GitHub, go into the project folder:

```bash
cd ~/projects/lifelike-gds
```

Then pull the latest changes:

```bash
git pull
```

After pulling changes, update the Python environment:

```bash
just setup
```

Or:

```bash
uv sync
```

## Common Problems

### Problem: `brew: command not found`

Homebrew is not installed or was not added to your shell path.

Reopen Terminal and try:

```bash
brew --version
```

If it still does not work, look at the instructions printed at the end of the Homebrew installation and run the suggested commands.

### Problem: `git: command not found`

Install Git:

```bash
brew install git
```

### Problem: `uv: command not found`

Install uv:

```bash
brew install uv
```

### Problem: `just: command not found`

Install just:

```bash
brew install just
```

### Problem: Jupyter opens but the project package cannot be imported

Make sure you started Jupyter from inside the project folder:

```bash
cd ~/projects/lifelike-gds
uv run jupyter lab
```

Also make sure the notebook is using this kernel:

```text
Python (lifelike-gds)
```

### Problem: Code asks for Neo4j or database settings

Some parts of this project are for Neo4j-backed graph workflows. If the code needs Neo4j, you may need database connection information such as:

```text
NEO4J_URI
NEO4J_USERNAME
NEO4J_PASSWORD
```

Do not share passwords in GitHub or commit them to the project.
