---
title: Managing branches
intro: You can create a branch off of a repository's default branch so you can safely experiment with changes.
redirect_from:
  - /desktop/contributing-to-projects/creating-a-branch-for-your-work
  - /desktop/contributing-to-projects/switching-between-branches
  - /desktop/contributing-to-projects/managing-branches
  - /desktop/contributing-and-collaborating-using-github-desktop/managing-branches
versions:
  fpt: '*'
---
## About managing branches
You can use branches to safely experiment with changes to your project. Branches isolate your development work from other branches in the repository. For example, you could use a branch to develop a new feature or fix a bug.

You always create a branch from an existing branch. Typically, you might create a branch from the default branch of your repository. You can then work on this new branch in isolation from changes that other people are making to the repository.

You can also create a branch starting from a previous commit in a branch's history. This can be helpful if you need to return to an earlier view of the repository to investigate a bug, or to create a hot fix on top of your latest release.

Once you're satisfied with your work, you can create a pull request to merge your changes in the current branch into another branch. For more information, see "[AUTOTITLE](/desktop/contributing-and-collaborating-using-github-desktop/working-with-your-remote-repository-on-github-or-github-enterprise/creating-an-issue-or-pull-request)" and "[AUTOTITLE](/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)."

You can always create a branch in {% data variables.product.prodname_desktop %} if you have read access to a repository, but you can only push the branch to {% data variables.product.prodname_dotcom %} if you have write access to the repository.

{% data reusables.desktop.protected-branches %}

## Creating a branch

{% tip %}

**Tip:** The first new branch you create will be based on the default branch. If you have more than one branch, you can choose to base the new branch on the currently checked out branch or the default branch.

{% endtip %}

{% mac %}

{% data reusables.desktop.click-base-branch-in-drop-down %}
  ![Screenshot of the "Current Branch" dropdown view. Under "Recent Branches", a branch, named "my-feature", is highlighted with an orange outline.](/assets/images/help/desktop/select-branch-from-dropdown.png)
{% data reusables.desktop.create-new-branch %}
  ![Screenshot of the "Current Branch" dropdown view. Next to the "Filter" field, a button, labeled "New Branch", is outlined in orange.](/assets/images/help/desktop/new-branch-button-mac.png)
{% data reusables.desktop.name-branch %}
{% data reusables.desktop.select-base-branch %}
{% data reusables.desktop.confirm-new-branch-button %}

{% endmac %}

{% windows %}

{% data reusables.desktop.click-base-branch-in-drop-down %}
  ![Drop-down menu to switch your current branch](/assets/images/help/desktop/click-branch-in-drop-down-win.png)
{% data reusables.desktop.create-new-branch %}
  ![New Branch option in the Branch menu](/assets/images/help/desktop/new-branch-button-win.png)
{% data reusables.desktop.name-branch %}
{% data reusables.desktop.select-base-branch %}
{% data reusables.desktop.confirm-new-branch-button %}

{% endwindows %}

## Creating a branch from a previous commit

{% data reusables.desktop.history-tab %}
2. Right-click on the commit you would like to create a new branch from and select **Create Branch from Commit**.
  
  ![Screenshot of a list of commits in the "History" tab. Next to a commit, in a context menu, the cursor hovers over the "Create Branch from Commit" option.](/assets/images/help/desktop/create-branch-from-commit-context-menu.png)

{% data reusables.desktop.name-branch %}
{% data reusables.desktop.confirm-new-branch-button %}

## Publishing a branch

If you create a branch on {% data variables.product.product_name %}, you'll need to publish the branch to make it available for collaboration on {% data variables.product.prodname_dotcom %}.

1. In the repository bar, click {% octicon "git-branch" aria-label="The branch icon" %} **Current Branch**, then click the branch that you want to publish.
  ![Screenshot of the "Current Branch" dropdown view. Under "Recent Branches", a branch, named "my-feature", is highlighted with an orange outline.](/assets/images/help/desktop/select-branch-from-dropdown.png)
2. Click **Publish branch**.
  ![Screenshot of the repository bar. On the right-hand side, a button, labeled "Publish branch", is highlighted with an orange outline.](/assets/images/help/desktop/publish-branch-button.png)

## Switching between branches
You can view and make commits to any of your repository's branches. If you have uncommitted, saved changes, you'll need to decide what to do with your changes before you can switch branches. You can commit your changes on the current branch, stash your changes to temporarily save them on the current branch, or bring the changes to your new branch. If you want to commit your changes before switching branches, see "[AUTOTITLE](/desktop/contributing-and-collaborating-using-github-desktop/making-changes-in-a-branch/committing-and-reviewing-changes-to-your-project)."
{% tip %}

**Tip**: You can set a default behavior for switching branches in the **Advanced** settings. For more information, see "[AUTOTITLE](/desktop/installing-and-configuring-github-desktop/configuring-and-customizing-github-desktop/configuring-basic-settings)."

{% endtip %}

1. In the repository bar, click {% octicon "git-branch" aria-label="The branch icon" %} **Current Branch**, then click the branch that you want to switch to.
  ![Screenshot of the "Current Branch" dropdown view. Under "Recent Branches", a branch, named "my-feature", is highlighted with an orange outline.](/assets/images/help/desktop/select-branch-from-dropdown.png)
1. If you have saved, uncommitted changes, in the "Switch Branch" window, select **Leave my changes on CURRENT-BRANCH** or **Bring my changes to NEW-BRANCH**, then click **Switch Branch**.

## Deleting a branch

You can't delete a branch if it's currently associated with an open pull request. You cannot undo deleting a branch.

{% mac %}

{% data reusables.desktop.select-branch-to-delete %}
  ![Screenshot of the "Current Branch" dropdown view. Under "Recent Branches", a branch, named "my-feature", is highlighted with an orange outline.](/assets/images/help/desktop/select-branch-from-dropdown.png)
{% data reusables.desktop.delete-branch-mac %}
  ![Screenshot of the menu bar on a Mac. In the expanded "Branch" dropdown menu, the cursor hovers over the "Delete" option, highlighted in blue.](/assets/images/help/desktop/delete-branch-mac.png)

{% endmac %}

{% windows %}

{% data reusables.desktop.select-branch-to-delete %}
  ![Screenshot of the "Current Branch" dropdown view. Under "Recent Branches", a branch, named "my-feature", is highlighted with an orange outline.](/assets/images/help/desktop/select-branch-from-dropdown.png)
{% data reusables.desktop.delete-branch-win %}
  ![Delete... option in the Branch menu](/assets/images/help/desktop/delete-branch-win.png)

{% endwindows %}

## Further reading

- "[AUTOTITLE](/desktop/contributing-and-collaborating-using-github-desktop/adding-and-cloning-repositories/cloning-a-repository-from-github-to-github-desktop)"
- "[AUTOTITLE](/get-started/quickstart/github-glossary#branch)" in the {% data variables.product.prodname_dotcom %} glossary
- "[AUTOTITLE](/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches)"
- "[Branches in a Nutshell](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)" in the Git documentation
- "[AUTOTITLE](/desktop/contributing-and-collaborating-using-github-desktop/making-changes-in-a-branch/stashing-changes)"
