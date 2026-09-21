# GitHub Desktop fundamentals

[Concept slides: keeping track of a research project](https://docs.google.com/presentation/d/1WlhH2rzUs7l7Xk1qYEAEDQI9GKQG5Oq3hd-hcYNSoXc/edit).

Monday's practice starts with the short tutorial built into GitHub Desktop, then uses the [Week 3 practice template](https://github.com/macss-berkeley/week03-git-practice). The template is an imaginary text-research project with one question, *Which campus news stories mention housing?*, a short project page, 40 made-up news items, and no results. You will make your own copy, clarify the proposed text-matching rule, publish the page, and review one change with a neighbor. The steps are in the practice sections below.

Friday's [Lab 3](../../lab/lab03_hidden_berkeley_pages.ipynb) practises the same workflow with the supplied Hidden Berkeley page, and HW2 uses that page too. Before Friday, work through the seven-minute interactive [How Git Thinks](https://macss-berkeley.github.io/compss-211a/interactives/week03-how-git-thinks.html), which shows where a change lives after each step. It also opens from your local copy of the course repository at `docs/interactives/week03-how-git-thinks.html`. HTML/CSS authoring is optional.

## What you will practice

By the end of this lesson, you should be able to:

1. explain the difference between Git and GitHub;
2. distinguish a local repository from its remote copy;
3. make, commit, push, and pull a change in GitHub Desktop;
4. publish a Markdown page with GitHub Pages and say what a published page does and does not establish;
5. use a branch and pull request for collaborative work;
6. recognize a merge conflict and inspect it before choosing a resolution.

## Why use version control?

Suppose two people edit the same file, or you overwrite code that worked yesterday. A folder full of names such as `analysis_final_v2_really-final.ipynb` will not tell you what changed or why.

Git records snapshots of a project's files. Each snapshot, or commit, has a message and a place in the project's history. You can inspect earlier versions, compare changes, and return to a known state without keeping a pile of duplicate folders.

Google Docs has a version history for one document. Git applies the same basic idea to a project containing code, data instructions, documentation, and other text files.

## Git and GitHub are different

Git is the version-control software. GitHub hosts remote Git repositories and adds a web interface for collaboration, review, and publishing.

A **repository** is the project folder Git tracks. It contains the current files plus the history stored in its hidden `.git` directory.

- The **local repository** is on your computer.
- The **remote repository** is hosted elsewhere, usually on GitHub in this course.

The two copies do not synchronize automatically:

1. **Commit** records selected local changes with a message.
2. **Push** sends local commits to GitHub.
3. **Pull** brings remote commits to your local repository.

<img src="../../img/workflow.png" alt="Local commits are pushed to GitHub, and remote commits are pulled back to the local repository." width="55%">

## Personal workflow

When you are the only person working in a repository, you will often commit directly to the `main` branch. The basic loop is:

1. inspect the changed files;
2. write a short commit message that explains the change;
3. commit locally;
4. push the commit;
5. check GitHub to confirm that it arrived.

### Create a repository

You can start in either place:

- **GitHub.com:** create a repository and select **Add a README file**. This creates the remote repository. Clone it in GitHub Desktop to create the local copy.
- **GitHub Desktop:** select **Current Repository -> Add -> Create New Repository** and initialize it with a README. This creates the local repository. Select **Publish repository** to create the remote copy.

Today's practice uses a third way. **Use this template** on a GitHub repository creates a new repository under your account, with the template's files as its first commit and none of the template's later history. You then clone it like any other remote repository.

### Practice 0: the GitHub Desktop tutorial

GitHub Desktop includes a short tutorial. It creates a private repository named `desktop-tutorial` under your account, clones it into your Documents/GitHub folder, and shows a panel that tells you the next step: create a branch, edit the README, commit, publish, and open a pull request. It takes about ten minutes.

1. Check that Desktop is signed in to your GitHub account under **Preferences** (macOS) or **Options** (Windows), then **Accounts**.
2. The **Create a Tutorial Repository...** button is on Desktop's start screen, which appears only while no repositories have been added. If you already added one, select it and choose **Repository -> Remove...** without moving it to the Trash. You can add it back later with **File -> Add Local Repository**.
3. Select **Create a Tutorial Repository...**, choose your account, and follow the panel on the left. If it asks you to install a text editor, VS Code was not detected; select **Skip** and open the folder in VS Code yourself.
4. Work through the branch, the edit on line 6 of the README, the commit, and **Publish**. Open the pull request if there is time; otherwise select **Skip**.

If Desktop says you already have a repository named `desktop-tutorial`, you ran the tutorial before. Delete that repository on GitHub under **Settings -> Danger Zone** and try again, or watch a neighbor.

The tutorial covers the branch workflow. It does not commit to `main`, pull, or publish a page. The practices below add those.

### Practice 1: make your copy and record one change

1. Open the [practice template](https://github.com/macss-berkeley/week03-git-practice) on GitHub. Choose **Use this template -> Create a new repository**. Choose your own account as the owner, give the repository a name such as `campus-news-housing`, make it **public** so you can publish the page later, and keep the default branch only.
2. In GitHub Desktop, select **File -> Clone Repository**, choose the **GitHub.com** tab, select your new repository, choose a local folder you can find again, and select **Clone**.
3. Select **Open in Visual Studio Code**. Read `README.md`, `docs/index.md`, and `data/stories.csv`, which holds 40 made-up campus news items.
4. With `data/stories.csv` open, press Cmd+F (macOS) or Ctrl+F (Windows) and search for `housing`. Note the number of matches. Switch **Match Case** (the `Aa` button) on and off, then **Match Whole Word** (the `ab` button), and watch the number change. Read two matching rows, then find two rows that are about housing but do not contain the word.
5. In `docs/index.md`, replace the sentence under **Proposed approach**, `Search each story for the word housing.`, with a rule that says what counts as a match: capitalization, whole words or parts of words, and related words such as *dorm*, *rent*, or *residence hall*. Save the file.

   Pause: the edit now exists in exactly one place. Where?
6. Return to GitHub Desktop and read the diff. Red lines are removed; green lines are added. Check that only the sentence you intended has changed.
7. Write a commit message that names the purpose, such as `Clarify the text-matching rule`, and select **Commit to main**.

   Pause: can a neighbor see this commit on GitHub yet?
8. Select **Push origin**. Open the repository on GitHub.com, open `docs/index.md`, and find your sentence. Open the commit list and find your message.

Question: At which step did the change become part of local history? At which step did it reach GitHub?

### Practice 2: publish the page and check it

GitHub Pages builds a website from the files in `docs/`. The supplied configuration and layout need no edits.

1. On GitHub.com, open **Settings -> Pages**. Under **Build and deployment**, choose **Deploy from a branch**, then branch `main` and folder `/docs`, and select **Save**.
2. While the site builds, return to VS Code and add one sentence to `README.md` describing the imaginary source, for example that the stories would come from one campus news website. Inspect the diff, commit with a clear message, and push.
3. Return to **Settings -> Pages** and open the site URL in a private browser window. Confirm that your matching rule appears on the page.
4. The repository view on GitHub shows the README; the website shows `docs/index.md`. Confirm which of your two edits is visible in which place.

Question: GitHub.com shows your new sentence, but the website still shows the old one. Name two different explanations, and say what you would look at to tell them apart.

## Collaborative workflow

When several people share a repository, use branches to keep unfinished work away from `main`.

A **branch** is another line of development inside the same repository. A **fork** is a separate copy of someone else's repository under another GitHub account. Team members with access to the same repository usually use branches. Outside contributors often use forks.

<img src="../../img/collaborative.png" alt="Contributors develop changes separately and merge reviewed work into the main branch." width="55%">

### Practice 3: propose a change on a branch and review a neighbor's

Work in your own copy of the template. Because the repository is public, a neighbor can read and comment on your pull request without being added as a collaborator.

1. In GitHub Desktop, switch to `main`, select **Fetch origin**, and pull if Desktop reports remote changes.
2. Select **Current Branch -> New Branch** and name it after the task, such as `explain-the-limits`.
3. In `docs/index.md`, under **What we would check**, add one sentence about a limit of your matching rule, naming one story from `data/stories.csv` by its `story_id` that the rule counts by mistake or misses.
4. Inspect the diff and commit on your branch.
5. Select **Publish branch**, then **Preview Pull Request**. Confirm that the base branch is `main`, the compare branch is yours, and only `docs/index.md` changed. Select **Create Pull Request**, then write a title and one sentence saying what a reviewer should check.
6. Swap repository URLs with a neighbor. Open their pull request, read the **Files changed** tab, and leave one comment: a question, or one specific improvement.
7. Read the comment on your own pull request. If you change the sentence, commit again on the same branch and push; the pull request updates by itself. Then select **Merge pull request** on GitHub.
8. In GitHub Desktop, switch to `main`, select **Fetch origin**, then **Pull origin**. Open `docs/index.md` and confirm that the merged sentence is on your computer. Delete the finished branch.
9. When the site has rebuilt, confirm the sentence on the published page.

A pull request is a review conversation around a proposed merge. It does not automatically make the code correct.

Question: Your neighbor's comment changed what you wrote. Where is that conversation recorded, and where would a third person go to read it?

## Merge conflicts

A conflict occurs when Git cannot combine changes automatically, often because two branches edited the same lines. Nothing in the practice above should produce one: each of you works in your own repository, on one branch at a time. The instructor will demonstrate a conflict in class, and the optional playground exercise below lets you produce one deliberately.

Do not resolve a conflict by choosing a side blindly. The correct result may keep one version, combine both, or replace both. After resolving a code conflict, rerun the relevant check. If a notebook conflicts, stop and coordinate with the other editor: `.ipynb` files are structured JSON and are much harder to merge safely than Markdown or Python files.

## Optional extra practice in the Git Playground

The [Git Playground](https://github.com/macss-berkeley/git-playground) is a separate shared repository for practising the same workflow on a repository that other people also edit, and for producing a merge conflict on purpose. It is optional.

### Fork and clone the playground

1. Fork the playground to your account.
2. In GitHub Desktop, select **File -> Clone Repository**.
3. Select your fork and choose a local folder you can find again.
4. If GitHub Desktop asks how you plan to use the fork, select **To contribute to the parent project**.
5. Read the playground README. Do not edit `conflicts/team_plan.md` until the merge-conflict exercise.

### Make a branch and pull request in the playground

This branch exercise is intentionally conflict-free.

1. Select **Current Branch -> New Branch** and use a descriptive name such as `add-river-contributor-note`.
2. In `contributors/`, copy `example.md` to a new file named with your GitHub username, such as `river.md`.
3. Replace the placeholders in your file. Do not edit another student's file, the repository README, or the conflict fixture.
4. Inspect the diff and commit the change on your branch.
5. Select **Publish branch**, then **Preview Pull Request**.
6. Confirm that the base branch is `main`, the compare branch is yours, and only your contributor file changed.
7. Select **Create Pull Request**, then write a title and short description in the browser.
8. Ask a teammate to inspect the **Files changed** tab and explain what they would approve or request before merging.

### Practise a controlled merge conflict

Complete the branch exercise first, then work in your own fork:

1. Commit any current work. Switch to `main`, select **Fetch origin**, and pull if GitHub Desktop reports remote changes.
2. Create a branch named `conflict-option-a` from `main`.
3. Open `conflicts/team_plan.md` and replace only the line beginning `Review rule:` with one concrete rule. Save, inspect, and commit the change.
4. Switch back to `main` without merging option A. Create a second branch named `conflict-option-b` from the same `main` commit.
5. Replace the same `Review rule:` line with a different rule, then commit it.
6. Switch to `main`. Select **Current Branch -> Choose a branch to merge into main**, choose `conflict-option-a`, complete the merge, and push your fork's `main`.
7. Switch to `conflict-option-b`. Select **Current Branch -> Choose a branch to merge into conflict-option-b**, then choose `main`. GitHub Desktop should report a conflict in `conflicts/team_plan.md`.
8. Open the repository in VS Code. Read both versions between `<<<<<<<`, `=======`, and `>>>>>>>`. Edit the file into the single final rule you actually want and remove every conflict marker.
9. Save the file. When GitHub Desktop reports that all conflicts are resolved, continue the merge and inspect the resulting commit.
10. Push `conflict-option-b`, open a pull request into your fork's `main`, and ask a teammate to verify that the final rule is coherent and contains no conflict markers.

Question: What evidence shows that your resolution preserved the intended work from both branches?

## Removing repositories and branches

These actions discard information, so verify the target first.

- Removing a repository from GitHub Desktop does not necessarily delete its local folder.
- Deleting the hidden `.git` directory removes local Git history but leaves the visible project files.
- Deleting the entire project folder removes both files and local history.
- Deleting a remote repository happens under **Settings -> Danger Zone** on GitHub and cannot be undone through the normal interface.
- A merged branch can usually be deleted after confirming that its commits are on `main`.

## What to remember

- Saving a file changes your working copy; a commit records local history; a push transfers commits to a remote.
- Inspect changes before committing or resolving a conflict.
- Pull before starting shared work, especially when teammates may have pushed changes.
- Use a branch and pull request when the change needs review before it reaches `main`.
- GitHub Pages builds the site from the pushed repository, not from the files on your computer. A finished push can still be waiting for the site to build.
