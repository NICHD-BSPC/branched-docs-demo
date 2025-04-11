# Branched Docs Demo

This repository demonstrates how to deploy different branches of a Jekyll site to subfolders on the repository's GitHub Pages site. This allows you to keep different site versions available without affecting the main (latest) site. Updates will occur whenever there are pushes to the `main` branch or to any branch that follows the specified naming convention.

## Branch Naming Convention

To publish a branch to GitHub Pages, use the `site-v*` naming convention for your branches. For example, `site-v1`, `site-v2`, etc. Other branches will be ignored, so you can use non-matching branch names for in-progress work.

### Editing the Branch Pattern in `jekyll-gh-pages.yml`

If you wish to use a different naming convention, replace all instances of the string `site-v*` within the `jekyll-gh-pages.yml` file with your desired branch pattern. The patterns should follow the glob-like expressions used by GitHub (see [docs](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule#about-branch-protection-rules)).

## GitHub Pages Configuration

The `jekyll-gh-pages.yml` workflow runs on each branch that matches the naming convention and commits the resulting site assets (HTML, images, etc.) to a corresponding folder on the `gh-pages` branch. The GitHub Actions Pages configuration then handles the deployment of that branch to the GitHub Pages site.

To configure GitHub Pages for your repository, follow these steps:

1. **Access GitHub Pages Settings**:
   - Go to your repository and click on **Settings**.
   - Click on the **Pages** section on the left. (You must be at least a Maintainer to see this setting.)
   - Under **Build and Deployment**, select "Deploy from a branch," then choose the `gh-pages` branch and the root folder.

2. **Configure Environments**:
   - Click on **Environments** on the left. (You must be an Admin to see this setting.)
   - Click on the `github-pages` environment that should be automatically created.
   - Go to **Deployment branches and tags** and ensure the following are added to the list of branches:
      - `main`
      - `gh-pages`
      - `site-v*` (this should be the same pattern as what's used in `jekyll-gh-pages.yml`).

For each push to a matching branch, you will observe two deployments: one that builds the files and pushes the assets to the `gh-pages` branch, and another that deploys the site from the `gh-pages` branch.
