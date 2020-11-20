## Creating Github Action Using NodeJS With Github API

In the previous blog titled [**How To Create A GitHub Action In NodeJS**](https://blog.svarun.dev/how-to-create-a-github-action-in-nodejs) we understood on who to create Github Actions using NodeJS.

In this post we will learn how to create github action which interacts with Github API using [actions/core](https://github.com/actions/toolkit/tree/main/packages/core) AND [actions/github](https://github.com/actions/toolkit/tree/main/packages/github) npm packages

> If you haven't yet read the previous blog post. please stop here. first read it and come back.

## Prerequisites
1.	 [Download](https://nodejs.org/en/download/current/)  and install Node.js 12.x or newer, which includes npm
2.	Create a new repository on GitHub. For the purposes of this blog, we will be working with a repository titled `githubapi-nodejs-action`
3.	Clone the above repository to your local computer
4.	Once cloned, using terminal, change directory to the repository as below:
`cd githubapi-nodejs-action`
5.	From your terminal, initialize the directory with a `package.json` file using:
`npm init -y`
6. `@actions/core` NPM Package


## Creating the Action Metadata file
Create a new file **`action.yml`** in the `githubapi-nodejs-action` directory with the following example code: 

```yml
name: 'NodeJS Action With Github API'

description: 'use of the `@actions/core` & `@actions/github` package, which is advanced action demo'

runs:
  using: 'node12'
  main: 'dist/index.js'
```

## Writing Action's Javascript Code

Since we are interacting with the Github REST API, we first need to import the `@actions/github` library into the core variable, since the client for the REST API is included in the Octokit

```javascript
const github = require( '@actions/github' );
```

Since we are interacting with the API, we need an authentication token, which should be provided by the user in the workflow YML file. The token will be parsed to the REST API client, and the instance will be stored in a variable

```javascript
if( typeof process.env.GITHUB_TOKEN === 'undefined' ) {    
throw new Error( 'GITHUB_TOKEN ENV Variable Is Required' ); 
}
const octokit = github.getOctokit( process.env.GITHUB_TOKEN );
```

Information such as event name, payload and other repository information will be available through `github.context`, which we will save in the `context` variable

```javascript
const context = github.context;
```

Now comes the actual action which **creates a new issue** in the current repository. Using the repository information in the `context` variable, we will add the issue to the repository.

```javascript
await octokit.issues.create( {
	...context.repo,
	title: `New issue! | Action Runner ID #${process.env.GITHUB_RUN_NUMBER}`,
	body: `Hello There,
	Current Time Is : ${time}
	`
} );
```

The complete code would look as below:

```javascript
const core   = require( '@actions/core' );
const github = require( '@actions/github' );

async function run() {
	try {
		if( typeof process.env.GITHUB_TOKEN === 'undefined' ) {
			throw new Error( 'GITHUB_TOKEN ENV Variable Is Required' );
		}

		const octokit = github.getOctokit( process.env.GITHUB_TOKEN );
		const context = github.context;
		const time    = ( new Date() ).toTimeString();

await octokit.issues.create( {
	...context.repo,
	title: `New issue! | Action Runner ID #${process.env.GITHUB_RUN_NUMBER}`,
	body: `Hello There,
	Current Time Is : ${time}
	`
} );

	} catch( error ) {
		core.setFailed( error.message );
	}
}

run();

```

_Please note that Github does not check or install any dependencies. The action code you create must be full packaged containing all dependencies within._

> To package your Github action, please install the [vercel/ncc](https://github.com/vercel/ncc) NPM package, which is a simple CLI for compiling a Node.js module into a single file, together with all its dependencies, gcc-style.

> After installing the [vercel/ncc](https://github.com/vercel/ncc) package, you must include a `prepare` statement in your package.json, which ensures that the compiler runs automatically each time you update the dependencies. Make sure to run `npm run prepare` before pushing to the repository each time.

```json
"scripts": {
    "prepare": "ncc build ./src/index.js -o dist --source-map --license licenses.txt"
},
```

The workflow file for this action, would look like the below:

```yml
name: "NodeJS Action With Github API"

on: [push]

jobs:
  nodejs_action_with_github_api:
    runs-on: ubuntu-latest
    name: "A Advanced Node JS Action"
    steps:
      - name: "Create Issue With Current Time"
        uses: learn-with-varunsridharan/github-action/githubapi-nodejs-action@main
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Output
When you run the above action with the exact code you should get output something like below

### Workflow Output

![Output](https://s2.do-spaces.com/2020/Nov/20/160586903061.jpg)

### Example Issue

![Example](https://s2.do-spaces.com/2020/Nov/20/160586907169.jpg)


---
You can download / clone the source code from below Github Repository

%[https://github.com/learn-with-varunsridharan/github-action]

---

%%[blog-footer]
