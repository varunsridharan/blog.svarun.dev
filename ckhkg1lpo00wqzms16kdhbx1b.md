## What is Github action?

**The Github Action is a process that allows you to automate your software development workflow by making use of the built-in CI/CD mechanism**. CI/CD (Continuous Integration, Continuous Deployment, and Delivery) is a process that reduces the repetitive process of testing and deploying software. It can be used to trigger automated tasks that help to build, test, and deploy your code. 

Using Github Actions, you can use events that happen within repositories to trigger a workflow file to perform specified actions.

A simple illustration would work something like this. Let us say you have a repository containing a WordPress Plugin you have built, and would like to trigger certain actions (eg: post a comment to the issue with predefined FAQs and troubleshooting tips) when an issue is opened, deleted or each time an issue has a new comment. 


## Understanding the terms `Event`, `Workflow` and `Action`
What do the above terms mean, and which are they in our illustration?

### `EVENT`
‘Issue opened’, ‘issue deleted’, and ‘issue comment’ are called events. They trigger the action. 

### `ACTION`
An ‘action’ is the end task that runs when an ‘event’ happens. An action can be something existing that is created by the community or custom-created by you for your repository’s specific requirements. In our example ‘post comment with FAQs and troubleshooting’ is one action. Another could be ‘send an email notification to yourself’.

### `WORKFLOW`
The ‘workflow’ is the YML file located inside the workflows folder which actually links the ‘event’ to the ‘action’. The workflow contains the event (eg: issue opened) and specifies what action should run (eg: post comment with FAQs and troubleshooting).


### Setting up the Environment

These are the steps you would follow, to set up the workflow environment for a repository:

1. Creating the folder structure inside your repository.
1. Creating a workflow file to listen for an event happening (eg: new issue)
1. Specifying the actual action (eg: post FAQ comment) that powers the workflow

Since this blog article is specifically about Github's actions, I will skip going into the details of items 1 and 2 above, and focus on the actual action itself.

If you would like to know about steps 1 and 2, you can learn them from this blog: https://blog.gvasquez.dev/how-to-setup-github-actions-on-your-github-repository 

---

We will learn about specifying the actual action, which is the focus of this blog series, in the next blog titled ***The why, how and creation of Github actions.***

_Do stay tuned._

---

%%[blog-footer]
