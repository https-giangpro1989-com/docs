---
title: Configuring prebuilds
shortTitle: Configure prebuilds
intro: You can configure your project to prebuild a codespace automatically each time you push a change to your repository.
versions:
  fpt: '*'
  ghec: '*'
type: how_to
topics:
  - Codespaces
  - Set up
permissions: People with admin access to a repository can configure prebuilds for the repository.
---

You can set up a prebuild configuration for the combination of a specific branch of your repository with a specific dev container configuration file.

Any branches created from a prebuild-enabled parent branch will typically also get prebuilds for the same dev container configuration. This is because prebuilds for child branches that use the same dev container configuration as the parent branch are, for the most part, identical, so developers can benefit from faster codespace creation times on those branches also. For more information, see "[AUTOTITLE](/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers)."

Typically, when you configure prebuilds for a branch, prebuilds will be available for multiple machine types. However, if your repository is greater than 32 GB, prebuilds won't be available for 2-core and 4-core machine types, since the storage these provide is limited to 32 GB.

## Prerequisites

Prebuilds are created using {% data variables.product.prodname_actions %}. As a result, {% data variables.product.prodname_actions %} must be enabled for the repository for which you are configuring prebuilds. For more information, see "[AUTOTITLE](/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)."

## Configuring prebuilds

{% data reusables.codespaces.accessing-prebuild-configuration %}
1. In the "Prebuild configuration" section of the page, click **Set up prebuild**.

   ![Screenshot of the "Prebuild configuration" section of the "Codespaces" settings page, showing the "Set up prebuilds" button.](/assets/images/help/codespaces/prebuilds-set-up.png)

1. Choose the branch for which you want to set up prebuilds.

   ![Screenshot of the "Configuration" settings for a prebuild with a dropdown menu listing branches to select. The "main" branch is currently selected.](/assets/images/help/codespaces/prebuilds-choose-branch.png)

   {% note %}

   **Note**: Any branches created from a prebuild-enabled base branch will typically also get prebuilds for the same dev container configuration. For example, if you enable prebuilds for a dev container configuration file on the default branch of the repository, branches based on the default branch will, in most cases, also get prebuilds for the same dev container configuration.

   {% endnote %}

1. Optionally, in the **Configuration file** dropdown menu that's displayed, choose the `devcontainer.json` configuration file that you want to use for your prebuilds. For more information, see "[AUTOTITLE](/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers#devcontainerjson)."

   ![Screenshot of the configuration file dropdown menu. Four configuration files are listed, with ".devcontainer/devcontainer.json" currently selected.](/assets/images/help/codespaces/prebuilds-choose-configfile.png)

1. Choose how you want to automatically trigger prebuild updates.

   - **Every push** (the default setting) - With this setting, prebuilds will be updated on every push made to the given branch. This will ensure that codespaces generated from a prebuild always contain the latest codespace configuration, including any recently added or updated dependencies.

   - **On configuration change** - With this setting, prebuilds will be updated every time any of the following files is changed:
     - `.devcontainer/devcontainer.json`

       {% note %}

       **Note**: Prebuild updates are not triggered by changes to `devcontainer.json` files within subdirectories of `.devcontainer`.

       {% endnote %}

     - The Dockerfile referenced in the `build.dockerfile` property of the `.devcontainer/devcontainer.json` file.

     This setting ensures that changes to the dev container configuration files for the repository are used when a codespace is generated from a prebuild. The {% data variables.product.prodname_actions %} workflow that updates the prebuilds will run less often, so this option will use fewer {% data variables.product.prodname_actions %} minutes. However, this option will not guarantee that codespaces always include recently added or updated dependencies, so these may have to be added or updated manually after a codespace has been created.

   - **Scheduled** - With this setting, you can have your prebuilds updated on a custom schedule that's defined by you. This can reduce consumption of {% data variables.product.prodname_actions %} minutes, however, with this option, codespaces may be created that do not use the latest dev container configuration changes.

   ![Screenshot of the "Prebuild triggers" settings. The "Scheduled" option is selected and set to "Every day" at "1pm" and "3:30pm."](/assets/images/help/codespaces/prebuilds-triggers.png)

1. Optionally, select **Reduce prebuild available to only specific regions** to create prebuilds only in specified regions. Select the regions in which you want prebuilds to be available.

   By default, prebuilds are created in all of the available regions, incurring storage charges per prebuild.

   ![Screenshot of the "Region availability" settings. "Reduce prebuild available to only specific regions" is selected with two regions selected.](/assets/images/help/codespaces/prebuilds-regions.png)

   {% note %}

   **Notes**:
   * The prebuild in each region incurs individual storage charges. You should, therefore, only enable prebuilds for regions in which you know they'll be used. For more information, see "[AUTOTITLE](/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces#billing-for-codespaces-prebuilds)."
   * Developers can set their default region for {% data variables.product.prodname_github_codespaces %}, which can allow you to enable prebuilds for fewer regions. For more information, see "[AUTOTITLE](/codespaces/customizing-your-codespace/setting-your-default-region-for-github-codespaces)."

   {% endnote %}

