## Setup & Configuration

Git config levels: **System** (`/etc/gitconfig`), **Global** (`~/.gitconfig`), **Local** (`.git/config`). Each level overrides the previous.

### View Settings
Show all settings and where they come from:
```bash
$ git config --list --show-origin

```

### Identity (Required)

Baked into every commit. Use `--global` for system-wide default, or omit for repo-specific.

```bash
$ git config --global user.name "John Doe"$ git config --global user.email johndoe@example.com

```

### Editor

Set default editor for messages (e.g., Emacs, Vim, VS Code).

```bash
$ git config --global core.editor emacs

```

**Windows (Notepad++)**:

```bash
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

```

## Repository Basics

### Initialize

Create the `.git` skeleton. No files are tracked yet.

```bash
$ git init

```

### Track & Commit

**Stage** specific files or wildcards:

```bash
$git add *.c$ git add LICENSE

```

**Stage** all changes (new, modified, deleted) in current directory:

```bash
$ git add .

```

**Commit** staged changes:

```bash
$ git commit -m 'Initial project version'

```

**Skip staging** (track modified files automatically, skips new files):

```bash
$ git commit -a -m 'Quick update'

```

### File Status

See what is tracked, modified, or untracked.

```bash
$ git status

```

### Ignore Files (.gitignore)

Create a `.gitignore` in the root to exclude **untracked** files at the **Working Tree** level.

**Note**: Ignored patterns do NOT affect files already in the **Index** (tracked).

```text
# .gitignore example
*.[oa]      # ignore .o and .a
*~          # ignore temp files
log/        # ignore log dir
!lib.a      # do NOT ignore lib.a
/TODO       # ignore TODO only in root

```

## File Management

### The Three Areas

1. **Working tree**: Current files.
2. **Index (Staging)**: Next commit.
3. **History**: Committed snapshots.

![alt text](../areas.png)

### Remove Files

**Remove** from Git and delete from disk:

```bash
$ git rm PROJECTS.md

```

**Untrack only** (keep file on disk):

```bash
$ git rm --cached README

```

### Move/Rename

Git detects renames, but `git mv` updates the index immediately.

```bash
$ git mv README.md README

```

## History & Fixes

### View History

**List commits** (reverse chronological):

```bash
$ git log

```

**Last N commits** with diffs (`-p`):

```bash
$ git log -p -2

```

### Amend Last Commit

Add forgotten files or fix message of the **most recent** local commit.
⚠️ **Do not use on pushed commits.**

```bash
$git add forgotten_file$ git commit --amend -m "Updated message"

```

### Undo Changes

**Unstage** a file (keep changes in working tree):

```bash
$ git restore --staged CONTRIBUTING.md

```

**Discard** changes (revert to last commit):
⚠️ Permanent data loss.

```bash
$ git restore CONTRIBUTING.md

```

## Remotes

### Manage Remotes

**List** remotes with URLs:

```bash
$ git remote -v

```

**Add** a remote:

```bash
$ git remote add origin [https://github.com/user/repo.git](https://github.com/user/repo.git)

```

**Inspect** specific remote details:

```bash
$ git remote show origin

```

**Rename/Remove** (local config only):

```bash
$ git remote rename origin upstream
$ git remote remove upstream

```

### Syncing

**Fetch** (download updates, do not merge):

```bash
$ git fetch origin

```

**Pull** (fetch + merge/rebase current branch):

```bash
$ git pull

```

**Push** current branch:

```bash
$ git push

```

**Push** specific branch (and set upstream with `-u`):

```bash
$ git push -u origin feature/login

```

## Tagging

### List Tags

```bash
$ git tag
$ git tag -l "v1.*"

```

### Create Tags

**Annotated** (recommended for releases):

```bash
$ git tag -a v1.0.0 -m "Release v1.0.0"

```

**Lightweight** (temporary/quick):

```bash
$ git tag v1.0.0-hotfix

```

**Tag past commit**:

```bash
$ git tag -a v1.2.0 9fceb02 -m "Release v1.2.0"

```

### Share Tags

**Push specific**:

```bash
$ git push origin v1.0.0

```

**Push all**:

```bash
$ git push origin --tags

```

### Delete Tags

**Local**:

```bash
$ git tag -d v1.0.0

```

**Remote**:

```bash
$ git push origin --delete v1.0.0

```
