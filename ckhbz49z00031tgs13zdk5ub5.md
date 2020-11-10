## Github Action - Workflow Sync | Sync Files Across Repositories

This Github Action can come in handy when you have a lot of projects as I do. wherein some cases certain projects users action workflow which is common across projects. For example: `Project 1` & `Project 2` it can be a pain to keep all the workflow updated with Github Action's Module's version.

This also isn't limited to Github Action YAML files.
Another use case could be keeping the `.editorconfig`, `LICENSE`, `tsconfig.json`, `tslint.json`, `.gitignore`, `azure-pieplines.yml`, etc. in sync across all your repositories.

> Here where this action comes in and reduces your stress 😉 it can update all your repository actions file based on the config provided

# How Files Sync Work?

Before copying the `WORKFLOW_FILES` from the source to the destination. this action will provide some flexibility. this searches for a file in various locations for example lets take `settings.yml` as the file that you want to sync for multiple repositories

#### Below are the locations that this action search for the file/folder
* `./{OWNER}/{REPO_NAME}/workflows/{filename}`
* `./{OWNER}/workflows/{filename}`
* `./{WORKFLOW_FILES_DIR}/{filename}`
* `./.github/workflows/{filename}`
* `./{OWNER}/{REPO_NAME}/{filename}`
* `./{OWNER}/{filename}`
* `./{filename}`

> if the `settings.yml` is found inside the `workflows` folder then the destination is automatically forced to `.github/workflows` in the destination repo
>
> if the `settings.yml` is outside of the `workflows` folder then the destination then its copied to the destination

### How this can be useful?
Let's assume that you want to maintain all the common GitHub files in a single repository and suddenly a repository needs a single file to be changed in that case instead of editing the action `YML` / `YAML` file. you can just create a folder like `{REPO_OWNER}/{REPO_NAME}/{FILE}` to copy the overridden file to the destination

%[https://github.com/varunsridharan/action-github-workflow-sync]

---

Questions or feedback?  Please comment below. 

See all my projects at <a href=https://github.com/varunsridharan/>Github</a>.

Follow me on <a href="https://twitter.com/varunsridharan2">Twitter for updates</a>