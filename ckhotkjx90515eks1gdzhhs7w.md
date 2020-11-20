## How To Create A GitHub Action In NodeJS

This guide uses the GitHub Actions Toolkit Nodejs module to speed up development. For more information, see the [actions/toolkit](https://github.com/actions/toolkit) repository.

> To ensure your JavaScript actions are compatible with all GitHub-hosted runners ( `Ubuntu`, `Windows`, & `macOS` ), the packaged JavaScript code should be in pure JavaScript and not rely on other binaries. 
> If it does rely on binaries, you should pack them alongside the code.

## Toolkit Helper Packages
GitHub provides a ready-available library of toolkit packages for Node.js which can be used to build the JavaScript actions. We will look at some of them briefly as below:

#### ✔️ [@actions/core](https://github.com/actions/toolkit/tree/main/packages/core)
This package provides a set of functions for handling inputs, outputs, results, logging, secrets and variables. Run `npm install @actions/core` to install this package.

#### 🏃 [@actions/exec](https://github.com/actions/toolkit/tree/main/packages/exec)
This package provides a function to execute commands in shell. Run `npm install @actions/exec` to install this package.

#### 🍨 [@actions/glob](https://github.com/actions/toolkit/tree/main/packages/glob)
This package provides a function to search for files matching glob patterns. Run `npm install @actions/glob` to install this package.

#### ✏️ [@actions/io](https://github.com/actions/toolkit/tree/main/packages/io)
This package provides a function to handle disk i/o functions like cp, mv, rmRF, find etc.. Run `npm install @actions/io` to install this package.

#### [@actions/github](https://github.com/actions/toolkit/tree/main/packages/github)
This package provides a set of functions to interact with Github’s REST API. Run `npm install @actions/github` to install this package.

_Please note that Github does not check or install any dependencies. The action code you create must be full packaged containing all dependencies within._

> To package your Github action, please install the `[@vercel/ncc]` NPM package, which is a simple CLI for compiling a Node.js module into a single file, together with all its dependencies, gcc-style.

> After installing the `[@vercel/ncc]` package, you must include a `prepare` statement in your package.json, which ensures that the compiler runs automatically each time you update the dependencies. Make sure to run `npm run prepare` before pushing to the repository each time.

```javascript
"scripts": {
    "prepare": "ncc build ./src/index.js -o dist --source-map --license licenses.txt"
  },
```


## Prerequisites
1.	 [Download](https://nodejs.org/en/download/current/)  and install Node.js 12.x or newer, which includes npm
2.	Create a new repository on GitHub. For the purposes of this blog, we will be working with a repository titled `simple-nodejs-action`
3.	Clone the above repository to your local computer
4.	Once cloned, using terminal, change directory to the repository as below:
`cd simple-nodejs-action`
5.	From your terminal, initialize the directory with a `package.json` file using:
`npm init -y`
6. `@actions/core` NPM Package

---

# Simple Github Action
We will be creating a Github action which will greet user and sets a output variable containing current timestamp.

## Creating the Action Metadata file
Create a new file **`action.yml`** in the `simple-nodejs-action` directory with the following example code: 

```yml
name: 'NodeJS Simple Action'

description: 'use of the `@actions/core` package, which is a simple action'

inputs:
  who-to-greet:  # id of input
    description: 'Who to greet'
    required: true
    default: 'World'

outputs:
  time: # id of output
    description: 'The time we greeted you'

runs:
  using: 'node12'
  main: 'dist/index.js'

```


Let us analyze the contents of the `action.yml` file, for better understanding:

The `runs` sections tells the runner that the action runs `using` **node12**, and that the the `main` **index.js** file is the one that contains the actual code for the action.

The `inputs` are the parameters passed to the action as input, and the `required` tells the runner that inputs are required. The `output` contains the `description` of the output parameter.

## Writing Action's Javascript Code

The first step in writing a simple action would be to install & import the `@actions/core` NPM library.

Run `npm install @action/core` to install and import it in the code like below

```javascript
const core = require( '@actions/core' );
```

Next, you need to get the input parameters from the user. In this example, we will consider a parameter named `who-to-greet`. You would do this as below:

```javascript
const nameToGreet = core.getInput( 'who-to-greet' );
```

Next, print the input parameters, in our case `nameToGreet`, to the Github action runner as below:

```javascript
core.info( `Hello ${nameToGreet}!` );
```

Next, set the output parameters. In this case, we are taking the current time as the output. This is done as below:
```javascript
core.setOutput( "time", time );
```

The final code would be as shown below:

```javascript
// Imports @actions/core npm library into core variable
const core = require( '@actions/core' );

try {
	// Get The Input Value of `who-to-greet`
	const nameToGreet = core.getInput( 'who-to-greet' );

	// Prints The Value of nameToGreet in Github Action
	core.info( `Hello ${nameToGreet}!` );

	// Fetchs The Current Time
	const time = ( new Date() ).toTimeString();

	// Sets The Time As Output
	core.setOutput( "time", time );
} catch( error ) {
	core.setFailed( error.message );
}
```

As soon as you finish the code, you must build the package and push to Github. **Make sure to follow the steps mentioned at the end of the _Toolkit Helper Packages_ section.**


The workflow file for this action, would look like the below:

```yml
name: "NodeJS Simple"

on: [push]

jobs:
  nodejs_simple:
    runs-on: ubuntu-latest
    name: "A Simple Node JS Action"
    steps:
      - name: "Greet & Output Time"
        id: hello
        uses: learn-with-varunsridharan/github-action/nodejs-simple@main
        with:
          who-to-greet: 'Mona the Octocat'

      - name: "Get the output time"
        run: echo "The time was ${{ steps.hello.outputs.time }}"
```

## Output

When you run the above action with the exact code you should get output something like below

![Output Image](https://s2.do-spaces.com/2020/Nov/19/1605786108-159.jpg)


You can download / clone the source code from below Github Repository

%[https://github.com/learn-with-varunsridharan/github-action]

---

We will learn about _**Creating Github Action With Github REST-API Using Javascript**_ in the next blog 

Do stay tuned.

---

%%[blog-footer]
