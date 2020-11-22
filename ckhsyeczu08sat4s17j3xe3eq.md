## How to publish a Github action

You can publish the actions you have created to the GitHub Marketplace and share your actions with the GitHub community.

> Your repository must only include the metadata file, code, and files necessary for the action. 

> Creating a single repository for the action allows you tag, release, and package the code in a single unit. 

> GitHub also uses the action's metadata on your GitHub Marketplace page.

## Prerequisites
Actions are published to GitHub Marketplace immediately without review, as long as they meet the below requirements:

1. The action must be in a public repository. 
1. Each repository must contain a single action. 
1. The action's metadata file (`action.yml` or `action.yaml`) must be in the root directory of the repository. 
1. The `name` in the action's metadata file must be unique. 
    1. The `name` cannot match an existing action name on GitHub Marketplace. 
    1. The `name` cannot match a user or organization on GitHub, unless the user or organization owner is publishing the action.
    1. The `name` cannot match an existing GitHub Marketplace category. 
    1. GitHub reserves the names of GitHub features.

## Publishing and removing an action
You can add the action you created to the GitHub Marketplace by tagging it as a new release and publishing it, or you can remove it. Github’s documentation for publishing and removing an action is illustrative and straightforward. You can see the steps in the [Publishing an action](https://docs.github.com/en/free-pro-team@latest/actions/creating-actions/publishing-actions-in-github-marketplace#publishing-an-action) section.

%[https://docs.github.com/en/free-pro-team@latest/actions/creating-actions/publishing-actions-in-github-marketplace]

---

%%[blog-footer]