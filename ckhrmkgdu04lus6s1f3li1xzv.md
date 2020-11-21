## How To Create A Github Action In Docker

In the previous blog, we have learnt how to create Github actions using `Node.js`. In this blog we will learn how to build a Github action using Docker. This will be similar to the **simple action** in `Node.js`, which will greet the user and set an output variable containing current timestamp.

## Prerequisites
1. You will need to have a basic understanding of Docker to start with, along with GitHub Actions environment variables and the Docker container filesystem. For better understanding, you can see the sections on  [Using environment variables](https://docs.github.com/en/free-pro-team@latest/actions/automating-your-workflow-with-github-actions/using-environment-variables) and [Virtual environments for GitHub"](https://docs.github.com/en/free-pro-team@latest/actions/automating-your-workflow-with-github-actions/virtual-environments-for-github-hosted-runners#docker-container-filesystem).
2. Create a new repository on Github. For the purposes of this blog, we will be working with a repository titled `simple-docker-action`
3. Clone the above repository to your local computer
4. Once cloned, using terminal, change directory to the repository as below:
`cd simple-docker-action`

## Creating the `action.yml` file
Create a new file `action.yml` in the `simple-docker-action` directory with the following example code:

```yml
name: 'Simple Docker Action'

description: 'Basic Docker Action Which uses AlpineOS'

inputs:
  who-to-greet:
    description: 'Who to greet'
    required: true
    default: 'World'

outputs:
  time:
    description: 'The time we greeted you'

runs:
  using: "docker"
  image: "Dockerfile"
  args:
    - ${{ inputs.who-to-greet }}

```

This metadata defines one `who-to-greet` input and one `time` output parameter. To pass inputs to the Docker container, you must declare the input using `inputs` and pass the input in the `args` keyword.  

> GitHub will build an image from your `Dockerfile`, and run commands in a new container using this image.

## Creating `entrypoint.sh`
You can choose any base Docker image and, therefore, any language for your action. The following shell script example uses the `who-to-greet` input variable to `print "Hello [who-to-greet]"` in the log file.

Next, the script gets the current time and sets it as an output variable that actions running later in a job can use. In order for GitHub to recognize output variables, you must use a workflow command in a specific syntax: `echo "::set-output name=<output name>::<value>"`. For more information, see [Workflow commands for GitHub Actions.](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-commands-for-github-actions#setting-an-output-parameter)

The entry point file mentioned in the Dockerfile under the **ENTRYPOINT** must be created in the repository. In this example, we have taken the entry point file as `entrypoint.sh`. Hence we will create a file called `entrypoint.sh` in the repository, and add the following code:

```bash
#!/bin/sh

# $1 will provide the value of who-to-greet
echo "Hello $1"

time=$(date)

echo "::set-output name=time::$time"
```

If `entrypoint.sh` executes without any errors, the action's status is set to success. You can also explicitly set exit codes in your action's code to provide an action's status. For more information, see [Setting exit codes for actions](https://docs.github.com/en/free-pro-team@latest/actions/creating-actions/setting-exit-codes-for-actions)


## Creating `Dockerfile`
In the repository, create a file called `Dockerfile`

> Dockerfile should be named exactly as `Dockerfile` with capital D, and no file extension.

### FROM
The first instruction in the `Dockerfile` must be ***FROM***, which selects a Docker base image. see the [FROM reference](https://docs.docker.com/engine/reference/builder/#from) in the Docker documentation

for the sake of this blog we will be using `Alpine Linux` as base image.

```
FROM alpine:latest
```

### COPY
Next step is to copy `entrypoint.sh` before we can execute it 
The COPY instruction copies new files or directories from `<src>` and adds them to the filesystem of the container at the path `<dest>`.
> Copies `entrypoint.sh` file from your action repository to the filesystem path `/` of the container

```
COPY entrypoint.sh /entrypoint.sh
```

### RUN
The `RUN` instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the `Dockerfile`.
> We need make `entrypoint.sh` executable since we copied the file to the runner.

```
RUN chmod +x /entrypoint.sh
```

### ENTRYPOINT
An `ENTRYPOINT` allows you to configure a container that will run as an executable.
> Code file to execute when the docker container starts up (`entrypoint.sh`)

```
ENTRYPOINT ["/entrypoint.sh"]
```

The final `Dockerfile` would look like below

```docker
FROM alpine:latest
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
```

## Testing out the action in a workflow
Before testing the code, make sure to commit the `action.yml`, `entrypoint.sh` and `Dockerfile` files and push to Github.

The workflow file for this action would look as below:

```yml
name: "Docker Simple"

on: [push]

jobs:
  docker_simple:
    runs-on: ubuntu-latest
    name: "A Simple Docker Action"
    steps:
      - name: "Greet & Output Time"
        id: hello
        uses: learn-with-varunsridharan/github-action/docker-action@main
        with:
          who-to-greet: 'Mona the Octocat'

      - name: "Get the output time"
        run: echo "The time was ${{ steps.hello.outputs.time }}"
```

## Output
When you run the above action with the exact code you should get output something like below

![Output](https://s2.do-spaces.com/2020/Nov/21/160595661851.jpg)


---

You can download / clone the source code from below Github Repository

%[https://github.com/learn-with-varunsridharan/github-action]


We will learn about _**Publishing Github Actions To Github Marketplace**_ in the next blog 

Do stay tuned.

---

%%[blog-footer]