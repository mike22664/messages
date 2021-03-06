---
title: Managing the default branch name for repositories in your organization
intro: 'You can set the default branch name for repositories that members create in your organization.'
permissions: Managing the default branch name for your repositories
versions:
  free-pro-team: '*'
  enterprise-server: '>=2.23'
---

### About the default branch name

When a member of your organization creates a new repository, {% data variables.product.prodname_dotcom %} will create a single branch and set it as the repository's default branch. You can change the name that {% data variables.product.product_name %} uses for the default branch in new repositories that members of your organization create. For more information about the default branch, see "[About branches](/github/collaborating-with-issues-and-pull-requests/about-branches#about-the-default-branch)."

{% data reusables.branches.set-default-branch %}

### Setting the default branch name

{% data reusables.profile.access_profile %}
{% data reusables.profile.access_org %}
{% data reusables.organizations.org_settings %}
{% data reusables.organizations.repository-defaults %}
3. Under "Repository default branch", click **Change default branch name now**. ![Override button](/assets/images/help/organizations/repo-default-name-button.png)
    {% note %}

    **Note:** If your enterprise owner has enforced a policy for the default name, you won't be able to change it here. You will be able to set the default branch on individual repositories. For more information, see "[Enforcing a policy on the default branch name](/github/setting-up-and-managing-your-enterprise-account/enforcing-repository-management-policies-in-your-enterprise-account#enforcing-a-policy-on-the-default-branch-name)" and "[Setting the default branch](/github/administering-a-repository/setting-the-default-branch)."

    {% endnote %}
4. Type the default name that you would like to use for new branches. ![Text box for entering default name](/assets/images/help/organizations/repo-default-name-text.png)
5. Click **Update**. ![Update button](/assets/images/help/organizations/repo-default-name-update.png)

### ??? ????????????

- /github/setting-up-and-managing-your-github-user-account/managing-the-default-branch-name-for-your-repositories
