---
title: About authentication for your enterprise
shortTitle: About authentication
intro: 'You {% ifversion ghae %}must configure SAML single sign-on (SSO) so people can{% else %}can choose how people{% endif %} authenticate to access {% ifversion ghec %}your enterprise''s resources on {% data variables.product.product_name %}{% elsif ghes %}{% data variables.location.product_location %}{% elsif ghae %}your enterprise on {% data variables.product.product_name %}{% endif %}.'
versions:
  ghec: '*'
  ghes: '*'
  ghae: '*'
type: overview
topics:
  - Accounts
  - Authentication
  - Enterprise
  - Identity
  - SSO
---

## About authentication for your enterprise

{% ifversion ghec %}

Enterprise owners on {% data variables.product.product_name %} can control the requirements for authentication and access to the enterprise's resources.

{% data reusables.enterprise.ghec-authentication-options %}

After learning more about these options, to determine which method is best for your enterprise, see "[Identifying the best authentication method for your enterprise](#identifying-the-best-authentication-method-for-your-enterprise)."

## Authentication methods for {% data variables.product.product_name %}

The following options are available for account management and authentication on {% data variables.product.product_name %}.

### Authentication through {% data variables.location.product_location %}

By default, each member must create a personal account on {% data variables.location.product_location %}. You grant access to your enterprise, and the member can access your enterprise's resources after signing into the account on {% data variables.location.product_location %}. The member manages the account, and can contribute to other enterprises, organizations, and repositories on {% data variables.location.product_location %}.

### Authentication through {% data variables.location.product_location %} with additional SAML access restriction

If you configure additional SAML access restriction, each member must create and manage a personal account on {% data variables.location.product_location %}. You grant access to your enterprise, and the member can access your enterprise's resources after both signing into the account on {% data variables.location.product_location %} and successfully authenticating with your SAML identity provider (IdP). The member can contribute to other enterprises, organizations, and repositories on {% data variables.location.product_location %} using their personal account. For more information about requiring SAML authentication for all access your enterprise's resources, see "[AUTOTITLE](/admin/identity-and-access-management/using-saml-for-enterprise-iam/about-saml-for-enterprise-iam)."

You can choose between configuring SAML at the enterprise level, which applies the same SAML configuration to all organizations within the enterprise, and configuring SAML separately for individual organizations. For more information, see "[AUTOTITLE](#deciding-whether-to-configure-saml-at-the-enterprise-level-or-the-organization-level)."

### Authentication with {% data variables.product.prodname_emus %} and federation

If you need more control of the accounts for your enterprise members on {% data variables.location.product_location %}, you can use {% data variables.product.prodname_emus %}. With {% data variables.product.prodname_emus %}, you provision and manage accounts for your enterprise members on {% data variables.location.product_location %} using your IdP. Each member signs into an account that you create, and your enterprise manages the account. Contributions to the rest of {% data variables.product.prodname_dotcom_the_website %} are restricted. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users)."

## Identifying the best authentication method for your enterprise

Both SAML SSO and {% data variables.product.prodname_emus %} increase security for your enterprise's resources. {% data variables.product.prodname_emus %} additionally allows you to control the user accounts for your enterprise members and restricts what the accounts are able to do. However, those restrictions may be unacceptable for your enterprise if they obstruct your developers' workflows.

To determine whether your enterprise would benefit more from SAML SSO or {% data variables.product.prodname_emus %}, ask yourself the following questions.

### Do you want to control the user accounts for your users?

{% data variables.product.prodname_emus %} may be right for your enterprise if you don't want enterprise members to use their own personal accounts on {% data variables.product.prodname_dotcom_the_website %} to access your enterprise's resources.

With SAML SSO, developers create and manage their own personal accounts, and each account is linked to a SAML identity in your IdP. {% data variables.product.prodname_emus %} functions more like other familiar SSO solutions, as you will provision the accounts for your users. You can also ensure user accounts conform with your company identity, by controlling usernames and the email addresses associated with the accounts.

If you currently require your users to create a new account on {% data variables.product.prodname_dotcom_the_website %} to use with your enterprise only, {% data variables.product.prodname_emus %} might be right for you. However, SAML SSO may be a better option if using your IdP as the source of truth for your user and access management would add too much complexity. For example, perhaps your enterprise does not have an established process for onboarding new users in your IdP.

