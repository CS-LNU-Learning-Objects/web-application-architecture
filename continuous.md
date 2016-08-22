# The continuous way of web application development

*prior  knowledge  - Programming, Web development, Basic git handling*

This text will give you a introduction to terms like Continuous Integration (CI), Continuous Development (CDev) and Continuous Deployment (CDep). It will try to explain the difference between these terms and also try to answer the questions what and why.

To get a clearer image of these terms we need to take a look back. Software development has been a subject for many years, long before the web and web applications (which this text is focusing on). One common project model was the waterfall model. Every part in the development was made in isolated steps. First all the requirements were collected, when this was done - then the planning started, then the development and when the code was ready a integration phase begun and so on. The integration was often experienced as a game, nobody was sure it would work and how much time (and money) that would be spend to get the application running in production. Code that has been isolated for month should run together and hopefully everything in the application will work. Of course that wasn't the case in most projects. Since the code had grown isolated problem and bugs was implemented early in the code but the teams didn’t found them until the big integration, probably a integration with a tight time frame before a promised release. Problems that could had been solved easy become more complex and hard to fix and no one had the whole picture. A lot of stressed work is to be done and there will be a big risk that bugs find their way out to production.

Today we see more project that are using a more iterative model since we realized that software ideas change during the process. We have also realized that integration should be done continuously. We must found eventual problem and bugs as soon as possible in the process. This is what the term Continuous Integration (CI) is all about.

## A Continuous Integration workflow

The term came from the eXtreme Programming (XP) community [REF NEDDED] and has been around for a while. A team with many programmers produce different chunk of code handling different features of the application. The applications main code should live in a shared repository where developers push or merge code several times a day. This will start a integration process where the code should validates against static analyzes (like code hinting) and run tests. That will catch some of the bugs and problem early in the process and force the developers to fix this before it grows to a bigger problem.

As you see CI does not only refers to integration of code. In the CI pipeline you should also build and test your code within the development environment. Imagine we have a team of a couple of developers writing code for a specific application. They all share the same main “master branch” where the application code for production should live. The may all produce their code commit and push directly to the master, build and test then code. A more common way may be that each developer work on a specific task, a feature, a fix and so on and have this work in a own branch. When the developer is confident about her/his code the branch is merge into the master branch which is the first step in the CI pipline.

### A CI pipeline
When working in a CI inspired project you should set up a pipeline or workflow. Below is a suggestion taken from the book ["The devops 2.0 toolkit"](https://leanpub.com/the-devops-2-toolkit) by Viktor Farcic.
[IMAGE here]


1. **Pushing/merging**
As said before the developers are working either in different branches and merge the commits together or all developers push their commits directly to the master to integrate the code. This should be done several times a day to find problems as fast as possible.

2. **Static Analysis**
This means checking code for syntax error, runs some code hinting to check that the code standard is meet (optional). This is of course something that the developer should check by her/himself but the CI pipeline should have some automated tool that guarantee that code not following the correct standard will end up in the shared repository.

3. **Pre-deployed tests**
In this step runs all types of test that don´t need code to be deployed to a server. This is mainly [unit tests](#) or maybe some [functional tests](#). Tests running in this steps should be easy to write and fast to execute.

4. **Packing and deploying to test eniviroment**. In this your code files should be compressed and minified (or maybe turn into WAR- or JAR-files). Static stuff should be send to your CDN for faster presentation. If you are working with [containers](#Link to container) the container should be created with all it dependencies required to run your application. The container is deployed to a test eniviroment.

5. **Post-deployed testing**



Building and deploying to a test environment
Post-deploy tests

### Test, test, test


But remember, there are no silver bullets when talking about web application development.
,

What we must know is that there will never be silver bullets in software development. The complexity of the applications, projects, teams, technology and so on will always be different.