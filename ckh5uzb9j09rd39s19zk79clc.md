## GitHub Action - Repository Roster | 📢 Shout-out Supporters In Your README.md

As developers, we put a lot of work into our GitHub repos to make them as useful as possible for others, but great projects sometimes go under-appreciated, and under-starred. Asking for stars is tacky, but publicly thanking your supporters by name in your **README** file is a sign of appreciation that happens to incentivize more users to join the crowd.

## 💡 Inspiration
One fine day I got an email [DEV Digest](https://s2.do-spaces.com/2020/Nov/03/1604373796-15.jpg) in which I got attracted by the title [**1 Step to Incentivize Stars and Forks on GitHub**](https://dev.to/nastyox1/1-step-to-incentivize-stars-and-forks-on-github-2md3) and decided to read the full article. it was new & interesting to me. Thanks to @ [nastyox1](https://dev.to/nastyox1) creating such an awesome tool. so I wanted to use it but I wanted it to be a `markdown-table` output which was not an option with that cloud-hosted service. so I decided to create this as an action that can provide various outputs.

check out the [examples output](https://github.com/varunsridharan/action-repository-roster/tree/main/examples)

---

## 🚀  Usage
1. Update Your `README.md` with the below code
2. Setup Action Workflow File

***Repository Stargazers***
```markdown
## ↳ Stargazers
<!-- REPOSITORY_STARS:START --> <!-- REPOSITORY_STARS:END -->
```

***Repository Forks***
```markdown
## ↳ Forkers
<!-- REPOSITORY_FORKS:START --><!-- REPOSITORY_FORKS:END -->
```
> ℹ️  Currently there are ways to auto-trigger the workflow when a user **stars** / **forks** the repository.
>
> ℹ️  Using this action with the workflow trigger [fork](https://docs.github.com/en/free-pro-team@latest/actions/reference/events-that-trigger-workflows#fork) & [watch](https://docs.github.com/en/free-pro-team@latest/actions/reference/events-that-trigger-workflows#watch) is the best optmized way.
>
> if you want to remove users that have un-stared / deleted the fork then you might have to use [cron](https://docs.github.com/en/free-pro-team@latest/actions/reference/events-that-trigger-workflows#schedule) to handle it

## Workflow File

```yml
name: "🙏 Repository Roster"

on:
  workflow_dispatch:
  fork:
  watch:
    types:
      - started

jobs:
  update_latest_roster:
    name: "🐔  Update Latest Roster"
    runs-on: ubuntu-latest
    steps:
      - name: "📥  Fetching Repository Contents"
        uses: actions/checkout@main

      - name: "🐔  Markdown - Repository Roster"
        uses: "varunsridharan/action-repository-roster@main"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```

## Example Output
![https://s2.do-spaces.com/2020/Nov/06/1604642798-178.jpg](https://s2.do-spaces.com/2020/Nov/06/1604642798-178.jpg)


For more details about the available config options. please check our GitHub repository 

%[https://github.com/varunsridharan/action-repository-roster]