### Which identity provider does your enterprise use?

{% data variables.product.prodname_emus %} is supported for a limited number of IdPs and requires SCIM, while SAML SSO offers full support for a larger number of IdPs, plus limited support for all IdPs that implement the SAML 2.0 standard, and does not require SCIM. For the list of supported IdPs for each option, see "[AUTOTITLE](/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users#identity-provider-support)" and "[AUTOTITLE](/admin/identity-and-access-management/using-saml-for-enterprise-iam/about-saml-for-enterprise-iam#supported-idps)."

You can use {% data variables.product.prodname_emus %} with an unsupported IdP only if you federate the unsupported IdP to a supported IdP to use as an integration point. If you wish to avoid this extra complexity, SAML SSO may be a better solution for you.

### Do your developers work in public repositories, gists, or {% data variables.product.prodname_pages %} sites?

To prevent enterprise members from accidentally leaking corporate-owned content to the public on {% data variables.product.prodname_dotcom_the_website %}, {% data variables.product.prodname_emus %} imposes strong restrictions on what users can do. For example, {% data variables.enterprise.prodname_managed_users %} cannot create public repositories, gists of any visibility, or {% data variables.product.prodname_pages %} sites that are visible outside the enterprise. For a full list of restrictions, see "[AUTOTITLE](/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users#abilities-and-restrictions-of-managed-users)."

These restrictions are unacceptable for some enterprises. To determine whether {% data variables.product.prodname_emus %} will work for you, review the restrictions with your developers, and confirm whether any of the restrictions will hinder your existing workflows. If so, SAML SSO may be a better choice for your enterprise.

### Do your developers rely on collaboration outside of your enterprise?

{% data variables.enterprise.prodname_managed_users_caps %} can only contribute to repositories within your enterprise. If your developers must contribute to both repositories within and outside of your enterprise, including private repositories, {% data variables.product.prodname_emus %} may not be right for your enterprise. SAML SSO may be a better solution.

Some companies maintain repositories within an existing enterprise using SAML SSO on {% data variables.location.product_location %}, and also create an {% data variables.enterprise.prodname_emu_enterprise %}. Developers who contribute to repositories owned by both enterprises from a single workstation must switch between the accounts on {% data variables.location.product_location %} within a single browser, or use a different browser for each account. The developer may also need to customize the workstation's Git configuration to accommodate the two accounts. The complexity of this workflow can increase the risk of mistakenly leaking internal code to the public.

If you decide to create an {% data variables.enterprise.prodname_emu_enterprise %} but require that developers contribute to resources outside of the enterprise from a single workstation, you can provide support for switching between the accounts in a developer's local Git configuration. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users#supporting-developers-with-multiple-user-accounts-on-githubcom)."

### Does your enterprise rely on outside collaborators?

With SAML SSO, you can give access to specific repositories to people who are not members of your IdP's directory, by using the outside collaborator role. This can be especially useful for collaborators that are external to your business, such as contractors. For more information, see "[AUTOTITLE](/organizations/managing-user-access-to-your-organizations-repositories/adding-outside-collaborators-to-repositories-in-your-organization)."

With {% data variables.product.prodname_emus %}, the outside collaborator role does not exist. Your enterprise's resources can only be accessed by {% data variables.enterprise.prodname_managed_users %}, which are always provisioned by your IdP. To give external collaborators access to your enterprise, you would have to use guest accounts in your IdP. If you're interested in {% data variables.product.prodname_emus %}, confirm with your developers whether this will hinder any of their existing workflows. If so, SAML SSO may be a better solution.

### Can your enterprise tolerate migration costs?

If your enterprise is new to {% data variables.product.prodname_dotcom_the_website %}, SAML SSO and {% data variables.product.prodname_emus %} are equally easy to adopt.

If you're already using {% data variables.product.prodname_dotcom_the_website %} with developers managing their own user accounts, adopting {% data variables.product.prodname_emus %} requires migrating to a new enterprise account. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users#getting-started-with-enterprise-managed-users)."

Although {% data variables.product.prodname_emus %} is free, the migration process may require time or cost from your team. Confirm that this migration process is acceptable to your business and your developers. If not, SAML SSO may be the better choice for you.

