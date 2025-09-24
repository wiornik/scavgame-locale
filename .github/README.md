
# Contributing to the `fr-FR` locale (for non-developers)
Welcome — this repo/fork holds the French (France) localization for the game. This README explains, step-by-step and in plain language, how a non-developer contributor can set up their computer, edit translations safely, and push changes so they are validated and merged.


## Table of contents
1. [Who this is for](#who-this-is-for)
2. [What you'll need (prerequisites)](#what-youll-need-prerequisites)
3. [Install & configure](#install--configure-quick-step-by-step)
4. [Make edits to `FR.json`](#make-edits-to-frjson)
5. [Committing & pushing changes](#committing--pushing-changes)
6. [What happens after your change is merged](#what-happens-after-your-change-is-merged)
7. [Pushing progress to the parent repository](#pushing-progress-to-the-parent-repository)
8. [Translation rules & common gotchas](#translation-rules--common-gotchas)
9. [Troubleshooting / FAQ](#troubleshooting--faq)
10. [Contacts / help](#contacts--help)

## Who this is for

This guide is written for **non-developers** (translators, QA, community contributors) who want to update the French (`fr-FR`) translations safely — without needing deep programming knowledge. If you know your ways around programming but want to be sure of what is expected as a contributor, you might also want to consider those recommendations.

## What you'll need (prerequisites)

- A GitHub account (create one at github.com if you don't have one).
- A computer running Windows, macOS, or Linux.
- Basic comfort editing text files (we'll use Visual Studio Code — friendly GUI).

Software recommended and that we'll guide you through installing:

- **Git** — for version control (we show commands, but VS Code hides most complexity).
- **Visual Studio Code (VS Code)** — editor.
- VS Code extensions:
    - **Git Graph**
    - **Code Spell Checker**
    - **French - Code Spell Checker** (language pack / French dictionary)

(We will show how to install each below.)

## Install & configure

### 1) Install Git

- Windows: install Git for Windows from the official site (use default options).
- macOS: `brew install git` if you use Homebrew, or install from the official package.
- Linux: use your package manager, e.g. `sudo apt install git`.

After install, configure your name/email (only once):

```bash
git config --global user.name "Your Full Name"
git config --global user.email "you@example.com"
```

### 2) Create / sign in to your GitHub account

- Go to github.com and register / sign in.

### 3) Install Visual Studio Code

- Download & install from code.visualstudio.com and open it.

### 4) Install the recommended VS Code extensions

In VS Code:

- Open the **Extensions** panel (left sidebar or `Ctrl/Cmd+Shift+X`) and search/install:
    - [`Git Graph`](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)
    - [`Code Spell Checker`](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
    - [`French - Code Spell Checker`](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker-french) (or the French language pack for the Code Spell Checker — look for "French" in its language packs)

The recommended configuration for the extensions is located inside this repo, so don't bother configuring them.
### 5) (Optional but recommended) Set up SSH keys on GitHub

This avoids repeatedly typing your password when pushing. Follow GitHub's [SSH key instructions](https://docs.github.com/fr/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) in your GitHub account settings. If SSH feels complex, you can use HTTPS clones and VS Code will prompt for credentials when needed.

## Clone the repository

There are two common contributor setups. Follow the one that applies to you.

If you want to be added as a team member you might as well query that on the [dedicated thread](https://discord.com/channels/955738554129063947/1419424554769449070) on the Ostroniks community translation discord section.
### A — You **do** have write access to this fork (team member)

1. Clone this fork directly:

```bash
git clone https://github.com/<this-fork-owner>/<repo-name>.git
cd <repo-name>
```

> If you prefer SSH use the SSH URLs instead of `https://`.
### B — You **do not** have write access to this fork (most contributors)

1. On GitHub, **fork** this repository into your own account (button `Fork` at top-right of the repo page).
2. Clone _your fork_ to your computer:

```bash
# replace <your-username> and <repo-name>
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

3. Add the original repo (this fork) as `upstream` so you can sync later (optional but useful):

```bash
git remote add upstream https://github.com/Orsoniks/scavgame-locale
git fetch upstream
```

> If you prefer SSH use the SSH URLs instead of `https://`.

## Make edits to `FR.json`

The translations live in the root file named `FR.json`. Do not modify `EN.json` or other language files, you are allowed to modify the root file named `README.md` to add due credits.
### 1) Open the project in VS Code

`File → Open Folder` → select the cloned repo folder.
### 2) Open the `FR.json` file

- Use VS Code explorer to find and open the file.
### 3) Use the tools

- **Spell check**: the Code Spell Checker will underline typos. Make corrections; it has a suggestions menu.
- **Git Graph** extension helps visualize commits & pushes with a GUI if you prefer not to use terminal git commands.
### 4) What to edit in `FR.json`

- Only replace the **English text** (the values) with the proper French translation.
- **Do not** change the JSON keys (the left-hand strings). Example:

```json
{
	"drybush": "Buisson", // OK — translated value
	"drybushdsc": "Votre intuition vous dit qu’il est mort.", // OK
}
```

- Keep placeholders intact: if the English text contains `<>`, `<1>`, `<color=\"grey\">`, `<limb>` or similar — **keep them exactly** and translate around them, e.g.:
    - `"J’ai mal au <limb>..."`
    - `"dirty1dsc": "Envisagez de prendre une petite douche. (<> %)"`.
- Keep punctuation consistent and use proper French typography where appropriate (e.g., NBSP before `:`, NNBSP before `!`, `?`, and use the correct apostrophe `’` and not `'`).

## Committing & pushing changes
We recommend pushing your work as frequently as you can to avoid changes staying on your side while another person is redoing the work. You can either work on the `main` branch or create your own, as we're not that many as of now.
### In VS Code (GUI, recommended for non-devs)

1. Open Source Control (left icon) → Click the `+` beside changed files to stage.
2. In the Commit message box write a short message like: `fr: fix typos in FR.json` or `fr: translate menu strings`, a message is always needed and everyone will see it.
3. Click the checkmark (Commit).
4. Click `...` → `Push` (if VS Code asks which branch, choose "Create new branch" and give it a short name like `translate/fix-typos`).
### In terminal (commands)

From the repo folder:

```bash
# create branch (recommended)
git checkout -b translate/fix-typos

# stage and commit
git add FR.json
git commit -m "fr: translate/typo fix in FR.json"

# push to your fork (origin) - first push sets branch name on remote
git push -u origin translate/fix-typos
```

### Create a Pull Request (PR)

- After pushing, GitHub shows a banner: click **Compare & pull request**.
- Title the PR clearly (e.g., `fr: translate shop strings`) and write a short description: what you changed and why.
- Select the **base** branch: `main` (the main branch of this fork).
- Submit the PR.

If you have direct write access you can push branches to this repo and create a PR in the same way. Or avoid it totally by committing on the main branch

## What happens after your change is merged

- **Automatic validation**: once code is merged into the fork's **main** branch, a GitHub Actions workflow runs automatically.
	This workflow checks:
    - That `FR.json` is valid JSON (no syntax errors).
    - That the keys in `FR.json` match the original `EN.json` (no keys removed or renamed).
    - That formatting is correct (Prettier / agreed formatting).

- If the workflow finds a problem, the PR or commit will show a failing status. Check the workflow logs in the GitHub Actions tab for details and fix the issues in a new commit on the same branch (or a new branch & PR if you prefer).

## Pushing progress to the parent repository

Once a month, the day preceding the month switch, an automated process is tasked to bring the modifications to the official [parent repo](https://github.com/Orsoniks/scavgame-locale).

Should this operation fail, a maintainer of the repo will be tasked to PR the changes.

## Translation rules & common gotchas

- **Never change keys** in the JSON (the left-hand identifiers). Only change values.
- **Preserve placeholders** exactly: `<>`, `<1>`, `<color=\"grey\">`, `<limb>` etc.
- **Keep sentence meaning**: do not invent or remove context.
- **Avoid trailing commas**: JSON must be valid.
- **Spacing / punctuation**: apply normal French rules but be consistent with the project style.
- **Short strings caution**: game UI may truncate very long text. Prefer translations with the approximate same amount of characters where possible, particularly with UI text.
- *Don't try to 'improve' the game, just make it French.*

## Troubleshooting / FAQ

**Q: The CI/checks failed — what do I do?**
A: Open the GitHub Actions logs (link in the failing checks). The logs usually say exactly which key is missing or what formatting is wrong. Fix locally, commit, and push again to the same branch — the workflow will run again.

**Q: Spell checker flags words that are correct (onomatopoeia, neologism)**
A: You can add project-specific terms to the workspace dictionary (Code Spell Checker supports adding words). Ask maintainers for a shared word list if many contributors add the same terms.

**Q: I accidentally edited `EN.json` or removed a key**
A: Revert the change locally by discarding that file and restore the proper version from `main` before committing. If it's already pushed, add a commit that restores the file or discuss with maintainers.

## Contacts / help

If you get stuck:

- Open an issue in this repository describing the problem (include screenshots or the error text).
- Or contact any repo maintainer be it on GitHub or in the the [dedicated thread](https://discord.com/channels/955738554129063947/1419424554769449070) on the Ostroniks community translation discord section

---

Thanks for helping translate! Your contributions make the game more accessible for French players. If something in this guide is unclear or you want a one-on-one walkthrough, open an issue and a maintainer will help — we love pairing with new contributors.

Happy translating! 🎉
[Azurian](https://github.com/clemtomera)