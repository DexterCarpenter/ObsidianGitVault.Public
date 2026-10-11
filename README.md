# My Publicly Published Obsidian Repo

Public notes from my personal Obsidian Vault.

## How to Set Up For Yourself

This guide explains how to set up a GitHub Action that **automatically pushes a subfolder** (e.g., `PublicPublish/`) from your **private repository** to a **public repository**.

### Use Case
You're working on a private repository but want to expose just part of it (a subfolder) to the public — for example, for publishing open-source notes, templates, or demos.

### Overview of the Setup
1. **Private repo**: Contains everything, including the subfolder you want to share.
2. **Public repo**: Will contain only the contents of the target subfolder.
3. **GitHub Action**: Pushes changes from the private subfolder to the public repo on every push to `main`.

### Prerequisites
1. You own **both repositories** (or have write access to both).
2. You’ve created a **classic Personal Access Token (PAT)** on GitHub with:
	- `repo` scope
    - Access to the **public repository**
3. The public repo has **GitHub Actions disabled** (to avoid recursive runs or token conflicts).

### Step-by-Step Setup
#### 1. **Create a Personal Access Token (Classic)**
- Visit: [https://github.com/settings/tokens](https://github.com/settings/tokens)
- Click **"Generate new token (classic)"**
- Set scopes:
    - `repo` (for full access)
- Copy and store the token safely

#### 2. Add the Token as a Secret in Your Private Repo
Go to your private repo > **Settings > Secrets > Actions**, and add:

| Name          | Value                 |
| ------------- | --------------------- |
| GH_PUBLIC_PAT | *(your copied token)* |

#### 3. Add the GitHub Actions Workflow
In your private repository, create the file:
```
.github/workflows/sync-public-folder.yml
```
Paste this content:
```
name: Sync Public Folder to Public Repo

on:
  push:
    branches: [ main ]
  workflow_dispatch:  # allows manual triggering

jobs:
  sync-public:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout full repo
        uses: actions/checkout@v4
        with:
          fetch-depth: 0  # full history needed for subtree

      - name: Configure Git
        run: |
          git config --global user.name "GitHub Action"
          git config --global user.email "actions@github.com"

      - name: Split the PublicPublish folder
        run: |
          git subtree split --prefix=PublicPublish -b public-split

      - name: Push to public repo using PAT
        env:
          GH_TOKEN: ${{ secrets.GH_PUBLIC_PAT }}
        run: |
          git config -l | grep 'http\..*\.extraheader' | cut -d= -f1 | \
            xargs -L1 git config --unset-all
          git remote add public https://your-username:${GH_TOKEN}@github.com/your-username/your-repo.git
          git push public public-split:main --force
```

### Why the `extraheader` Fix Is Required
Without this line:
```
git config -l | grep 'http\..*\.extraheader' | cut -d= -f1 | xargs -L1 git config --unset-all
```
You may encounter this error:
```
Permission to <repo> denied to github-actions[bot]
```
This happens because GitHub automatically injects an `extraheader` for authentication, which **overrides your PAT**. You must remove it manually before pushing.
Source: [GitHub Actions Auth Error Fix](https://stackoverflow.com/questions/64270867/auth-error-trying-to-copy-a-repo-with-github-actions)

### Testing It
- Push to `main` in your private repo, or
- Go to the **Actions tab** and click **"Run workflow"** under your `sync-public-folder.yml` file
You should see the folder contents reflected in your public repository.

### Important Notes
- The **public repo must have GitHub Actions disabled** to avoid recursive sync loops or workflow security issues.
- This setup **forces** the push from private to public, overwriting the `main` branch of the public repo each time.

## Acknowledgements

Thanks to [Nathan Jesudason](https://github.com/NathanJesudason) for helping me tackle some bugs <3