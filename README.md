I wrote a blog post a long time ago about TFS and DevOps. A lot has changed since that last post with multiple different version of the build pipeline being released. Microsoft has been working hard to create a better experience for build automation and continuous integration. Recently they released the idea of multi-stage pipelines that work and feel much like how GitLab CI works.

In this post I'll walk through a basic YAML file and show how you can get a C# project up build and tested quickly.

# Setup

We need to have a project that is checked into DevOps before we begin. I have a repository that I made for this blog up on DevOps that is a basic dotnet core console application and a unit test project that goes along with it. At the time of writing this blog post you will also need to turn on the multi-sgae pipelines Preview Feature in order to get the best view for these pipelines. You can do that by clicking on the user settings button

![user settings](images/user-settings.png)

Then click on preview features

![preview features](images/preview-features.png)

Then ensure that multi-stage pipelines are enabled

![mult-stage pipelines](images/multi-stage-pipelines.png)



# First Steps

First we need to add a yaml file into our project. I tend to put this file directly at root and name it like azure-pipelines.yaml. Then we need to define our stages. A stage is a collection of jobs and can be run concurrently or can be dependent on another stage successfuly completing. For this quick project we will have two different stages
	• Build
	• Test

In order to define these stages in our pipeline we need to write some YAML like

``` yaml
stages:
  - stage: build
    displayName: Build
  - stage: test
    displayName: Test
    dependsOn:
    - build
```

this will give us our building blocks to add our jobs.