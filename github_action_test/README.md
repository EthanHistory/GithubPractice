https://docs.github.com/en/actions

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. You can create workflows that build and test every pull request to your repository, or deploy merged pull requests to production.

## Components of Github Actions
1. **Workflows**
    Workflow is a configurable automated process written by YAML file checked in to your repository. It is triggered by below ways.
    - an event
    - mannually
    - a defined schedule
    - posting to a REST API

2. **Events**
    An event is a specific activity in a repository that triggers a workflow run. For example, activity can originate from GitHub when someone creates a pull request, opens an issue, or pushes a commit to a repository. You can manage which event triggers which workflow. Here is [the event lists](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows) you can use to trigger workflows.

3. **Jobs**
   A job is a set of steps in a workflow that is executed on the same runner. Each step is either a shell script that will be executed, or an action that will be run. The meaning of using the same runner is that you can share data from one step to another. Basically, each job runs parallelly with other jobs. However, you can set dependencies on these jobs so that specific jobs run after dependent jobs finished. 

4. **Runner**
    A runner is a server that runs your workflows when they're triggered. Each runner can run a single job at a time.

## Create an example workflow

GitHub Actions uses YAML syntax to define the workflow. Each workflow is stored as a separate YAML file in your code repository, in a directory named `.github/workflows`.