## How To Show Latest Hashnode Blog Posts In Github Profile Readme?

Hi There,

I recently decided to start my own [blog] using **Hashnode**. after setting up the blog I found out that there is no **GitHub action** which can update my [Github Profile Readme] with the latest posts I write here.

So I decided to jump into work and started to create a GitHub action that can do the job. 

---


## 🎉 Github Action For Hashnode Blogs 🎉
%[https://github.com/varunsridharan/action-hashnode-blog]
Using this action you will be able to display the latest posts from your account to your [Github Profile Readme] or Update it in a [Github Gist] which can be pinned to your profile later & it can render the latest posts data in multiple styles.

### Setting up with Github Profile Readme
I assume that you already have created your [Github Profile Readme]

#### Step 1 :
Add the below content to your `README.md` file in **Github Profile**
```markdown
## My Latest Blog Posts 👇
<!-- HASHNODE_BLOG:START -->
<!-- HASHNODE_BLOG:END -->
```
![https://s2.do-spaces.com/2020/Nov/05/1604579158-16.jpg](https://s2.do-spaces.com/2020/Nov/05/1604579158-16.jpg)

#### Step 2 :
Create `blog.yml` file inside of `.github/workflows/` folder in your [Github Profile Readme] repository

```yml
name: "📚 Blog Updater"

on:
  workflow_dispatch:
  schedule:
    - cron: '0 0 * * *' # Runs Every Day

jobs:
  update_blogs:
    name: "Update Blogs"
    runs-on: ubuntu-latest
    steps:
      - name: "📥  Fetching Repository Contents"
        uses: actions/checkout@main

      - name: "📚  Hashnode Updater"
        uses: "varunsridharan/action-hashnode-blog@main"
        with:
          USERNAME: 'your-username'
          COUNT: 10
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

That's it now we have configured the workflow & README.md file. and the workflow is set to run once every day or when manually triggered. 

now navigate to the `Actions` tab in that repository, select the workflow that we added and click **RUN**

***How To Run Github Workflow Manually***

%[https://www.youtube.com/watch?v=nEJ-FkVVmzQ]


**Note**
> This action can be used with Gist or with any other repository 
> For more information on this action please check the GitHub repository

%[https://github.com/varunsridharan/action-hashnode-blog]


[Github Gist]: https://gist.github.com/
[Github Profile Readme]: https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-profile/managing-your-profile-readme
[Github]: https://github.com/varunsridharan
[blog]: https://blog.svarun.dev
[Hashnode Blogs Github Action]: https://github.com/varunsridharan/action-hashnode-blog