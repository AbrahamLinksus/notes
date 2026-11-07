# Git basics

> Git is a distributed version control system: every developer has the full repo locally. Changes move from working directory → staging area → local repo → remote repo, while GitHub is just the cloud host for that remote.

studied: 2026-11-07 · status: done · source: Backend.pdf (pp. 7–8)

## Key ideas
- **Git:** a distributed version control system that helps developers track their codebase, collaborate with others and manage multiple versions of a project.
- **Decentralized:** every developer has a **full copy** of the repo on their machine.
- **Git vs GitHub:**
  - **Git** is the local software.
  - **GitHub** is a cloud-based hosting platform for storing and sharing Git repos.
- **Four areas:**
  - **Local machine:**
    - **working directory**: your code files
    - **staging area**: files about to be committed
    - **local repo**: the `.git` local files
  - **Remote:**
    - **remote repo**: the cloud copy
- **Core commands:**
  - `git init`: create a repo
  - `git add`: working directory → staging
  - `git commit`: staging → local repo
  - `git push`: local repo → remote
  - `git pull`: remote → your working copy
  - `git clone`: copy a remote repo to your machine

## Example
```
working dir ──git add──► staging ──git commit──► local repo ──git push──► remote
     ▲                                                                       │
     └──────────────────────────── git pull / git clone ─────────────────────┘
```
```bash
git clone https://github.com/user/app.git   # get full copy
# edit server.py
git add server.py                           # stage it
git commit -m "add health endpoint"         # save to local repo
git push                                    # share on GitHub
git pull                                    # get teammates' changes
```

## Pitfalls
- `git commit` doesn't put anything on GitHub. Until you `push`, the work is only on your machine.
- Unstaged edits aren't included in a commit. You have to `add` first.
- Saying "Git" when you mean "GitHub": the tool and the hosting service are different things.

## Related
- [CI/CD](ci-cd.md)
- [Database migrations](../databases/database-migrations.md)
