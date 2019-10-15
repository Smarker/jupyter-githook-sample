# Jupyter Notebook Pre-Commit Git Hook Sample

Data science projects often start with using jupyter notebooks for exploration.
When sharing results with others, it helps to have the python code separate
from generated plots and plots separated from the code when sharing
visualizations to others. Using a `pre-commit` githook to capture plots and
code separately allows data science projects to be more organized and more
easily be transitioned from exploration to production.

[Git Hooks](https://git-scm.com/docs/githooks) are scripts you can put in a
hooks directory. In this case, we decided to use `.githooks` as our hooks
directory. The hooks will trigger actions at certain points in git’s execution.

For example, the [pre-commit](https://git-scm.com/docs/githooks#_pre_commit),
is invoked before obtaining the proposed commit log message and making a commit.

## Setup Requirements

* Git version `>=2.9` installed on your system.
* Filenames **must not contain spaces**.
* `notebooks`, `scripts`, and `html` folders must exist at the root of your
project.

## Setup

To configure the `pre-commit` hook for your project, run:

```sh
make
```

This will run:

```sh
git config core.hooksPath .githooks
```

What this will do will set up the git hooks directory to point to a directory
called `.githooks`.
