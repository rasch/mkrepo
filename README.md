# mkrepo

Initialize a Git repository in the current working directory and
remotely on [Sourcehut], [Codeberg], [GitHub] and [GitLab] 🌱

## Usage

```txt
mkrepo <name> <description> [private]
```

- `<name>` (required) Name of the local and remote repository. It must
  contain only lowercase letters (a-z), numbers (0-9), and dashes (-)
  and can't begin with a dash.

- `<description>` (required) Description of the repository. The only
  requirement is that it can not be an empty string. Wrap the
  description in quotes to avoid escaping spaces and other special
  characters.

- `[private]` (optional) Set visibility of project to one of 'private'
  or 'public'. Projects are public by default.

## Examples

```sh
mkrepo dotfiles 'configuration files'
mkrepo personal-notes 'personal notebook and wiki' private
mkrepo mpvd '🎹 run mpv as a daemon with an API similar to mpc'
```

## Installation

```sh
# download script
curl -O https://git.sr.ht/~rasch/mkrepo/blob/main/mkrepo

# make it executable
chmod +x mkrepo

# move script to somewhere in "$PATH" such as:
mv mkrepo /usr/local/bin/
```

## Configuration

By default, a local repository is created and pushed only to Sourcehut.
To enable additional remotes, set the following environment variables.

- `GIT_USER` - set username for remote Git hosts. If not set, defaults to
  the output of the `whoami` command.

- `CODEBERG_USER`, `GITHUB_USER`, `GITLAB_USER`, `SOURCEHUT_USER` - set
  Codeberg, GitHub, GitLab and Sourcehut usernames to override
  `$GIT_USER` as needed.

- `CODEBERG_TOKEN`, `GITHUB_TOKEN`, `GITLAB_TOKEN` - set Codeberg,
  GitHub, and GitLab personal access tokens to enable additional
  remotes.

- `SOURCEHUT_DISABLE` - set to a non-empty string to disable Sourcehut

## Tips & Tricks

Instead of pushing to each remote individully it may be helpful to
create a git alias in the git configuration.

```sh
git config --global alias.pushall '!for r in $(git remote); do git push --all "$r"; done'
```

## What does `mkrepo` actually do?

- initialize git repository (`git init <reponame>`)
- change directory into repository (`cd <reponame>`)
- create README.md (`touch README.md` and `git add README.md`)
- initial commit (`git commit -m '🎉 Initial commit'`)
- add remotes for sourcehut, codeberg, github and gitlab (`git remote
  add <remote> <url>`)
- push to Sourcehut and set as upstream (Sourcehut supports creating new
  repositories on push)
- create repositories on Codeberg, GitHub and GitLab using their APIs
  and push the Initial commit

[sourcehut]: https://sr.ht
[codeberg]: https://codeberg.org
[github]: https://github.com
[gitlab]: https://gitlab.com
