
# TimeOff.Management

Web application for managing employee absences.

<a href="https://travis-ci.org/timeoff-management/timeoff-management-application"><img align="right" src="https://travis-ci.org/timeoff-management/timeoff-management-application.svg?branch=master" alt="Build status" /></a>

## Features

**Multiple views of staff absences**

Calendar view, Team view, or Just plain list.

**Tune application to fit into your company policy**

Add custom absence types: Sickness, Maternity, Working from home, Birthday etc. Define if each uses vacation allowance.

Optionally limit the amount of days employees can take for each Leave type. E.g. no more than 10 Sick days per year.

Setup public holidays as well as company specific days off.

Group employees by departments: bring your organisational structure, set the supervisor for every department.

Customisable working schedule for company and individuals.

**Third Party Calendar Integration**

Broadcast employee whereabouts into external calendar providers: MS Outlook, Google Calendar, and iCal.

Create calendar feeds for individuals, departments or entire company.

**Three Steps Workflow**

Employee requests time off or revokes existing one.

Supervisor gets email notification and decides about upcoming employee absence.

Absence is accounted. Peers are informed via team view or calendar feeds.

**Access control**

There are following types of users: employees, supervisors, and administrators.

Optional LDAP authentication: configure application to use your LDAP server for user authentication.

**Ability to extract leave data into CSV**

Ability to back up entire company leave data into CSV file. So it could be used in any spreadsheet applications.

**Works on mobile phones**

The most used customer paths are mobile friendly:

* employee is able to request new leave from mobile device

* supervisor is able to record decision from the mobile as well.

**Lots of other little things that would make life easier**

Manually adjust employee allowances
e.g. employee has extra day in lieu.

Upon creation employee receives pro-rated vacation allowance, depending on start date.

Email notification to all involved parties.

Optionally allow employees to see the time off information of entire company regardless of department structure.

## Screenshots

![TimeOff.Management Screenshot](https://raw.githubusercontent.com/timeoff-management/application/master/public/img/readme_screenshot.png)

## Installation

### Cloud hosting

Visit http://timeoff.management/

Create company account and use cloud based version.

### Self hosting

Install TimeOff.Management application within your infrastructure:

(make sure you have Node.js (>=4.0.0) and SQLite installed)

```bash
git clone https://github.com/timeoff-management/application.git timeoff-management
cd timeoff-management
npm install
npm start
```
Open http://localhost:3000/ in your browser.

## Run tests

We have quite a wide test coverage, to make sure that the main user paths work as expected.

Please run them frequently while developing the project.

Make sure you have Chrome driver installed in your path and Chrome browser for your platform.

If you want to see the browser execute the interactions prefix with `SHOW_CHROME=1`

```bash
USE_CHROME=1 npm test
```

(make sure that application with default settings is up and running)

Any bug fixes or enhancements should have good test coverage to get them into "master" branch.

## Updating existing instance with new code

In case one needs to patch existing instance of TimeOff.Managenent application with new version:

```bash
git fetch
git pull origin master
npm install
npm run-script db-update
npm start
```

## Solution
For this scenario we will use some of the most useful and intuitive AWS services that give us facility to implement an CI/CD automation. Some of those services will be:
### AWS CodePipeline

AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates. CodePipeline automates the build, test, and deploy phases of your release process every time there is a code change, based on the release model you define.

### AWS CodeBuild

AWS CodeBuild is a fully managed continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy. With CodeBuild, you don’t need to provision, manage, and scale your own build servers

### Amazon Elastic Container Registry

Amazon Elastic Container Registry (ECR) is a fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images. Amazon ECR is integrated with Amazon Elastic Container Service (ECS), simplifying your development to production workflow. Amazon ECR eliminates the need to operate your own container repositories or worry about scaling the underlying infrastructure

### Amazon Elastic Container Service

Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service. ECS is a great choice to run containers for several reasons. One of the most important is that you can choose to run your ECS clusters using AWS Fargate, which is serverless compute for containers. Fargate removes the need to provision and manage servers, lets you specify and pay for resources per application, and improves security through application isolation by design.

### AWS CloudFormation

AWS CloudFormation gives you an easy way to model a collection of related AWS and third-party resources, provision them quickly and consistently, and manage them throughout their lifecycles, by treating infrastructure as code. A CloudFormation template describes your desired resources and their dependencies so you can launch and configure them together as a stack. You can use a template to create, update, and delete an entire stack as a single unit, as often as you need to, instead of managing resources individually.

## Diagrams

The Following diagram shows the CI/CD flow used for this scenario 
(IMAGEN)

The Following diagram shows the Infrastructure used for this scenario
(IMAGEN)

## Deploying the infrastructure

### Prerequisites 

Because we will integrate a GitHub repository with AWS CodeBuild, first, me must create a connection between these 2 platforms. For this we’ll follow the steps that are defined in the following documentation:

https://docs.aws.amazon.com/codepipeline/latest/userguide/connections-github.html

This operation isn’t allowed to be automated because it must be performed using your GitHub credentials and it will only be executed once.
Once we have the connection created, we will get something like this:
![GitHub_Connection](https://github.com/joemaster9/timeoff-management-application/blob/master/img/github-connection.png)

The ARN of this connection will be used in the CodeBuild Service Role to allow a full clone when a change is made in the reposiroty.

### Deploying the infrastructure as code on AWS

In this section, we will deploy the necessary resources to run our application and the CI/CD solution. All the files will be in the “iac” folder.
![GitHub_Connection](https://github.com/joemaster9/timeoff-management-application/blob/master/img/iac-snapshot.png)

First of all we will need to create an Cloudformation Stack with the “amazon-lab-vpc.yaml” template, this stack will create all the necessary networking services that will be used for the rest for the rest of the services.

The second part of this deployment will be the “template.yaml” template that will contain the infrastructure necessary to run CI/CD services and our application successfully.

## Feedback

Please report any issues or feedback to <a href="https://twitter.com/FreeTimeOffApp">twitter</a> or Email: pavlo at timeoff.management

