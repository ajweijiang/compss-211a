# Team project: collaborate in one repository

Continue here after [Git and GitHub basics](1_github_basics.md). Keep the
[glossary](3_git_github_glossary.md) handy for unfamiliar terms.

Work through **sections 1–4 in class**: set up the team repository, review each
other's PRs, and resolve a deliberate conflict. Complete **sections 5–7 before
Friday's lab**. SSH and website publishing are optional reference for later.

## 1. Create one shared repository and clone it

Use an existing team repository if you already have one. Otherwise:

1. **One teammate** opens the [project template](https://github.com/macss-berkeley/compss-211a-project-template)
   and chooses **Use this template → Create a new repository**.
2. Choose that teammate as owner, use a team-specific name such as
   `team-2-project`, and select **Public**. Leave **Include all branches** off.
   Create it and share its URL. [Example creation form](../../img/team-template-form.png).
3. The owner opens the repository's **Settings → Collaborators → Add people**
   and invites each teammate by exact GitHub username. Everyone accepts the
   invitation. [Example invitation dialog](../../img/github-add-people.png);
   its repository name will differ from yours.
4. Everyone opens **File → Clone Repository** in Desktop, selects the shared
   repository under **GitHub.com**, and clones it to a local folder. If it is
   missing, check the invitation and signed-in account, or use its URL.
5. Open the cloned folder in VS Code. Check that everyone has the **same remote
   URL**, with a separate local copy on each computer.

A template creates a new project from starter files. **Clone** brings an
existing remote repository to your computer. Each teammate clones the team's
repository. The owner has invited everyone to work in this repository, so
teammates can publish branches directly to it. No separate forks are needed.

The template has a README and places for data, notebooks, and scripts. Today,
we only need to edit Markdown; environment setup comes in the
[follow-up below](#5-set-up-the-shared-python-environment).

## 2. Review and merge a teammate's pull request

Each person proposes one planning note. A teammate reads it and responds.
**Review** means inspecting and discussing the proposal; **merge** means
accepting its changes into `main`.

1. **Author: create a branch.** In Desktop, select the team's repository and
   `main`, fetch, and pull. Create `plan-USERNAME` from `main`, replacing
   `USERNAME` with your GitHub username.
2. **Author: write a note.** At the top level, create `plan-USERNAME.md`:

   ```markdown
   # Project plan

   Question: What might we investigate?
   Possible source: Where might the data come from?
   Next step: What should we check first?
   ```

   Replace the prompts with your ideas. A tentative proposal is fine. Using
   your own filename keeps this first contribution from overlapping others'
   edits. Save, inspect the diff, commit, and **Publish branch**.
3. **Author: open a PR on GitHub.** Use **base: `main`** and **compare:
   `plan-USERNAME`**. Both branches belong to the team's repository. Give the
   PR a descriptive title, explain your proposal, and share its link with a
   teammate who will review it.
4. **Reviewer: read the proposed change.** Open **Files changed**. Is the
   question understandable? Is the suggested next step feasible? Did only
   the intended file change? Leave feedback under **Conversation**: suggest
   a specific improvement, or explain why the proposal is ready to merge.
5. **Author: respond.** Reply to the feedback. If a revision is needed, edit
   on the same `plan-USERNAME` branch, save, commit, and push. The existing PR
   updates; ask your reviewer to read the new version.
6. **Reviewer: merge when ready.** Read the final diff, then select **Merge
   pull request** and confirm. You can merge because the repository owner
   invited you as a collaborator. Merely making a repository public would
   not give you that permission. If GitHub reports a conflict, resolve it
   before merging; we practise that next.
7. **Everyone: update your local copy.** In Desktop, switch to `main`, fetch,
   and pull. Open a teammate's planning note locally and find its merged PR
   on GitHub. Swap author/reviewer roles so each person reviews a contribution.

**Checkpoint:** Did publishing the branch put the note on `main`? Did merging
its PR automatically update everybody's laptop?

## 3. Resolve a conflict between two pull requests

The earlier stash exercise combined two edits to the same sentence. Now we
will create that problem with **two teammates' committed branches**. Work in
the shared team repository and use a small practice file.

1. **Prepare a shared starting point.** One teammate adds `team-next-step.md`
   through a branch and reviewed PR, using the workflow above. Give the file
   exactly this line, and merge that setup PR:

   ```text
   Next step: choose a data source.
   ```

2. **Both teammates start together.** With no uncommitted edits, each switches
   to `main`, fetches, and pulls. Confirm both copies show the sentence above.
   Person A creates `check-license`; person B creates `compare-sources`.
   **Create both branches before merging either person's changes.**
3. **Make two different edits.** Replace the original line as follows:

   | Person | Branch | New line in `team-next-step.md` |
   | --- | --- | --- |
   | A | `check-license` | `Next step: check the data license.` |
   | B | `compare-sources` | `Next step: compare two data sources.` |

   Both save, commit, publish their branch, and open a PR into the team's
   `main`. Keep both PRs open until both are ready.
4. **Merge the first proposal.** B reviews and merges A's `check-license` PR.
   Now open B's `compare-sources` PR. GitHub should report a conflict: `main`
   has changed the same original line differently. Read both versions and
   agree on the sentence you want the team to use.
5. **B resolves the conflict in the browser.** On B's PR, choose **Resolve
   conflicts**. Replace the conflict block, including the `<<<<<<<`, `=======`,
   and `>>>>>>>` marker lines, with:

   ```text
   Next step: compare two data sources and check their licenses.
   ```

   Select **Mark as resolved**, then **Commit merge**. This updates
   `compare-sources` with the resolution; it has **not yet merged B's PR into
   `main`**. [GitHub's conflict-resolution guide](https://docs.github.com/en/pull-requests/how-tos/merge-and-close-pull-requests/resolving-a-merge-conflict-on-github).
6. **A reviews and merges the resolved PR.** Read **Files changed** again.
   Check that the final sentence preserves both intentions, then select
   **Merge pull request** and confirm.
7. **Everyone pulls the result.** In Desktop, switch to `main`, fetch, and
   pull. Check that `team-next-step.md` contains the same agreed sentence on
   each computer and on GitHub. Finished branches can be deleted after merging.

**Checkpoint:** Why did the second PR develop a conflict only after the first
was merged? How is **Commit merge** during conflict resolution different from
**Merge pull request** afterwards?

If no conflict appears, check that both branches started from the same original
sentence and that both people replaced that line in the same file. A conflict
can also happen when one person works on two branches; it is the competing
edits, rather than the number of people, that cause it.

## 4. Carry these habits into the project

- Start each task from updated `main` and create a new, task-specific branch.
  Keep changes small enough for someone else to review.
- Agree on **one active editor per notebook**. Notebook files also contain
  outputs and metadata, which can make their diffs and conflicts difficult.
  Commit, push, complete review/merge, and tell the next editor where to
  continue. They pull the shared version before starting.
- Check which files you are committing. Small shareable examples can support
  reproducibility; passwords, API keys, and `.env` files stay outside Git.
  Follow the source's rules for private or restricted data.
- `.gitignore` excludes matching **untracked** files. It does not untrack files
  already committed or erase old history. The template's ignore rules help
  keep environments and generated files out; still inspect the Changes list.

**Before you leave:** show your branch commit, a PR you reviewed, and a
teammate's merged note on your computer. Agree on the team's next real task.
For that task, use a new branch to improve the README, investigate a source,
or start the code.

## 5. Set up the shared Python environment

Work in the team's repository created from the
[project template](https://github.com/macss-berkeley/compss-211a-project-template).
The main files you will use are:

| File or folder | Purpose |
| --- | --- |
| `README.md` | Question, team, instructions, and eventual findings. |
| `notebooks/` | Exploration, analysis, and explanations alongside code. |
| `scripts/` | Tasks that should run consistently from beginning to end. |
| `data/` | Permitted small files or instructions for obtaining data. |
| `pyproject.toml` | Supported Python version and project dependencies. |
| `uv.lock` | Exact dependency versions for the shared environment. |

Every teammate should open the **whole cloned repository folder** in VS Code,
then open a terminal in that folder and run:

```bash
uv sync --frozen
```

Select the repository's `.venv` as the Python interpreter and notebook kernel.
Confirm everyone can use this environment before beginning the analysis.

## 6. Choose a notebook or script

Start in a **notebook** when exploring data, trying a method, inspecting output,
or explaining an analysis step by step. Use a **script** when a task is
understood and should run the same way repeatedly, such as downloading data
or recreating final figures.

Discuss where each task belongs:

1. Inspect ten documents and write observations beside the output.
2. Download the same bounded set of API records again.
3. Compare two cleaning rules.
4. Rebuild the final analysis file from raw data.
5. Explain a result using prose, a table, and a plot.

Try a small script on a new branch. Add `scripts/check_setup.py`:

```python
import sys
print("Python:", sys.version.split()[0])
```

Run it from the repository folder:

```bash
uv run python scripts/check_setup.py
```

Then run the equivalent code in a notebook cell. The Python is the same;
the script runs from beginning to end, while the notebook supports inspecting
and discussing individual steps. Review the contribution through a PR.

## 7. Agree on the next project work

Use the planning notes from class to agree on a tentative question, candidate
source, and next responsibility. Through a reviewed PR, put that agreement in
the README so the team has one current overview.

Choose small next tasks and assign different files where practical: improve
the README, document the source in `data/README.md`, start an exploratory
notebook, or add a useful script. Continue the same branch and PR workflow
from [section 2 above](#2-review-and-merge-a-teammates-pull-request).

For a shared notebook, agree who is editing before work begins. Restart and
run it from top to bottom before review. After merging, tell the next editor
it is available. If a notebook conflicts, coordinate on the intended cells,
rerun the result, and review the rendered notebook; do not choose an entire
version simply because Git calls it yours or theirs.

Before Friday, check that everyone can use `.venv`, the README names the team's
question and responsibilities, and you have agreed who edits each notebook.

## Optional: SSH keys

GitHub Desktop uses **HTTPS**, so signing in to Desktop is enough for today's
workflow; you do not need to create an SSH key. [Desktop connection reference](https://docs.github.com/en/desktop/installing-and-authenticating-to-github-desktop/about-connections-to-github-in-github-desktop).

SSH is another way to authenticate when using Git from a terminal. If you
choose it later, follow GitHub's
[key-generation instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).
Generate the key pair on your computer, then open your avatar → **Settings →
SSH and GPG keys → New SSH key**. Give it a descriptive title, select
**Authentication Key**, and paste the **public `.pub` key**.

Keep the private key on your computer; never paste it into GitHub or commit it.
See [adding the public key to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

## Optional: publish a website with GitHub Pages

Publishing a repository makes its files available on GitHub. **GitHub Pages**
is a separate service that builds a website from a configured branch/folder
or workflow. A repository README and a published webpage are different views.

For a template already prepared to publish from `docs/`:

1. In **your team's repository**, open **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select branch `main`, folder `/docs`, then **Save**.
4. Wait for deployment, then use **Visit site** or the URL GitHub displays.
   Check your team's URL, not the template author's example URL.
5. For a later change to `docs/index.md`, use a branch and reviewed PR. After
   merging to `main`, wait for the site to rebuild and check the rendered page.

These choices assume the repository already contains the site's files in
`docs/`; the small `week3-practice` repository from class does not.
See [configuring a Pages publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

A successful push or merge can still be waiting for a website build. If GitHub
shows the new text but the site does not, check the publishing branch/folder,
deployment status, and site URL. An edit to the root README does not update a
page published from `docs/`.

**Discuss:** The website loads and shows the team's result. What would you
still check before trusting it? Look at the source records, method, code
version, denominator, and whether the claim matches the evidence. A successful
deployment tells you the page was published, not that the research is correct.

Friday's [Lab 3](../../lab/lab03_hidden_berkeley_pages.ipynb) and HW2 use the
supplied Hidden Berkeley page. Follow their instructions for that exercise;
you do not need to author HTML/CSS for Monday's Git practice.
