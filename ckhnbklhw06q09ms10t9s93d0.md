## Creating and working with action.yml

GitHub actions, irrespective of the chosen environment, require a metadata file, which contains information such as title, description, author, etc., and also defines the inputs, outputs and entry-point for the action. GitHub uses this file to understand that the information contained identifies an action.

Action metadata files use the **`YAML`** syntax, identified by a **`.yml`** or **`.yaml`** extension. The action metadata file is named **`action.yml`**. If you're new to YAML, you can [read more here](https://www.codeproject.com/Articles/1214409/Learn-YAML-in-five-minutes).

## Action Metadata

![Meta Info](https://s2.do-spaces.com/2020/Nov/18/1605698511-182.png)

The **`action.yml`** relies on seven metas, some of which are required, and others optional, as shown below:

| Meta | Description |
| :--- | :--- |
| `name` * | The name of your action. GitHub displays the name in the **actions workflow run log** and in the **actions marketplace**. |
| `author` | The name of the action's author. |
| `description` | A short description of the action. |
| `inputs` | Input parameters allow you to specify data that the action expects during runtime. These are stored as environment variables. It is recommended to use lowercase input ids (Uppercase is automatically converted to lowercase). |
| `outputs` | Output parameters allow you to declare data that an action produces. For actions that run in succession, the output data of one action can in turn be used as input for the next action. |
| `runs` * | Configures the path to the action's code and the application used to execute the code. |
| `branding` * | You can use a color and Feather icon to create a badge to personalize and distinguish your action. Badges are shown next to your action name in the GitHub Marketplace. |

_* Required Field_

The **inputs**, **outputs**, **runs** and **branding** meta contains multiple parameters each, and hence requires an exploration in-depth, which we will learn below.

---

## inputs

![Inputs Args](https://s2.do-spaces.com/2020/Nov/18/1605695888-195.jpg)

Input parameters allow you to specify data that the action expects to use during runtime. These are stored as environment variables. It is recommended to use lowercase input ids (Uppercase variables are automatically converted to lowercase).

There are four **input parameters** that an action permits, as shown below:

| Meta | Type | Description |
| :--- | :--- | :--- |
| `inputs.<id>` *  | _string_ | Unique identifier within the inputs object. The value of <id> is a map of the input's metadata. It must start with a letter or `_` and contain only alphanumeric characters, `-`, or `_`. |
| `inputs.<id>.description` *  | _string_ | Description of the input parameter. |
| `inputs.<id>.required` *  | _boolean_ | Indicates if the action requires the input parameter. `true` if the parameter is required. |
| `inputs.<id>.default`  | _string_ | Represents a default value. It is used when an input parameter isn't specified in a workflow file. |


_* Required Field_

---

## outputs

![Output Args](https://s2.do-spaces.com/2020/Nov/18/1605696070-163.jpg)

Output parameters allow you to declare data that an action produces as output. For actions that run in succession, the output data of one action can in turn be used as input for the next action.

There are two **output parameters** that an action permits, as shown below:

| Meta | Type | Description |
| :--- | :--- | :--- | :--- |
| `outputs.<id>` * | _string_ | Unique identifier within the `outputs` object. The value of `<id>` is a map of the outputs’s metadata. It must start with a letter or `_` and contain only alphanumeric characters, `-`, or `_`. |
| `outputs.<id>.description` * | _string_ | Description of the output parameter. |

_* Required Field_

---

## runs
Configures the path to the action's code and the application used to execute the code. The `runs` meta contains a separate set of parameters which is environment-specific. These are discussed environment-wise as below:


### JavaScript Action

![JSArgs](https://s2.do-spaces.com/2020/Nov/18/1605696523-18.jpg)

The `runs` meta for a JavaScript action, contains six parameters as detailed below:

| Meta | Description |
| :--- | :--- | :--- |
| `using` * | The application used to execute the code specified in `main`. |
| `main` * | The file containing the action code. |
| `pre` | Run a script at the start of a job before `main:` begins, such as a prerequisite setup script. Always runs by default, but can be overridden using `pre-if` |
| `pre-if` | Define conditions for `pre:`, which will only run if the conditions in `pre-if` are met. If not set, then `pre-if` defaults to always(). |
| `post` | Run a script at the end of a job after `main:` has completed. For example, you can use `post:` to terminate certain processes or remove unneeded files. |
| `post-if` | Define conditions for `post:` execution, which will only run if the conditions in `post-if` are met. If not set, then `post-if` defaults to always(). |


_* Required Field_

###  Docker Action

![DockerArgs](https://s2.do-spaces.com/2020/Nov/18/1605696794-130.jpg)

The `runs` meta for a Docker actions, contains seven parameters as detailed below:

| Meta | Description |
| :--- | :--- | :--- |
| `using` * | You must set this value to 'docker'. |
| `pre-entrypoint` | Run a script before the entrypoint action begins. For example, you can use `pre-entrypoint:` to run a prerequisite setup script. Always runs by default but can be overridden using `pre-if`. |
| `pre-if` | Define conditions for `pre-entrypoint:`, which will only run if the conditions in `pre-if` are met. If not set, then `pre-if` defaults to always(). |
| `image` * | The Docker image to use as the container to run the action. Can be Docker base image name, a local Dockerfile, or public image in Docker Hub or another registry. To reference local Dockerfile, use a relative path to your action metadata file. |
| `env` | Key/value map of environment variables to set in the container environment. |
| `entrypoint` | Used when Dockerfile does not specify ENTRYPOINT or you want to override the ENTRYPOINT |
| `post-entrypoint` | Run scripts after `entrypoint` action is complete. For example, cleanup scripts. This runs by default but can be overridden using `post-if`. |
| `post-if` | Define conditions for `post:` execution, which will only run if the conditions in `post-if` are met. If not set, then `post-if` defaults to always(). |
| `args` | Array of strings that define the inputs for a Docker container, which can include hardcoded strings. GitHub passes the args to the container's ENTRYPOINT when the container starts up. |

_* Required Field_

---

## branding

![Branding](https://s2.do-spaces.com/2020/Nov/18/1605696970-113.jpg)

The `branding` meta contains two parameters, both of which are required if you are publishing to a marketplace, otherwise are optional. They are as below:

| Meta | Description |
| :--- | :--- |
| `color` | Background color of the badge. Can be: `white`, `yellow`, `blue`, `green`, `orange`, `red`, `purple`, or `gray-dark`. |
| `icon` | The name of the icon to use. Refer [Feather Icons](https://feathericons.com/) for names. |

_* Required Field_

> [haya14busa](https://twitter.com/__haya14busa__) has created a ***GitHub Actions Branding Cheat sheet*** which you can use to find icon & color for your GitHub action 

%[https://github.com/haya14busa/github-action-brandings]

---

We will learn about _**Creating Github Actions Using Javascript**_ in the next blog 

Do stay tuned.

---

%%[blog-footer]