## Deciding whether to configure SAML at the enterprise level or the organization level

If you decide to use SAML instead of {% data variables.product.prodname_emus %}, you must decide whether to configure SAML at the enterprise level or the organization level.

If some groups within your enterprise must use different SAML authentication providers to grant access to your resources on {% data variables.location.product_location %}, configure SAML for individual organizations. You can implement SAML for your organizations over time by allowing users to gradually authenticate using SAML. Alternatively, you can require SAML authentication by a certain date. Organization members who do not authenticate using SAML by this date will be removed. For more information about organization-level SAML, see "[AUTOTITLE](/organizations/managing-saml-single-sign-on-for-your-organization/about-identity-and-access-management-with-saml-single-sign-on)."

If you configure SAML at the organization level, members are not required to authenticate via SAML to access internal repositories. For more information about internal repositories, see "[AUTOTITLE](/repositories/creating-and-managing-repositories/about-repositories#about-internal-repositories)."

If you need to protect internal repositories or enforce a consistent authentication experience for every organization in your enterprise, you can configure SAML authentication for your enterprise account instead. The SAML configuration for your enterprise overrides any SAML configuration for individual organizations, and organizations cannot override the enterprise configuration. After you configure SAML for your enterprise, organization members must authenticate with SAML before accessing organization resources, including internal repositories.

SCIM is not available for enterprise accounts, and team synchronization is only available for SAML at the enterprise level if you use Azure AD as an IdP. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/using-saml-for-enterprise-iam/managing-team-synchronization-for-organizations-in-your-enterprise)."

Regardless of the SAML implementation you choose, you cannot add external collaborators to organizations or teams. You can only add external collaborators to individual repositories.

{% elsif ghes %}

Site administrators can decide how people authenticate to access a {% data variables.product.product_name %} instance. You can use {% data variables.product.product_name %}'s built-in authentication, or, if you want to centralize identity and access management for the web applications that your team uses, you can configure an external authentication method.

## Authentication methods for {% data variables.product.product_name %}

The following authentication methods are available for {% data variables.product.product_name %}.

### Built-in authentication

{% data reusables.enterprise_user_management.built-in-authentication-new-accounts %} To access your instance, people authenticate with the credentials for the account. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/using-built-in-authentication/configuring-built-in-authentication)."

### External authentication

If you use an external directory or identity provider (IdP) to centralize access to multiple web applications, you may be able to configure external authentication for {% data variables.location.product_location %}. For more information, see the following articles.

- "[AUTOTITLE](/admin/identity-and-access-management/using-cas-for-enterprise-iam)"
- "[AUTOTITLE](/admin/identity-and-access-management/using-ldap-for-enterprise-iam)"
- "[AUTOTITLE](/admin/identity-and-access-management/using-saml-for-enterprise-iam)"

{% data reusables.enterprise.saml-or-ldap %}

If you choose to use external authentication, you can also configure fallback authentication for people who don't have an account on your external authentication provider. For example, you may want to grant access to a contractor or machine user. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/managing-iam-for-your-enterprise/allowing-built-in-authentication-for-users-outside-your-provider)."

{% ifversion scim-for-ghes %}

If you use SAML SSO for authentication, you can also provision users and map IdP groups to teams using SCIM. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/using-saml-for-enterprise-iam/configuring-user-provisioning-with-scim-for-your-enterprise)."

{% endif %}

{% elsif ghae %}

{% data variables.product.product_name %} uses SAML SSO for authentication. Enterprise owners must configure SAML SSO with a SAML identity provider (IdP) during initialization. For more information, see "[AUTOTITLE](/admin/identity-and-access-management/using-saml-for-enterprise-iam/about-saml-for-enterprise-iam)."

{% endif %}

## Further reading

- "[AUTOTITLE](/get-started/learning-about-github/types-of-github-accounts)"
- "[AUTOTITLE](/admin/overview/about-enterprise-accounts)"
{%- ifversion ghec %}
- "[AUTOTITLE](/organizations/managing-membership-in-your-organization/can-i-create-accounts-for-people-in-my-organization)"
- "[AUTOTITLE](/admin/identity-and-access-management/using-saml-for-enterprise-iam/switching-your-saml-configuration-from-an-organization-to-an-enterprise-account)"
{%- endif %}
