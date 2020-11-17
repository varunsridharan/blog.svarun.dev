## The why, how and creation of GitHub actions

## Why use Github actions?
Much of software development involves repetitive tasks, which consumes a major chunk of time. This time can be more efficiently used by the developers in actually producing code, instead of on these repetitive tasks, which can easily be automated by GitHub actions.

Further, repetitive tasks tend to become mundane, and can easily cause a step or two to be missed when routinely performing the same tasks. Github actions help automate these tasks and ensure that every step is run precisely each time.

When multiple developers or development teams are working on a large project, CI/CD becomes the core requirement, which allows developers to commit code without affecting the work of others in the team. GitHub actions with its built-in CI/CD fit the bill perfectly.

---

## How Github actions can be useful?
The possibilities for GitHub actions are endless. You can make use of useful actions already created by the community, or create customized actions that suit your requirements as needed by your repository.


Generally, Github actions can be useful for four primary groups of tasks:

### 1. Code Scanning
![Code Scanning](https://github.blog/wp-content/uploads/2020/09/94614428-fd9a6b80-025a-11eb-85c5-f71a22a3cdee-1.png)

Each time a file is committed to the repository, the workflow can be used to trigger an action to scan the code for ‘malicious’ or ‘erroneous’ content. If such content is detected, the developer can be notified via email. Further, the action can also be used to check for sensitive content accidentally left in the file during development, such as passwords or API tokens.

This helps in consistently keeping the code clean, the developer safe from accidentally publishing sensitive content, as well as the users safe from downloading and using malicious or erroneous code.

### 2. Coding Standards

![Others](https://github.blog/wp-content/uploads/2019/03/editor-tools-social-1.png?w=1200)

An action can be used to scan the committed file and ensure that all the relevant coding standards have been followed by the developer. Accordingly, the developer can be notified via email regarding notices, warnings, and breaches in the standards, for necessary rectification.

This helps make sure the content committed is always up to coding standards and can easily be followed by fellow developers, ensuring ease of maintenance and ongoing development.

### 3. Building, Publishing, and Deploying Code

![Build,Publish](https://github.blog/wp-content/uploads/2020/04/eanderson-devops-culture.jpeg?w=1200)

Most software packages begin as source files written by developers in human-readable code and are required to be compiled into a machine-readable installation package. Github action can be used to automatically build the code from source files as needed, which would then be suitable for publishing or deployment. 

Once the code is built, the action can go further and either publish the package (eg: WordPress Plugins) or deploy the same to a live server. This automation eliminates a plethora of possible errors that can be committed by the developer at each stage.

### 4. Miscellaneous

![Others](https://s2.do-spaces.com/2020/Nov/17/1605608821-174.jpg)

Github actions can also be used to perform routine tasks which commonly plague software developers such as sending email to users when a new version is launched, auto-updating the changelog, etc.

The creation of actions in Github is only limited by the extent of your customization and the requirement of your repository. Actions can be integrated with GitHub's APIs and any publicly available third-party API.

---

## Ways to create Github actions
Github actions can be created in three environments, depending on the Operating system:

| Environment | Linux | Windows | MacOS |
| --- | --- | --- | --- |
| Docker container | ✔️ | ❌ | ❌ |
| JavaScript | ✔️ | ✔️ | ✔️ |
| Composite run steps | ✔️ | ✔️ | ✔️ |


### Docker Container

![Docker Container](https://s2.do-spaces.com/2020/Nov/17/1605609856-144.jpg)

Actions using the Docker container can only execute on the Linux OS. You must use a Linux OS and have Docker installed to run Docker container actions. The Docker container allows you to use specific versions of an OS, dependencies, tools, and code. It is more consistent and reliable because the consumer of the action need not worry about the tools or dependencies.  

Do keep in mind though, that because of the latency to build and retrieve the container, Docker container actions are slower than JavaScript actions.  

### JavaScript actions

![JS](https://s2.do-spaces.com/2020/Nov/17/1605609910-135.jpg)

This simplifies the action code and executes faster than a Docker container action. To ensure compatibility with GitHub-hosted runners (Ubuntu, Windows, and macOS), JS actions must be written in pure JavaScript and not rely on other binaries. If you're developing a Node.js project, the [GitHub Actions Toolkit](https://github.com/actions/toolkit) provides packages that you can use in your project to speed up development.

### Composite run steps actions

![Composite](https://s2.do-spaces.com/2020/Nov/17/1605610241-148.jpg)

This allows you to combine multiple workflow run steps within one action. For example, you can use this feature to bundle together multiple run commands into an action, and then have a workflow that executes the bundled commands a single step using that action. To see an example, check out the [documentation](https://docs.github.com/en/free-pro-team@latest/actions/creating-actions/creating-a-composite-run-steps-action).

I will discuss the steps for creating actions in the Docker container and Javascript environments in this blog series.

---

We will learn about _action.yml_  metadata file,

in the next blog titled ***Creating and working with action.yml***

Do stay tuned.

---

%%[blog-footer]
