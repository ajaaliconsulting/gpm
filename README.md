# Git Project Manager (GPM)

GPM is a textual project management software for software projects. It links directly to git and also uses git for its state.

GPM can be used in 2 modes:
1. Space, this is where you create a gpm space in its own repo. This is most useful as a project management tool that spans across git repos, feature and teams.
2. Project, this is where you create a gpm project inside your project's git repository. This is useful for issue and bug tacking of a single repostory. In this mode you can raise pull requests that amend change your code and close issues at the same time.

## Features
1. Easily create issues from your git repository and have them link directly to your project.
1. Configure your project structure, issue templates, and kanban boards from your text editor in markup.
1. Plan your project using any project management style or create your own.
1. Have 4 eyes control on new issues and approve them through pull requests.

# Installation

You can install GPM with cargo:

```shell
cargo install gpm
```
# Getting Started (Space mode)
GPM uses git for manage the application state, so to start using gpm you will need to have `git` installed and on your path.

To create a new gpm space run
```shell
git clone http://myproject-domain/my_gpm_project.git
cd my_gpm_project
gpm init space
```

This will create default `gpm.yaml` file in your project and default issue type templates in the `templates` folder.

```yaml
space:
    name: myspace
    types:
        - feature
        - issue
        - bug
    status:
        - backlog
        - inprogress
        - closed

```

You can then create a new project under your space
```shell
gpm project add supersoft --git http://myproject-domain/supersoft.git
```

Your new project is now available under `projects/supersoft` and has its own `project.yaml` and templates folder for you to customise further.

To add a new issue to your project just call

```shell
gpm project supersoft add feature "Cryptometer"
```
This will add a feature to the supersoft project and open a text editor with the feature template for you to fill in.

## Using gpm space from other git repositories.

When you created the gpm space, gpm added the space folder on your drive to its list of spaces. You can then use gpm from any
other git repository.  If the git repository is already added as a project to your space then you can add issues by simply calling
```shell
gpm add issue --link feature="cryptometer"
```

You can also list all issues for your repository with the `list` command
```shell
gpm list bug

412dsre Wrong mime type ... src/mimetypes.rs 200
e3451xw Template picture size ... src/templates/picture.html 10
```

# Getting Started (Project mode)
GPM project mode allows you to create a gpm project from within your repo. This unlocks the ability to raise PRs on your repository and change your project state in one go. An example of this is closing a bug with a PR. 

The downside is that your project state is in lock step with your repository, therefore you might want to exclude the `.gpm` folder inside your repository from your CI processes to ignore pure project changes.

To create a gpm project from within your code repository run
```shell
gpm init project
```

This will create a `.gpm` folder in your code repo where your project configuration and templates are defined.


# Commands

Initialise a new gpm space with:
`gpm init`


