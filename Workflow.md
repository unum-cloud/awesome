# Organizing Software Development

There are a lot's of buzzwords like test-driver development, or continuos integration/deployment/profiling, or agile, but as always, everyone understands them differently.
Here is our structure for organizing software development.

1. If you want to add/edit/remove code, first, open an issue.
2. Every issue, has gets it's own branch in the same repo, generally forked from `main-dev`.
   1. If you want your every commit displayed and discussed, push right there.
   2. If you want to work on something privately, fork it under your own username.
3. For your Pull Request to pass a review, submit not just the code, but also the tests, and the documentation.

Sounds simple.
Now let's dive into details.

## Git Credentials

- `git config --global user.email "id+username@users.noreply.github.com"`

Git is amazing.
It allows navigating the history, ~~to punish the guilty, and to liberate the oppressed~~...
It doesn't work, however, if your `git log` looks like this:

```txt
commit e5ca9b4b78bfe359a1a293c5cba0526eed02ec54
Author: Ash <ash@localhost>
Date:   Tue Jun 14 18:05:38 2022 +0400
```

The obvious recommendation is to use real full names and reachable emails, instead of `localhost` names.
But there is probably a better way.
The GitHub profile is the face of the software developer.
If you want to build a career, select a nickname, register a GitHub account, and you will get a unique ID.
Concatenating those, you will get a special GitHub address, that I use for all my commits.

```txt
commit e5ca9b4b78bfe359a1a293c5cba0526eed02ec54
Author: Ashot Vardanian <1983160+ashvardanian@users.noreply.github.com>
Date:   Tue Jun 14 18:05:38 2022 +0400
```

> Configuring Git credentials.

## Branches

- `main` for last stable version.
- `main-dev` to synchronize the development.
- `150-feature-add-something`-like branch per issue.
- `v1.0.0`-like branch per LTS version.

Since ~~the dawn of time~~ around 2020, the default branch on Github is called `main`, and not `master`.
That is where the most recent stable version of your software lives.

The `trunk`, `development`, or shorter `dev`, are generally the most active parts of your project.
In our case, we call that branch `main-dev`, because of the way branch protection rules are defined for GitHub.
All the `main*` branches we protect.
Currently with the following rules:

- [x] Require Pull Request Before Merging
  - [x] Require approvals
  - [ ] Dismiss stale pull request approvals when new commits are pushed
  - [x] Require review from Code Owners
  - [ ] Restrict who can dismiss pull request reviews
  - [x] Allow specified actors to bypass required pull requests: core maintainers
  - [ ] Require approval of the most recent reviewable push
- [ ] Require status checks to pass before merging [info](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches#require-status-checks-before-merging)
- [x] Require conversation resolution before merging [info](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches#require-conversation-resolution-before-merging)
- [ ] Require signed commits [info](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches#require-signed-commits)
- [ ] Require linear history [info](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches#require-linear-history)
- [ ] Require deployments to succeed before merging [info](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/about-protected-branches#require-deployments-to-succeed-before-merging)
- [ ] Lock branch
- [ ] Do not allow bypassing the above settings
- [x] Restrict who can push to matching branches
  - [x] Restrict pushes that create matching branches: core maintainers

> [More on the default branch names](https://www.biteinteractive.com/of-git-and-github-master-and-main/).

## Issues

- Every major repo should have issue templates at `.github/ISSUE_TEMPLATE`.
- Issue names should be capitalized, without sentence termination punctuation marks.

> [More on the issue templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates)

## Commits

- Title should continue the sentence: This commit will ...
- Title line should be 50 characters or less.
- Title needs no sentence termination punctuation marks.
- Before title you should put a [commit type](#commit-types).
- Descriptions are optional. If present should be 72 characters or less.

As a result, the commit message would look like this.

```txt
Fix: Short (50 chars or less) summary

More detailed explanatory text. Wrap it to 72 characters. The blank
line separating the summary from the body is critical (unless you omit
the body entirely).

Write your commit message in the imperative: "Fix bug" and not "Fixed
bug" or "Fixes bug." This convention matches up with commit messages
generated by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Bullet points are okay, too.
- Typically a hyphen or asterisk is used for the bullet, followed by a
  single space. Use a hanging indent.
```

### Commit Types

## Versioning

- Every repo has a root level `VERSION` file.
- Contents are `major.minor.patch` followed by newline.

We use a variation of Semantic Versioning.
The only difference being, that we sometimes prefer to use the depth of the Git branch as the `patch` number.
