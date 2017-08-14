This is a template repository for quickly creating new Node.js microservices.

* [Start by reading the instructions.](https://github.com/Applifier/unity-ads-documentation/wiki/Setting-up-a-new-service)
* Clone this repository.
* Delete `.git` in your clone and `git init` if you don't want to keep the history of the template repo in your own repository.
* Replace `ads-common-template-node` with your own service name in these files
    * `Dockerfile`
    * `Dockerfile-compose`
    * `src/config.js`
* Remove this header part from your README and update the rest accordingly. (Also see [template_README.md](https://github.com/Applifier/unity-ads-documentation/blob/master/development/template_README.md) in the documentation repository.)
* Customize your build process, see `Jenkinsfile`. Remove commented configuration that you don't use and remove `extra_steps.groovy` if further customization is not required.
* Implement your service.
* Note: template uses most recent version of node and alpine variant of the image. If you require earlier version, want to use a specific version or require non-alpine version you need to edit FROM section of the Dockerfile (and Dockerfile-compose)

### Set Up Your Service To Kubernetes (Staging and Production)

You should set up your project to Kubernetes as early as possible, even, if you are not going live soon. Ideally your first pull request or commit to master could go to staging. You can ask help from TechOps how to do this or you can do it your self with following steps:

* Create feature branch under devops_root (ask special access from TechOps)
* Create manifest under `devops_root/kubernetes/deployments/ads/<application group>/manifests/<your_service_name>.yaml`
    * Your service name should be the name of your repository.
    * Application group is one of:
      * admin (all dashboards and admin utilities)
      * delivery (real time ad plan: comet, auction, brand etc...)
* You can use `devops-root/kubernetes/deployments/ads/sandbox/manifests/ads-common-template-node.yaml` as template. It contains instructions how to create deployment and service. This template is deployed to kubernetes using this manifest.
* If you want to use templated values in your manifest, you can define them in `<application group>.settings.rb`. E.g. if you have in your settings.rb:
  ```
            globals: {
                  "NODE_ENV" => "staging"
              },
  ```
  * You can use that value with: `"<%= node[:settings][:globals]["NODE_ENV"] %>"` in your manifest.yaml
* Create pull request with instructions how to verify that the service is up after it's deployed.
* To enable automated deployments in your project edit `Jenkinsfile`:
  ```
  Script {
    deploy = "kubernetes"
    cluster = "sandbox"
    deploy_prod = "true"
  }
  ```
  * Here `cluster_name` is same as application group above e.g. `admin` or `delivery`.
  * If you haven't set up kubernetes deployment yet, you should have just empty Script block in Jenkinsfile to disable deployments.


Same process applies to changes in your kubernetes environment also.

---

[![Greenkeeper badge](https://badges.greenkeeper.io/Applifier/ads-common-template-node.svg?token=e4d925d470c9d59e24c7c44b236913229cc0bbff4912ff0849717e4c6f3b7164&ts=1496059400495)](https://greenkeeper.io/)

# Project Title

One Paragraph of project description goes here

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```
Give examples
```

### Build

The command needed to compile/transpile the code into runnable code to the platform you're using

### Run

A step by step series of examples that tell you have to get a development env running

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Debugging

Sometimes we need to change things and we might not fully understand how it works.

List the commands and setup necessary to debug this application

Example:
```
npm run debug
```
or in your editor

```
Give an example
```


## Tests

Explain how to run the automated tests for this system

Example:
```
npm run test
```

### Debugging Tests

Explain what these tests test and why

Example:
```
npm run test:debug
```

### Coding style tests

Explain what these tests test and why

Example:
```
npm run lint
```

## Code Coverage

list the commands necessary to execute a code coverage

Example:
```
npm run coverage
```

## Logging

There should be some logging convention that needs to be linked or outlined here

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