1. Optionally, under **Template history**, set the number of prebuild versions to be retained. You can input any number between 1 and 5. The default number of saved versions is 2, which means that only the latest prebuild and the previous version are saved.

   ![Screenshot of the "Template history" setting. It is set to 2 versions.](/assets/images/help/codespaces/prebuilds-template-history-setting.png)

   Depending on your prebuild trigger settings, your prebuild could change with each push or on each dev container configuration change. Retaining older versions of prebuilds enables you to create a prebuild from an older commit with a different dev container configuration than the current prebuild. This setting allows you to set the number of retained versions to a level that is appropriate for your needs.

   If you set the number of prebuild versions to save to 1, {% data variables.product.prodname_github_codespaces %} will only save the latest version of the prebuild and will delete the older version each time the template is updated. This means you will not get a prebuilt codespace if you go back to an older dev container configuration.

   There is a storage cost associated with each prebuild version that's retained. For example, if you are generating prebuilds in 4 regions and retaining 2 versions, you will be charged for storage of up to 8 prebuilds. For more information on billing, see "[AUTOTITLE](/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces#codespaces-pricing)."

1. Optionally, add users or teams to notify when the prebuild workflow run fails for this configuration. You can begin typing a username, team name, or full name, then click the name once it appears to add them to the list. The users or teams you add will receive an email when prebuild failures occur, containing a link to the workflow run logs to help with further investigation.

   ![Screenshot of the "Failure notifications" setting. The team named "octocat-team" has been added.](/assets/images/help/codespaces/prebuilds-failure-notification-setting.png)

1. Optionally, at the bottom of the page, click **Show advanced options**.

   ![Screenshot of the bottom of the prebuilds configuration page. The link "Show advanced options" is highlighted with a dark orange outline.](/assets/images/help/codespaces/show-advanced-options.png)

   In the "Advanced options" section, if you select **Disable prebuild optimization**, codespaces will be created without a prebuild if the latest prebuild workflow has failed or is currently running. For more information, see "[AUTOTITLE](/codespaces/troubleshooting/troubleshooting-prebuilds#preventing-out-of-date-prebuilds-being-used)."

1. Click **Create**.

   {% data reusables.codespaces.prebuilds-permission-authorization %}

After you create a prebuild configuration it is listed on the {% data variables.product.prodname_github_codespaces %} page of your repository settings. A {% data variables.product.prodname_actions %} workflow is queued and then run to create prebuilds in the regions you specified, based on the branch and dev container configuration file you selected.

![Screenshot of the list of prebuild configurations. One prebuild is listed, labeled "Currently running." To the right of it is a "See output" button.](/assets/images/help/codespaces/prebuild-configs-list.png)

For information about editing and deleting prebuild configurations, see "[AUTOTITLE](/codespaces/prebuilding-your-codespaces/managing-prebuilds)."

## Configuring environment variables

To allow the prebuild process to access environment variables required to create your development environment, you can set these either as {% data variables.product.prodname_codespaces %} repository secrets or as {% data variables.product.prodname_codespaces %} organization secrets. For more information, see "[AUTOTITLE](/codespaces/managing-codespaces-for-your-organization/managing-encrypted-secrets-for-your-repository-and-organization-for-github-codespaces#adding-secrets-for-a-repository)" and "[AUTOTITLE](/codespaces/managing-codespaces-for-your-organization/managing-encrypted-secrets-for-your-repository-and-organization-for-github-codespaces#adding-secrets-for-an-organization)."

Secrets that you create in this way will be accessible by anyone who creates a codespace from this repository. If you do not want this, you can alternatively set the `CODESPACES_PREBUILD_TOKEN` secret. The `CODESPACES_PREBUILD_TOKEN` secret is only used for prebuilding and its value is not accessible in users' codespaces.

Prebuilds cannot use any user-level secrets while building your environment, because these are not available until after the codespace has been created.

## Configuring time-consuming tasks to be included in the prebuild

You can use the `onCreateCommand` and `updateContentCommand` commands in your `devcontainer.json` to include time-consuming processes as part of the prebuild creation. For more information, see the {% data variables.product.prodname_vscode %} documentation, "[devcontainer.json reference](https://code.visualstudio.com/docs/remote/devcontainerjson-reference#_lifecycle-scripts)."

`onCreateCommand` is run only once, when the prebuild is created, whereas `updateContentCommand` is run at creation of the prebuild and at subsequent updates to it. Incremental builds should be included in `updateContentCommand` since they represent the source of your project and need to be included for every prebuild update.

## Further reading

- "[AUTOTITLE](/codespaces/prebuilding-your-codespaces/allowing-a-prebuild-to-access-other-repositories)"
- "[AUTOTITLE](/codespaces/troubleshooting/troubleshooting-prebuilds)"
